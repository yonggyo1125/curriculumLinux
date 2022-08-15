# Apache httpd : 설치

- httpd 설치

```
[root@www ~]# dnf -y install httpd
# welcome 페이지 이름변경 또는 삭제
[root@www ~]# mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf.org
```

- httpd 설정. 서버 이름을 현재 환경에 맞게 적절하게 변경.

```
[root@www ~]# vi /etc/httpd/conf/httpd.conf
# line 89 : change to admin's email address
ServerAdmin root@srv.world

# line 98 : change to your server's name
ServerName www.srv.world:80

# line 147 : change (remove [Indexes])
Options FollowSymLinks

# line 154 : change
AllowOverride All

# line 167 : add file name that it can access only with directory's name
DirectoryIndex index.html index.php index.cgi
# add follows to the end
# server's response header
ServerTokens Prod
[root@www ~]# systemctl enable --now httpd
```

- 방화벽이 동작 중이라면  HTTP 서비스나 .  80/TCP 포트를 허용해 준다.

```
[root@www ~]# firewall-cmd --add-service=http --permanent
success
[root@www ~]# firewall-cmd --reload
success
```

- 페이지 동작 테스트

```

[root@www ~]# vi /var/www/html/index.html
<html>
<body>
<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
Test Page
</div>
</body>
</html>
```

* * * 
# Apache httpd : Virtual Hostings

Virtual Hosing을 설정하여 여러 도메인에서 서버를 공유할 수 있도록 한다.

```
[root@www ~]# vi /etc/httpd/conf.d/vhost.conf
# create new
# settings for original domain
<VirtualHost *:80>
    DocumentRoot /var/www/html
    ServerName www.srv.world
</VirtualHost>

# settings for new domain
<VirtualHost *:80>
    DocumentRoot /var/www/virtual.host
    ServerName www.virtual.host
    ServerAdmin webmaster@virtual.host
    ErrorLog logs/virtual.host-error_log
    CustomLog logs/virtual.host-access_log combined
</VirtualHost>

<Directory "/var/www/virtual.host">
    Options FollowSymLinks
    AllowOverride All
</Directory>

[root@www ~]# mkdir /var/www/virtual.host
[root@www ~]# chmod 755 /var/www/virtual.host
[root@www ~]# systemctl restart httpd
```

```

[root@www ~]# vi /var/www/virtual.host/index.html
<html>
<body>
<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
Virtual Host Test Page
</div>
</body>
</html>
```
* * * 
# Apache httpd : Enable Userdir

- UserDir 설정을 활성화 한다.

```
[root@www ~]# vi /etc/httpd/conf.d/userdir.conf
# line 17 : comment out
#UserDir disabled
# line 24 : uncomment
UserDir public_html
# line 32,33
<Directory "/home/*/public_html">
    AllowOverride All     # change if you need
    Options None          # change if you need
    Require method GET POST OPTIONS
</Directory>

[root@www ~]# systemctl restart httpd
```

- SELinux가 활성화되어 있다면 다음과 같이 정책을 변경한다.

```
[root@www ~]# setsebool -P httpd_enable_homedirs on
[root@www ~]# restorecon -R /home
```

- 다음과 같이 페이지를 만들고 사용자별로 웹페이지 접속이 가능한지 테스트한다.

```
[cent@www ~]$ mkdir public_html
[cent@www ~]$ chmod 711 /home/cent
[cent@www ~]$ chmod 755 /home/cent/public_html
[cent@www ~]$ vi ./public_html/index.html
<html>
<body>
<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
UserDir Test Page
</div>
</body>
</html>
```

* * * 
# APM 설치(Apache, PHP, MariaDB)

## PHP 7.4 : Install

```
root@dlp ~]# dnf module list php
CentOS Stream 8 - AppStream
Name      Stream       Profiles                       Summary
php       7.2 [d]      common [d], devel, minimal     PHP scripting language
php       7.3 [e]      common [d], devel, minimal     PHP scripting language
php       7.4          common [d], devel, minimal     PHP scripting language

Hint: [d]efault, [e]nabled, [x]disabled, [i]nstalled

# if other versions are enabled, reset once and switch to the version
[root@dlp ~]# dnf module reset php
[root@dlp ~]# dnf module enable php:7.4
# specify PHP 7.4 and install
[root@dlp ~]# dnf module -y install php:7.4/common

[root@dlp ~]# php -v
PHP 7.4.6 (cli) (built: May 12 2020 08:09:15) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies

# verify to create test script
[root@dlp ~]# echo "<?php echo 'PHP 7.4 Test Page'.\"\n\"; ?>" > php_test.php
[root@dlp ~]# php php_test.php
PHP 7.4 Test Page

````

## Apache httpd : Use PHP Scripts

- PHP 설치가 완료되면 다음과 같이 PHP 설정을 활성화 한다.
```
[root@www ~]# systemctl restart httpd
[root@www ~]# systemctl status php-fpm

# PHP 동작 테스트를 위한 정보 확인 페이지 생성 
[root@www ~]# echo '<?php phpinfo(); ?>' > /var/www/html/info.php
```

* * * 
## MariaDB 설치

[MariaDB 설치와 운용 참고](https://github.com/yonggyo1125/curriculumLinux/tree/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84#mariadb-%EC%84%A4%EC%B9%98%EC%99%80-%EC%9A%B4%EC%98%81)


* * * 
## 그누보드 설치해 보기

- [다운로드](https://sir.kr/g5_pds)

- PHP 문법을 알아보고 간단한 웹페이지 만들어 보기

* * * 
## Node.js 

- Node.js 설치하기
	- [다운로드](https://nodejs.org/ko/)

- 간단한 Node.js 사용법 알아보기
- Node.js + Express를 이용해서 간단한 웹페이지 만들어 보기
