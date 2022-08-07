# 텔넷 서버

- 지금은 많이 사용하지 않지만 , 텔넷은 오랫동안 전통적으로 사용되어 온 원격 접속 방법이다. 
- 보안 등에 취약하기 때문에 요즘은 텔넷만 사용하지는 않으며 보안 기능을 더해서 사용한다. 

## 텔넷 서버 개요

- 리눅스 서버에 텔넷 서버를 설치했다면, 원격지에서 리눅스 서버에 접속할 PC에는 텔넷 클라이언트 프로그램이 필요하다. 
- 대부분의 운영체제에는 기본적으로 텔넷 클라이언트 프로그램이 내장되어 있으므로 별 문제가 없다.

- 다음과 같이 과 같이 원격지의 PC (텔넷 클라이언트)에서 리눅스 서버에 접속하면 서버 앞에 앉아서 직접 텍스트 모드로 작업하는 것과 완전히 동일한 효과를 낼 수 있다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image1.png)

### 서버/클라이언트 개념

- 서버(Server)/클라이언트(Client)는 아주 흔한 용어지만, 처음 서버를 구축하는 사람들은 개념이 완전하지않을 수 있으므로 짚고 넘어가자. 
- 예를 들어 많은 사람이 네이버(www.naver.com)를 사용하는데 이것 역시서버/클라이언트의 개념이다. 네이버라는 웹 서버(리눅스 웹 서버라 가정해보자)가 작동하고 있고, 사람들은웹브라우저(주로 인터넷 익스플로러, 크롬, 사파리, 파이어폭스 등)라는 웹 클라이언트 프로그램을 이용해서웹 서버에 접속하는 것이기 때문이다. 
- 즉, 서버 프로그램이 작동할 때 서버를 사용하려면 클라이언트 프로그램이 필요하다.

- 텔넷 서버도 마찬가지다. 텔넷 서버 프로그램이 작동할 때 텔넷 서버에 접속하려면 텔넷 클라이언트 프로그램이 있어야 한다. 다른 서버 프로그램 대부분도 각각의 클라이언트 프로그램이 있어야 서버에 접속해서 사용할수 있는 것과 같다.

- 서버/클라이언트의 특징은 다음과 같다.

	- 서버에 접속하려면 꼭 클라이언트 프로그램이 필요하다.
	- 서버가 리눅스라고 클라이언트 리눅스일 필요는 없다. 즉, 서버의 OS와 클라이언트의 OS가 같아야하는 것은 아니다.
	- 각각의 서버 프로그램은 자신에게 맞는 별도의 클라이언트 프로그램이 필요하다.
	- 웹 서버(아파치 또는 IIS) 웹 클라이언트(인터넷 익스플로러, 크롬, 사파리, 파이어폭스, 모질라 등)
	- 텔넷 서버 \<--\> 텔넷 클라이언트(telnet, 한글 PuTTY 등)
	- FTP서버 \<--\> FTP 클라이언트(알FTP, wsFTP, ftp, gftp 등)
	- VNC 서버 \<--\> VNC 클라이언트(vncviewer, TightVNC 등)
	- SSHD 서버 \<--\> SSH 클라이언트 (ssh, 한글 PuTTY 등)
	- 오라클 서버 \<--\> 오라클 클라이언트(sqlplus)

## 텔넷 서버를 구축해보자

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image2.png)

### 실습1

- 리눅스에 텔넷 서버를 설치하고 가동하자. 그리고 원격지의 Windows에서 접속해 리눅스를 관리하자.

#### step 0

- Server를 처음 설치 상태로 초기화하자
- 부팅한다. root 사용자로 접속하고 터미널을 하나 연다.

#### step 1

- <b>rpm -qa telnet-server</b> 명령을 입력해 텔넷 서버가 설치됐는지 확인하자. 기본적으로 설치되어있지 않으니 <b>dnf -y install telnet-server</b> 명령을 입력해 설치하자.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image3.png)

> rpm 명령의 -qa 옵션은 패키지가 설치되었는지 확인하는 명령이다. 패키지 이름이 정확히 기억나지 않으면 <b>rpm -qa | grep 일부문자</b> 명령을 입력해 설치 여부를 확인하면 된다.

#### step2

- Server 텔넷 서비가 가동되도록 설정하자.
- 다음을 입력해 텔넷 서버 서비스를 시작하자.

```
systemctl start telnet.socket     -> 서비스 시작
systemctl status telnet.socket    -> 서비스 상태 확인
```

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image4.png)

> <b>systemctl 작동옵션 서비스 또는 소켓이름 명령</b>으로 서비스를 실행할 수 있다. 작동 옵션은 시작(start), 중지(stop), 재시작(restart), 상태 확인(status)을 사용할 수 있다. systemctl 명령을 멈추려면 Q를 누른다.

- 서비스 상태는 작동(active) 중이며, 포트는 23번을 사용한다는 것을 확인할 수 있다.

> <b>포트</b><br>포트(Port) TCP 포트 또는 UDP 포트를 줄여서 부르는 것인데, 가상의 논리적인 통신 연결 번호를 말한다. 컴퓨터를 건물이라고 가정하면 IP 주소는 건물의 정문이고, 포트 번호는 건물 안의 각 방의 방 번호라고 생각하면 된다. 예를 들어 회의실은 55번 방, 휴게실은 77번 방, 식당은 33번 방과 같이 번호를 매긴 것을 생각하면 이해하기 쉽다.<br><br>모든 컴퓨터는 0~65535까지 포트 번호가 있다. 그런데 일반적으로 0~1023까지는 예약된 포트 번호가 많다. 지금 구축한 텔넷 서버는 23번, FTP 서버는 21번, 웹 서버는 80번 등으로 예약되어 있다.

- <b>adduser teluser</b> 명령을 입력해 접속 테스트를 위한 사용자를 만들고 <b>passwd teluser</b> 명령을 입력한다.


![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image5.png)

- 자신의 컴퓨터에서 <b>teluser</b>로 접속해보자. 별 문제없이 잘 접속될 것이다.

```
telnet 서버IP주소   -> 텔넷 클라이언트를 사용해서 접속. teluser로 접속한다.
whoami               -> 접속된 사용자 이름 확인
exit                    -> 텔넷 종료
```

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image6.png)

#### step 3

- <b>호스트 컴퓨터 또는 Windows 클라이언트</b> 이번에는 외부에서 텔넷 서버로 접속해보자.
- 텔넷 클라이언트 기능을 추가 설치하자. [시작]에서 마우스 오른쪽 버튼을 클릭한 후 [앱 및 기능]을 선택한다. 제일 아래로 스크롤해서 [프로그램 및 기능]을 클릭하고 왼쪽의 [Windows 기능 켜기/끄기]를 클릭하자.
- [Windows 기능]에서 [텔넷 클라이언트] 또는 [Telnet Client]에 체크하고 \<확인\>을 클릭하면 설치가 진행된다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image7.png)

- Windows [시작] 버튼에서 마우스 오른쪽 버튼을 클릭해 [Windows PowerShell] 또는 [명령 프롬프트] 창을 열고 <b>ping 10.0.2.100</b> 명령을 입력해 Server와 네트워크로 연결되는지 확인한 후, <b>telnet 10.0.2.100</b> 명령을 입력해 텔넷 접속을 시도하자.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image8.png)

- 그런데 네트워크는 응답하지만 한참을 기다려도 텔넷 연결이 되지 않는다. CentOS를 설치했을 때 기본적으로 서버 서비스 대부분을 허용하지 않는 상태로 설치했기 때문이다. 즉 자체 방화벽이 설치되어 있다. 이렇게 설정된 '보안 수준 설정'을 변경해줘야 한다.

#### step 4

- Server 텔넷 서비스의 포트(23번)를 연다.

- firewall-config 명령을 입력해서 [방화벽 설정]이 나오면 [public]이 선택된 상태에서 [설정]을 [영구적]으로 변경하고 [서비스] 탭의 [telnet]을 클릭해서 체크하자. 그리고 선택한 내용을 적용하기 위해 메뉴의 [옵션] → [Firewalld 다시 불러오기]를 선택한 후 [방화벽 설정] 창을 닫는다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image9.png)

- 텍스트 모드에서 방화벽을 설정하려면 <b>firewall-cmd --add-service=서비스이름</b> 또는 <b>firewall-cmd --add-port=포트번호/프로토콜</b> 명령을 실행한다. 이번 실습에서 지금 텔넷 (23번 포트) 서비스를 허용하려면 <b>firewall-cmd --add-service=telnet</b> 혹은 <b>firewall-cmd --add-port=23/tcp</b> 중 하나를 실행한다.

- 만약 재부팅 후에도 방화벽 설정을 유지하려면 --permanent 옵션을 붙인다. 즉  <b>firewall-cmd --permanent --add-service=telnet</b> 명령을 실행해 텔넷 설정을 유지하고 <b>firewall-cmd --reload</b> 명령을 실행해서 다시 텔넷을 로딩한 것과 같은 효과다.

- <b>systemctl enable telnet.socket</b> 명령을 입력해서 재부팅 후에도 계속 텔넷 서버가 가동되도록 설정하자.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image10.png)

#### step 5

- 호스트 컴퓨터 또는 WinClient Server의 텔넷 서버에 다시 접속해보자.
- 다시 명령 프롬프트를 실행해 <b>telnet 10.0.2.100</b> 명령을 입력하고 방금 전에 생성한 <b>teluser</b> 사용자로 접속한다. ifconfig enp0s3 명령을 입력해 IP 주소를 확인하면 Server의 IP 주소를 확인할 수 있을 것이다. 즉 Server로 잘 접속되었다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image11.png)

> whoami 명령은 현재 접속한 사용자(자기 자신)를 확인할 때 사용한다.

- 이제 어느 곳에서든 인터넷만 된다면 리눅스 서버 앞에 직접 앉아서 작업하는 것과 동일한 환경이 구축되었다. 지금은 Windows에서 리눅스 서버로 접속했지만, 클라이언트 OS가 리눅스라도 동일한 telnet 명령을 사용해서 리눅스 서버로 접속할 수 있다.


* * * 
# OpenSSH 서버

- 텔넷은 오래 전부터 사용되어 왔으나 요즘 들어 문제가 발생하고 있다. 서버와 클라이언트 사이에서 데이터 전송 시 암호화하지 않아 해킹 위험에 노출되는 것이다. 
- 실제 텔넷으로 접속한 컴퓨터가 전송하는 데이터의 값을 알아내는 것은 별로 어려운 일이 아니다. 앞의 실습이라면 Windows에서 리눅스로 접속할 때 사용하는 아이디와 비밀번호가 네트워크상에 그대로 전송되는 일을 예로 들 수 있다.

- 이를 해결하려고 사용하는 것이 바로 리눅스에서 지원하는 openssh 서버다. 다음 그림을 보면 텔넷과 거의 동일하지만, 데이터 전송 시 암호화한다는 차이점을 확인할 수 있다.


![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image12.png)

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image13.png)

- 텔넷 서버를 이해했다면 OpenSSH 서버는 아주 간단하다. 텔넷과 같은 방식으로 사용하면 되며, CentOS는 기본적으로 OpenSSH 서버를 설치하고 가동시켜주므로 원격지에서 클라이언트로 접속하면 된다.

### 실습2

- 보안이 강화된 OpenSSH 서버를 사용하자.

#### step1

- Server를 실행한 후 다음 명령을 입력해 패키지가 설치되고 가동되는지 확인하자. SSH 서버의 설치 패키지 이름은 'openssh-server'이고, 서비스(데몬) 이름은 'sshd'다.

```
rpm -qa openssh-server   -> 패키지 설치 여부 확인
systemctl status sshd       -> 서비스 가동 여부 확인(Q를 누르면 종료됨)
```

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image14.png)

