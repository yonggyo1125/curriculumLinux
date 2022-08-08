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

#### step 2

- Client를 실행한 후 Server의 SSH 서버에 접속해보자.
- Client를 처음 설치 상태로 초기화하자 
- 부팅하고 터미널을 하나 연다(자동으로 centos 사용자로 접속되도록 설정했다).
- <b>ssh 사용자이름@호스트이름</b> 또는 <b>ssh 사용자이름@IP주소</b> 명령으로 접속하면 된다. 텔넷 서버에서 만들었던 teluser 사용자로 접속해보자. 접속한 후에는 텔넷과 동일하게 사용하면 된다. 단지, 암호화를 해서 텔넷과 비교했을 때 더 안전하다는 차이점이 있을 뿐이다. <b>ifconfig enp0s3</b> 혹은 <b>ifconfig</b> 명령을 입력하면 현재 Server의 IP인 10.0.2.100이 나올 것이다. 즉 Server에 접속되어 사용 중이다.

> 처음 접속할 때 'ECDSA Key'와 관련된 메시지가 나오면 yes를 입력한다.

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image15.png)

#### step 3

- <code>Server</code> 지금 Client에서 바로 접속할 수 있었던 이유는 Server에서 SSH 서버 사용을 이미 허용했기 때문이다. <b>firewall-config</b> 명령을 입력해서 확인하면 [ssh] 항목에 체크되어 있을 것이다. 확인 후 [방화벽 설정]을 닫자.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image16.png)

> SSH의 포트 번호는 22번이다. 자주 사용되므로 기억해두자.

##### step4

- <code>호스트 컴퓨터 또는 WinClient</code> 이번에는 Windows에서 접속해보자.
- telnet 클라이언트 프로그램은 Windows에서 기본적으로 제공하지만, SSH 클라이언트 프로그램은Windows에서 제공하지 않는다. 그러므로 인터넷에서 다운로드하여 설치한다. 대표적으로 '한글 PuTTY'라는 프로그램을 추천한다. https://github.com/iPuTTY/iPuTTY/releases 또는 책의 Q&A 사이트(http://cafe.naver.com/thisisLinux)에서 iPuTTY-0.70.2-x86-ko.zip 파일을 다운로드한 후 압축을 풀자.
- 압축이 풀린 폴더의 putty.exe를 더블 클릭해 실행하자.
- PuTTY 설정에서 [Host Name (for IP address)]에 Server의 IP 주소인 '10.0.2.100'을 입력하고 \<열기\> 버튼을 클릭한다. [Port]는 22번, [접속 형식] SSH가 이미 선택되어 있을 것이다(서버 호스트키 관련 메시지가 나오면 \<예\>를 클릭한다).

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image17.png)

- 기존에 만들어둔 teluser 사용자로 접속한다. 이제는 리눅스에서 접속하는 Windows에서 접속하든 완전히 동일하게 사용할 수 있다.

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image18.png)

- su - 명령을 입력해 root 사용자로 접속한 후 Is 명령을 입력하면 한글도 잘 보일 것이다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image19.png)

> 한글 PuTTY는 SSH 클라이언트뿐 아니라 텔넷 클라이언트로도 사용할 수 있다. PuTTY 설정의 [접속 형식] [Telnet]을 선택하면 된다

- exit 명령을 2회 입력하면 종료된다.

* * * 

#  XRDP 서버

- 실제로 텔넷 서버 및 SSH 서버를 설치하고 나면 모든 작업을 다 할 수 있지만, X 윈도 환경은 지원하지 않으므로 X 윈도 전용 명령을 사용할 수 없다. 꼭 텍스트 모드에서 사용 가능한 명령만 써야 한다. 오래 전부터 리눅스를 사용해 온 관리자라면 불편하지 않겠지만, 최근 추세에 따라 X 윈도 환경에서 사용되는 유틸리티나 명령어가 많으므로 이제는 X 윈도 환경 자체를 원격지에서도 사용할 수있어야 한다.

- 이번에는 그래픽 모드로 원격 관리를 지원하는 XRDP 서버를 알아보자. XRDP 서버는 지금 얘기한 것처럼 원격지에서 X 윈도 환경 자체를 사용할 수 있게 하는 서버 프로그램이다. 특히 XRDP는 Windows의 '원격 데스크톱 연결' 프로그램을 사용해서 리눅스에 그래픽 환경으로 접속한다. 그래픽을 네트워크로 전송해야 하므로 텍스트만 전송하는 텔넷과 비교했을 때 속도가 느려진다는 단점이 있다. 다음 그림을 보면 텔넷과 거의 동일하지만 서버에서 X 윈도를 사용하는 것과 완전히 동일한 효과를 낼 수 있다.

> 리눅스에 X 윈도 환경으로 접속하는 데에는 XRDP 외에 VNCSERVER 등의 방식도 사용할 수 있다. 특히 VNCSERVER의 경우 클라이언트가 리눅스든 Windows든 상관없이 서버에 접속할 수 있다. 

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image20.png)

- 다음과 같은 과정으로 실습을 진행해보자. CentOS는 xrdp라는 패키지를 제공한다.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image21.png)

### 실습3

- X 윈도 환경으로 원격 접속을 지원하는 XRDP를 사용해보자.

#### step1

- <code>Server</code> XRDP 서버를 설치하고 가동하자.
- 먼저 <b>dnf -y install epel-release</b> 명령으로 EPEL 저장소에서 추가 설치를 허용하자.

> EPEL(Extra Packages for Enterprise Linux) 저장소란, CentOS 8 및 RHEL 8에서 제공하는 패키지 외에 추가패키지를 제공하는 저장소며 Fedora Community에서 관리한다. CentOS 8에서는 xrdp를 기본으로 제공하지 않지만, EPEL을 통해 설치하면 잘 작동한다.

- <b>dnf -y install xrdp</b> 명령을 입력해 CentOS에서 제공하는 xrdp 패키지를 설치한다.

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image22.png)

- <b>systemctl start xrdp</b> 명령으로 서비스를 시작하고 <b>systemctl enable xrdp</b> 명령으로 상시 가동하도록 설정하자.

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image23.png)

#### step 2

- <code>Server</code> 방화벽에서 xrdp의 포트 번호인 3389번을 허용하자.
- <b>firewall-config</b> 명령으로 방화벽 설정 창을 연다.
- 설정을 [영구적]으로 변경한 후 [포트] 탭을 클릭한다. \<추가\>를 클릭해서 3389 (tcp) 포트를 추가한다.

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/1%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%9B%90%EA%B2%A9%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B4%80%EB%A6%AC/images/image24.png)

-  메뉴의 [옵션] → [Firewall 다시 불러오기]를 선택해서 추가한 포트를 적용시킨다. [방화벽 설정]을 닫는다.

#### step 3

- <code>호스트 컴퓨터 또는 WinClient</code> 원격 데스크톱을 실행해서 연결하자.
- [시작] → [Windows 보조 프로그램]에 있는 [원격 데스크톱 연결]을 실행하고, 컴퓨터에 Server의 IP인 10.0.2.100을 입력한 후 \<연결\>을 클릭한다.

- 보안 인증서와 관련된 경고창이 나오면 \<예\>를 클릭해서 진행한다.
- 접속된 로그인 창에서 Session은 Xvnc를, Username은 centos를, password는 centos를 입력하고 \<OK\>를 클릭한다.

- 잠시 기다리면 Server X 윈도 환경으로 접속된다. centos 사용자로 처음 접속했다면 언어 설정 등의 과정이 필요한데, 기본값으로 진행하면 된다.

- 이제부터는 텍스트 및 그래픽의 모든 환경으로 Server에 접속해서 사용할 수 있다.

- 지금까지 구축한 세 가지 서버를 비교하면 다음과 같다.

||텔넷 서버|SSH 서버|XRDP 서버|
|----|-----|-----|-----|
|속도|빠르다|빠르다|약간 느리다.|
|그래픽 지원|X|X|O|
|보안|취약하다.|강하다.|보통이다.|
|사용 가능 명령|텍스트 모드의 명령만 사용할 수 있다.|텍스트 모드의 명령만 사용할 수 있다.|제한 없다.|
|클라이언트 프로그램|대개의 운영체제가 기본적으로 있다.|리눅스는 기본적으로 있다. Windows는 별도 설치해야 한다.|Windows에 포함되어 있다.|

- 각각 장단점이 있지만 아무래도 빠른 속도와 보안 강화 측면에서 SSH를 기본적으로 사용할 수 있게설정하고, XRDP 서버는 설정만 해둔 채 가동하지 않으면 된다.

- 원격지에서 SSH 서버로 접속해 관리하다가 X 윈도 환경 접속이 필요한 경우 SSH 서버 접속 창에서 XRDP 서버를 구동시키고 Windows의 원격 데스크톱으로 접속하면 된다. 실제로 리눅스 서버관리를 오래 하다 보면 X 윈도 환경이 있어야 하는 경우가 그렇게 많지는 않다. 텔넷 서버의 경우에는 보안이 완전한 회사 안 네트워크에서만 사용하는 것이 무난할 것이다.






