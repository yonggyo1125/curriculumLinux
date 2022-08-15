# Zabbix 6.0 설치하기

## Apache 웹서버 설치하기

[Apache httpd : 설치 참조](https://github.com/yonggyo1125/curriculumLinux/tree/master/Linux2/8~9%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%9B%B9%20%EC%84%9C%EB%B2%84#apache-httpd--%EC%84%A4%EC%B9%98)

## PHP 7.4 버전 설치

[PHP 7.4 : Install 참조](https://github.com/yonggyo1125/curriculumLinux/tree/master/Linux2/8~9%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%9B%B9%20%EC%84%9C%EB%B2%84#php-74--install)

## MariaDB 10.8 서버 설치

[MariaDB 설치와 운용 참고](https://github.com/yonggyo1125/curriculumLinux/tree/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84#mariadb-%EC%84%A4%EC%B9%98%EC%99%80-%EC%9A%B4%EC%98%81)


## Zabbix 설치

- Install required PHP modules and Add Zabbix repository.

```
[root@dlp ~]# dnf -y install php-mysqlnd php-gd php-xml php-bcmath php-ldap
[root@dlp ~]# dnf -y install https://repo.zabbix.com/zabbix/6.0/rhel/8/x86_64/zabbix-release-6.0-1.el8.noarch.rpm
```

- Install Zabbix Server. To monitor Zabbix Server itself, Install Zabbix Agent, too.
```
[root@dlp ~]# dnf -y install zabbix-server-mysql zabbix-web-mysql zabbix-apache-conf zabbix-sql-scripts zabbix-selinux-policy zabbix-agent
```

- Create a database for Zabbix.

```
[root@dlp ~]# mysql

MariaDB [(none)]> create database zabbix; 
Query OK, 1 row affected (0.00 sec)

# replace any password for DB [password]
MariaDB [(none)]> grant all privileges on zabbix.* to zabbix@'localhost' identified by 'password'; 
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> flush privileges; 
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> exit 
```

```
[root@dlp ~]# zcat /usr/share/doc/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -p zabbix
Enter password:   # password of zabbix user on MariaDB you set above
```

- Configure and start Zabbix Server.

```
[root@dlp ~]# vi /etc/zabbix/zabbix_server.conf
# line 94 : add
DBHost=localhost
# line 130 : add Zabbix DB password
DBPassword=password
[root@dlp ~]# systemctl enable --now zabbix-server
```

- If SELinux is enabled, change policy like follows.

```
[root@dlp ~]# setsebool -P zabbix_can_network on
[root@dlp ~]# setsebool -P httpd_can_connect_zabbix on
[root@dlp ~]# setsebool -P domain_can_mmap_files on
[root@dlp ~]# setsebool -P daemons_enable_cluster_mode on
```

```
[root@dlp ~]# vi zabbix_server.te
# create new
module zabbix_server 1.0;

require {
        type initctl_t;
        type devlog_t;
        type proc_kcore_t;
        type zabbix_t;
        type zabbix_agent_t;
        type rpm_exec_t;
        type rpm_var_lib_t;
        class fifo_file getattr;
        class sock_file getattr;
        class file { execute execute_no_trans map open getattr };
        class capability dac_override;
}

#============= zabbix_t ==============
allow zabbix_t self:capability dac_override;

#============= zabbix_agent_t ==============
allow zabbix_agent_t devlog_t:sock_file getattr;
allow zabbix_agent_t initctl_t:fifo_file getattr;
allow zabbix_agent_t proc_kcore_t:file getattr;
allow zabbix_agent_t rpm_var_lib_t:file open;
allow zabbix_agent_t rpm_exec_t:file { execute execute_no_trans map };

[root@dlp ~]# checkmodule -m -M -o zabbix_server.mod zabbix_server.te
[root@dlp ~]# semodule_package --outfile zabbix_server.pp --module zabbix_server.mod
[root@dlp ~]# semodule -i zabbix_server.pp
```

- If Firewalld is running, allow Zabbix related ports.

```
[root@dlp ~]# firewall-cmd --add-service={http,https}
success
[root@dlp ~]# firewall-cmd --add-port={10051/tcp,10050/tcp}
success
[root@dlp ~]# firewall-cmd --runtime-to-permanent
success
```

- Configure and start Zabbix Agent to monitor Zabbix Server itself.

```
[root@dlp ~]# vi /etc/zabbix/zabbix_agentd.conf
# line 117 : specify Zabbix server
Server=127.0.0.1
# line 164 : specify Zabbix server
ServerActive=127.0.0.1
# line 175 : change to the own hostname
Hostname=dlp.srv.world
[root@dlp ~]# systemctl enable --now zabbix-agent
```

- Change httpd settings. That's OK to configure Zabbix Server.

```
[root@dlp ~]# vi /etc/httpd/conf.d/zabbix.conf
# line 12 : add access permittion for Zabbix Web frontend if you need
# by default, All are allowed
#Require all granted
Require ip 127.0.0.1 10.0.0.0/24
[root@dlp ~]# systemctl restart httpd php-fpm
```