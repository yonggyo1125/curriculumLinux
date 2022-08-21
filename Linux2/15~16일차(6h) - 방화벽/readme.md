# 방화벽 명령어 firewall-cmd
- firewall 데몬이 우선 실행되고 있는지를 판단하기 위해서 systemctl 명령어를 이용해서 확인합니다.

```
systemctl status firewalld
```

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/15~16%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%B0%A9%ED%99%94%EB%B2%BD/images/image1.png)

- 지금과 같이 active(running) 상태라면 현재 데몬이 실행 중인 것입니다. 그럼 먼저 firewall-cmd 명령을 이용해서 상태를 확인해 보겠습니다.

## 방화벽 실행 확인 state

- 방화벽이 실행되고 있음을 확인하는 명령어 입니다.

```
# firewall-cmd --state
```

- 위 명령어를 실행하면 running 혹은 not running으로 나옵니다.

## 방화벽 존(zone) 목록 출력

- 방화벽이 실행되고 있다면 어떤 존들이 있는지 존의 목록들을 가져옵니다. 

```
# firewall-cmd --get-zones
# firewall-cmd --get-active-zones
```

- 첫 번째 명령어는 사용 가능한 존 목록들을 전부 가져옵니다. 
- 두 번째는 현재 active 된 존 목록들을 가져오고 있습니다.

## 방화벽 허용 포트 목록 출력

- 서비스 포트를 추가하거나 제거해야 실제 방화벽으로부터 포트를 타고 서버 내부의 서비스를 이용할 수 있게 됩니다. 포트를 추가/제거하는 방법에는 명령어를 이용하는 방법과 설정파일을 이용하는 방법 2가지가 있습니다.

### 명령어를 이용하는 방법

```
# firewall-cmd --add-service=ftp
# firewall-cmd --remove-service=ftp
# firewall-cmd --add-port=21/tcp
# firewall-cmd --remove-port=21/tcp
```

- 기본적으로 firewall-cmd 명령어와 함께 --add-service 혹은 --remove-service를 이용하면 well-known 포트로 이용되고 있는 서비스들의 포트를 추가하거나 제거할 수 있습니다. 하지만 같은 서비스라 하더라도 포트를 변경해서 사용할 수 있기 때문에 port를 직접 추가하기 위해서는 --add-port 혹은 --remove-port를 사용할 수 있습니다.

- 단, 명령어를 이용해서 방화벽 작업을 진행하고 시스템 재부팅 이후에도 지속적으로 적용하기 위해서는 --permanent 옵션이 필요합니다.

```
# firewall-cmd --permanent --add-service=snmp
```

### 설정파일을 이용하는 방법 

- 설정파일은 아래 경로에 위치하고 있습니다.

```
# vi /etc/firewalld/zones/public.xml
```

- 파일을 vi 편집기를 통해서 오픈하면 내용들을 확인할 수 있습니다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/15~16%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%B0%A9%ED%99%94%EB%B2%BD/images/image2.png)

- 이곳에 보면 service가 기본적으로 추가되어 있는 것을 볼 수 있습니다. 여기에서 서비스 혹은 포트를 추가할 수 있습니다.

```xml
<service name="ftp
 />
 <port port="21" protocol="tcp" />
```


## 설정 후 재시작

- 방화벽 수정을 하고 재시작을 해야 정상적으로 적용할 수 있습니다. 재시작 명령어는 다음과 같습니다.

```
# firewall-cmd --reload
```

- 재시작의 결과로 정상이라면 success 메세지가 나타납니다.