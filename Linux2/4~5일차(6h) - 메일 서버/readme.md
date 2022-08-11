# 메일 서버의 개념
이메일 송수신에 사용되는 프로토콜은 세 가지다.  다음 그림에서 각프로토콜이 사용되는 용도를 살펴보자.

- <b>SMTP(Simple Mail Transfer Protocol)</b> : 클라이언트가 메일을 보내거나, 메일 서버끼리 메일을 주고받을 때 사용한다.
- <b>POP3(Post Office Protocol)</b> : 메일 서버에 도착한 메일을 클라이언트로 가져올 때 사용한다.
- <b>IMAP(Internet Mail Access Protocol)</b> : POP3와 용도가 같다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image1.png)

- 위 그림은 단순하지만 이메일 전송 원리가 잘 표현된 그림이다.
- 우선 kim이라는 이름의 사람은 daum.net이라는 메일 서버에 계정이 있다. 즉 kim@daum.net이라는 계정이 있다. 또 lee라는 사람은 naver.com이라는 메일 서버에 계정이 있다. 즉 lee@naver.com이라는 계정이 있다.

- 이제 kim이 lee에게 메일을 보내고 받는 과정을 살펴보자.

	- (1) kim이 PC 1에서 메일 클라이언트 프로그램 (에볼루션, Outlook 등)을 실행하여 daum.net에 접속한다. '편지쓰기'를 클릭해서 [받는이]란에 'lee@naver.com'이라고 쓰고 내용을 채운 후 \<보내기\> 버튼을 클릭해서 메일을 보낸다(이때는 SMTP 프로토콜을 이용한다).
	- (2) 메일 서버 1 (daum.net)은 kim이 보낸 메일을 잠시 임시 장소에 보관한다. 시간 여유가 있을 때 메일 서버 1은 kim이 보낼 메일의 수신자 주소인 naver.com 메일 서버 IP 주소를 네임 서버에게 요청해서 알아온다.
	- (3) 메일 서버 1은 인터넷을 통해 메일을 메일 서버 2 (naver.com)로 전송한다(이때도 SMTP 프로토콜을 이용한다).
	- (4) 메일 서버 2 (naver.com)는 메일 서버 1(daum.net)로부터 받은 메일의 수신자 이름을 확인한다. 즉 lee라는 수신자 이름이 자신이 관리하는 계정 중에 있는지 확인한다. lee라는 이름이 자신의 계정 중에 있으면 lee의 메일 박스에 kim에게서 받은 메일을 넣어둔다.
	- (5) lee는 PC 2에서 메일 클라이언트 프로그램을 실행해 자신의 메일 서버인 naver.com에 접속한 후, 자신의 메일 박스에 도착된 편지들을 PC 2로 보낸다(이때는 POP3/IMAP 프로토콜을 사용한다). 이제 kim으로부터 온 메일을 읽으면 된다.

- 지금까지의 과정이 인터넷상에서 메일을 주고 받는 작동 원리를 단순화한 것이다.
- 다음 그은 메일이 전송되는 과정을 우리가 구현할 센드메일 Sendmail 서버 입장에서 내부적으로 좀 더 상세히 표현한 것이다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image2.png)

- (1) 메일 클라이언트 1은 SMTP 프로토콜을 이용해서 메일 서버 1의 센드메일 서비스(=데몬)에게 메일을 보내달라고 요청한다.

- (2) 센드메일 서비스는 메일을 '메일 큐'에 넣어둔다(이 파일은 /var/spool/mqueue 다).
- (3) 센드메일 서비스는 시간이 되면 MDA에게 메일을 보내달라고 요청한다.

- (4), (5) MDA는 SMTP 프로토콜을 이용해서 메일 서버 2의 센드메일 서비스에게 메일을 전송한다.
- (6), (7) 메일 서버 2의 센드메일 서비스는 받은 메일을 MDA를 통해 사용자의 메일 박스에 넣어놓는다.
- (8) 메일 클라이언트 2는 메일 서버 2의 dovecot 서비스에게 자신의 메일을 달라고 요청한다. 
- (9) dovecot 서비스는 메일 박스에서 메일 클라이언트 2의 메일을 POP3 또는 IMAP 프로토콜을 이용해 전송한다.

- 이와 같은 작동들이 센드메일 서버를 이용해 메일을 보내는 과정에서 발생한다.

* * *

# 센드메일 서버 구현

- 이번에는 메일 서버 프로그램 중 CentOS에서 기본적으로 제공하는 센드메일Sendmail 서버를 구축해보자.
- 이번에는 메일 서버를 직접 구현해본다. 메일 서버 1대를 구현하는 것으로는 별로 실습 효과가 크지 않을 것이므로, 이번 실습에서는 메일 서버 2대를 설치한다. 실습을 진행하기 전에 꼭 네임 서버 개념을 완전히 파악하고 있어야 한다. 네임서버 구현 없이는 메일 서버를 구현할 수 없기 때문이다.
- 메일 서버 구현을 제대로 실습하려면, 인터넷상에서 2개의 다른 도메인으로 메일 서버를 운영해야 메일이 잘 전송되는지 확인할 수 있다. 그래서 다른 서버와 비교했을 때 네트워크 환경이 좀 복잡한 편이다. 하지만 우리는 VirtualBox 프로그램의 장점을 적극 활용해 인터넷상에 2개의 도메인이 있는 것과 동일한 효과를 내보겠다.

- 이번 실습은 VirtualBox 내부를 사설 네트워크라고 생각하지 말고 그냥 외부 인터넷의 일부라고 생각한다. 그러면 인터넷상에서 2개의 메일 서버를 구축하고 운영하는 것과 완전히 동일한 환경이 된다.

- 다음을 보면 이번 실습을 제대로 구현하는 데 메일 서버 2대, 메일 클라이언트 PC 2대, 네임서버 1대 등 총 5대의 컴퓨터가 필요하다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image3.png)

> 도메인 이름으로 'daum.net'과 'naver.com'을 사용해도 되는 이유는, 지금 사설 네트워크 안을 인터넷이라고 가정하기 때문이다. 즉, 우리가 사용하는 4대의 컴퓨터(가상머신)끼리는 이러한 이름을 사용해도 된다. 당연히 외부컴퓨터에서는 VirtualBox 내부로 접속할 수 없기 때문에 우리가 구축한 메일 서버를 사용할 수 없다.

- 먼저 위 그림과 함께 다음 설명을 잘 이해해야 이번 실습을 진행할 수 있다.
	- VirtualBox 내부의 사설 네트워크를 내부 네트워크라고 생각하지 않고 그냥 외부 인터넷이라고간주한다.
	- 메일 서버 2대를 구현한다. Server는 naver.com 메일 서버로 구현하고, Server(B)는 daum.net 메일 서버로 구현한다.
	- Client는 naver.com 메일 서버의 lee라는 계정을 가진 사용자 PC다. 즉 lee@naver.com이라는 계정이 사용할 PC다.
	- WinClient는 daum.net 메일 서버의 kim이라는 계정을 가진 사용자 PC다. 즉 kim@daum.net이라는 계정이 사용할 PC다.
	- 먼저 네임 서버를 구현한다. 위 그림에는 별도의 컴퓨터로 나타나 있지만, Server가 네임서버의 역할도 하도록 설정한다. 즉 Server는 naver.com 메일 서버 겸 네임 서버의 역할을하는 것이다. 이 네임 서버는 naver.com과 daum.net 두 개의 도메인을 관리하는 역할을 할것이다.
	- 모든 컴퓨터는 'DNS 이름 서버 (=네임 서버)’를 10.0.2.100으로 사용할 것이다.

### 실습1 

- naver.com과 daum.net의 도메인을 관리하는 네임 서버를 구현한다. 메일 서버를 구현하려면 먼저 해야하는 작업이다.

#### step 0
- <code>Server</code>Server를 처음 설치 상태로 초기화하자.
- 부팅한다. root 사용자로 접속하고 터미널을 하나 연다
- <b>dnf -y install sendmail</b> 명령으로 센드메일을 설치한다.

#### step 1

<b>Server-메일 서버</b> 호스트 이름을 mail.naver.com으로 설정하자.

> 이번 실습에서는 Server가 2가지 역할을 하므로 역할을 분명하게 구분하겠다. Server가 '네임 서버' 역할일 때는 <b>Server-네임 서버</b>, '메일 서버' 역할일 때는 <b>Server-메일 서버</b> 라고 표기한다. 나머지 Server(B), Client, WinClient는 한 가지 역할만 하므로 기존대로 표기한다.

- vi 에디터나 gedit으로 /etc/hostname 파일의 'localhost.localdomain'을 'mail.naver.com'으로변경한다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image4.png)

- /etc/hosts 파일의 제일 아래에 '10.0.2.100   mail.naver.com'을 추가한다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image5.png)

- /etc/mail/local-host-names 파일의 제일 아래에 'mail.naver.com'을 추가한다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image6.png)

- /etc/sysconfig/network 파일의 맨 아래에 'HOSTNAME=mail.naver.com' 을 추가한다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image7.png)

- 설정된 내용이 적용되도록 <b>reboot</b> 명령을 입력해 재부팅하고 root 사용자로 로그인한다.

#### step 2

Server(B)의 호스트 이름을 'mail.daum.net'으로 설정하자.

- Server(B)를 처음 상태로 초기화하자.
- root 사용자로 접속한 후, 먼저 <b>dnf -y install sendmail</b> 명령으로 샌드메일을 설치한다.
- vi 에디터로 /etc/hostname 파일의 'localhost.localdomain'을 'mail.daum.net'으로 변경한다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image8.png)

- /etc/hosts 파일의 제일 아래에 '10.0.2.200   mail.daum.net'을 추가한다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image9.png)

- /etc/mail/local-host-names 파일의 제일 아래에 'mail.daum.net'을 추가한다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image10.png)

- /etc/sysconfig/network 파일의 제일 아래에 'HOSTNAME=mail.daum.net'을 추가한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image11.png)

- 설정된 내용이 적용되도록 <b>reboot</b> 명령을 입력해 재부팅하고 root 사용자로 로그인한다.
- <b>hostname</b> 명령을 입력하면 호스트 이름이 변경된 것을 확인할 수 있다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image12.png)

#### step 3

- <b>Server-네임 서버</b> naver.com과 daum.net 도메인 네임 서버를 설정한다.
- 먼저 <b>dnf -y install bind bind-chroot</b> 명령을 입력해 네임 서버 패키지를 설치하자.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image13.png)

- vi 에디터나 gedit으로 /etc/named.conf 파일을 열어서 다음 내용을 수정하거나 추가한다.

```
11행쯤 수정          listen-on port 53 { 127.0.0.1; };  -> listen-on port 53 { any; };
12행쯤 수정          listen-on-v6 port 53 { ::1; };    -> listen-on-v6 port 53 { none; }; 
19행쯤 수정          allow-query   { localhost; };    -> allow-query  { any; };
34행쯤 수정          dnssec-validation yes;          -> dnssec-validation no;
제일 아래에 추가    zone "naver.com" IN { 
                                  type master;
								  file "naver.com.db";
								  allow-update { none; };
                          };
						  zone "daum.net" IN {
						          type master;
								  file "daum.net.db"
								  allow-update { none; };
						  };
```

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image14.png)

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image15.png)

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image16.png)

-  /var/named/ 디렉터리로 이동한 후 naver.com,db 파일과 daum.net.db라는 빈 파일을 만든다. 해당 파일이 만들어졌는지 확인한다.

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image17.png)

- vi 에디터나 gedit을 실행해 /var/named/naver.com.db 파일을 다음처럼 추가 및 수정하고 저장한 후 종료한다.

```
$TTL    3H
@       SOA    @      root.   ( 2  1D  1H  1W  1H )
          IN       NS    @
	      IN       A      10.0.2.100                  -> Server의 IP 주소
		  IN       MX    10   mail.naver.com.     -> 메일을 처리하는 컴퓨터를 지정

mail    IN        A      10.0.2.100                  -> Server의 IP 주소 
```

> IP 주소 부분 끝에 '.'을 입력해서는 안 되며, URL 형식 부분 끝에는 '.'을 찍어줘야 한다.

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image18.png)

- 역시 vi 에디터나 gedit을 실행해 /var/named/daum.net.db 파일을 다음처럼 추가/수정하고 저장

```
$TTL    3H
@       SOA    @      root.   ( 2  1D  1H  1W  1H )
          IN       NS    @
	      IN       A      10.0.2.200                  -> Server(B)의 IP 주소
		  IN       MX    10   mail.daum.net.     -> 메일을 처리하는 컴퓨터를 지정

mail    IN        A      10.0.2.100                  -> Server(B)의 IP 주소 
```

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image19.png)

- 설정한 파일에 이상이 없는지 체크한다.
```
# named-checkconf
# named-checkzone naver.com naver.com.db
# named-checkzone daum.net daum.net.db
```

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image20.png)

-  <b>systemctl restart/enable/status named</b> 명령을 차례대로 입력해 네임 서비스를 재시작하고 상시 가동하도록 설정한 후 상태를 확인하자.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image21.png)

- 이제 DNS 포트를 방화벽에서 열어야 한다. 앞으로 다른 포트도 여러 개 열어야 하므로, 실습이 편하도록 <b>systemctl stop/disable firewalld</b> 명령을 차례로 입력해 방화벽 실행을 멈춘 후 잠시 방화벽을 꺼두자.

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image22.png)

- <b>nslookup</b> 명령을 입력한 후 <b>server 10.0.2.100, mail.naver.com, mail.daum.net</b>을 차례로 입력해 네임 서버가 잘 설정되었는지 확인해본다.

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image23.png)

- 이렇게 해서 naver.com과 daum.net 도메인을 관리하기 위한 네임 서버의 설정이 완료되었다. <b>exit</b>로 nslookup을 종료한다.

#### step 4

- <b>Server-메일 서버</b> mail.naver.com 메일 서버의 DNS 서버를 우리가 구축한 네임 서버 (10.0.2.100)로 설정한다.
- vi나 gedit으로 /etc/sysconfig/network-scripts/ifcfg-enp0s3 파일을 열고 DNS1 부분을 10.0.2.100으로 수정한 다음 저장하고 종료한다

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image24.png)

- 다시 vi나 gedit으로 /etc/resolv.conf 파일을 열고 nameserver 부분을 '10.0.2.100'으로 수정한 다음 저장하고 종료한다.

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image25.png)

> Server는 메일 서버와 네임 서버의 역할을 동시에 한다. 그래서 10.0.2.100 은 메일서버의 IP 주소이자 네임 서버의 IP 주소다.

- <b>reboot</b> 명령으로 Server를 재부하고 root로 로그인한다.

#### step 5
- <b>Client</b> 'Server-메일 서버'와 동일하게 네임 서버를 10.0.2.100으로 설정하자.
- Client를 처음 설치 상태로 초기화하고 부팅한다.
- <b>su-c 'gedit /etc/resolv.conf'</b> 명령을 입력해 nameserver 부분을 10.0.2.100으로 설정하고 저장한다.

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image26.png)

- <b>nslookup</b> 명령을 입력하고 mail.naver.com과 mail.daum.net을 차례로 입력해 각각의 IP 주소가 10.0.2.100과 10.0.2.200 인지 확인한다.

#### step 6

- <b>Server (B)</b> 네임 서버를 10.0.2.100으로 설정해보자.
에디터로 /etc/sysconfig/network-scripts/ifcfg-enp0s3 파일을 열고 DNS1 부분을 10.0.2.100으로 수정하자.
- vi 에디터로 /etc/resolv.conf 파일을 열고 nameserver 부분을 10.0.2.100으로 수정하자.
- 수정 후 nslookup 명령을 입력하여 mail.naver.com(10.0.2.100)과 mail.daum.net(10.0.2.200)의 IP 주소가 정확히 나오는지 다시 한 번 확인한다.
- <b>reboot</b> 명령으로 Server(B)를 재부팅하고 root로 로그인한다.

#### step 7

- <b>WinClient</b> 네임 서버를 10.0.2.100으로 변경한다.

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image27.png)

- 명령 프롬프트에서 <b>nslookup</b> 명령을 입력하고 mail.naver.com(10.0.2.100)과 mail.daum.net(10.0.2.200)의 IP 주소가 정확히 나오는지 확인한다.

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image28.png)

### 실습2
naver.com 메일 서버와 daum.net 메일 서버를 구현하자.

#### step 0

\<실습 1\>에 이어서 진행한다.

#### step 1

<b>Server-메일 서버</b> naver.com 메일 서버를 구축한다.

- 메일 서버를 구현하는 필수 패키지는 sendmail, sendmail-cf, dovecot 3가지다. sendmail은 앞의 실습에서 설치했으므로 <b>dnf -y install sendmail-cf dovecot</b> 명령을 입력해 패키지를 설치한다.

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image29.png)

- 패키지가 잘 설치되었는지 <b>rpm -qa | grep sendmail</b> 및 <b>rpm -qa dovecot</b> 명령으로 확인하자.

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image30.png)

- vi 에디터로 /etc/mail/sendmail.cf 파일을 열고 다음과 같이 수정한다 (vi 에디터에서 행 번호는 "set

```
85행쯤 수정      Cwlocalhost     -> Cwnaver.com(붙여서 쓸 것)
267행쯤 수정    0 DaemonPortOptions=Port=smtp, Addr=127.0.0.1, Name=MTA
                       -> 0 DaemonPOrtOptions=Port=smtp, Name=MTA
					     ('Addr=127.0.0.1,' 부분 삭제)
```

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image31.png)

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image32.png)

#### sendmail.cf 파일

- /etc/mail/sendmail.cf 파일은 Sendmail 서버의 설정 파일이다. 설정 내용이 길고 복잡해서 까다롭게 여겨지지만, 꼭 필요한 부분만 알면 된다.
	- <b>Cw도메인이름</b>: 도메인 이름을 가진 메일 서버로 사용하겠다는 의미다.
	- <b>MaxMessageSize=용량</b>: 메일 1개의 본문과 첨부파일을 합친 제한 용량(바이트 단위)이다.
	- <b>Mlocal 설정내용</b>: 전체 메일 공간을 '설정내용'으로 제한한다.
	- <b>O QueueDirectory=/var/spool/mqueue</b>: 메일 전송 시 사용하는 임시 저장 디렉터리
	- <b>O DaemonPortOptions=Port=smtp, Addr=127.0.0.1, Name=MTA</b>: 'Addr=127.0.0.1'은 자기자신만 메일을 보낼 수 있다는 의미다. 그래서 외부에서도 메일을 보낼 수 있도록 이 부분을 삭제했다.
	
	
- sendmail.cf 파일을 수정한 후에는 Sendmail 메일 서비스를 재시작해야 한다. 하지만 지금은 다른 설정까지 모두 마친 후에 서비스를 다시 시작할 것이므로, 아직은 서비스를 재시작하지 않아도 된다.

- 외부 네트워크 또는 호스트가 메일을 보낼 수 있도록 허가해준다. gedit이나 vi로 /etc/mail/access 파일에 다음 내용을 추가한다.

```
naver.com  RELAY    -> naver.com 도메인의 릴레이 허용
daum.net   RELAY    -> daum.net 도메인의 릴레이 허용
10.0.2        RELAY    -> 10.0.2.xxx 컴퓨터의 릴레이 허용
```

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image33.png)

- /etc/mail/access 파일을 수정한 후에는 <b>makemap hash /etc/mail/access \< /etc/mail/access</b>명령을 입력해서 적용해야 한다.

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image34.png)

> <b>메일 릴레이</b><br>메일 릴레이(Mail Relay)란 다른 네트워크 또는 호스트에서 자신의 메일 서버를 경유하여 메일을 전송하는것이다. 이 기능을 악용해서 스팸 메일이나 바이러스 메일 등 대량 메일을 발송하는 경우가 종종 발생되어 사회적인 문제까지 야기시키곤 한다.<br><br>그래서 Sendmail에서 제공하는 메일 릴레이 기능은 기본적으로 자기 자신의 IP 주소(127.0.0.1)외에는 아무도 메일을 발송할 수 없도록 설정된 것이다. 이 파일이 /etc/mail/access 파일이다.<br><br>하지만 모든 사용자가 메일 서버 컴퓨터 앞에 앉아서 메일을 보낼 수는 없으므로 신뢰할 수 있는 도메인이나호스트 또는 네트워크에는 메일을 릴레이할 수 있도록 허용한다. 보통 /etc/mail/access 파일의 릴레이 허용은 RELAY로 거부는 REJECT 또는 DISCARD를 사용한다.<br><br>예를 들면 다음과 같다.

```
10.0.2.200     RELAY        -> 10.0.2.200 컴퓨터 릴레이 허용
abc.com       RELAY        -> abc.com 도메인에 릴레이 허용 
192.168        RELAY        -> 192.168.xxx.xxx의 모든 컴퓨터에 릴레이 허용
babo@         DISCARD    -> babo라는 계정의 메일 거부(거부 메시지 안 보냄)
@daum.net   REJECT       -> daum.net 메일 사용자의 메일 거부(거부 메시지 보냄)
```

- /etc/mail/access 파일을 수정하면 꼭 센드메일 서비스를 재시작해야 한다. 지금은 모든 설정을 마친 후에 서비스를 시작할 것이므로 서비스를 재시작하지 않아도 된다.

- 사용자에게 메일 박스의 내용을 보내주는 dovecot 서비스의 설정 파일은 /etc/dovecot/dovecot.conf 다. vi 에디터로 연 다음 다음 부분을 수정한다.

```
24행쯤 주석(#) 제거: protocols = imap pop3 lmtp
30행쯤 주석(#) 제거: listen = *, ::
33행쯤 주석(#) 제거: base_dir = /var/run/dovecot/
```

![image35](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image35.png)

> dovecot.conf 설정 파일도 내용이 좀 복잡하다.<br><br>앞에서 수정한 내용 중 24행의 protocols는 세 가지 프로토콜을 모두 사용한다는 의미다. 30행의 '\*'는 IPv4를, ':'은 IPv6 프로토콜을 의미한다. dovecot.conf 파일의 주석에 상세히 잘 나와 있으니 참조하자.<br>더 자세한 사항은 http://wwww.dovecot.org 를 방문하거나 man dovecot.conf 명령을 입력해 확인해보자.

- /etc/dovecot/conf.d/10-ssl.conf 를 vi 에디터로 열고 아랫부분을 수정한다.

```
8행쯤 수정:     SSL = required  -> ssl = yes
```

![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image36.png)

- /etc/dovecot/conf.d/10-mail.conf 를 vi 에디터로 열고 아랫부분을 수정한다.

```
25행쯤 주석(#) 제거                  mail_location = mbox:~/mail:INBOX=/var/mail/%u
121행쯤 주석(#) 제거 후 변경      mail_access_groups = mail
166행쯤 주석(#) 제거                 lock_method = fcntl
```

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image37.png)

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image38.png)

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image39.png)

- naver.com의 메일 계정 사용자인 lee를 생성하자(암호도 기억하기 쉽게 lee로 지정하자). lee의 메일 계정은 lee@naver.com이 될 것이다.

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image40.png)

- 다음 명령을 입력해 sendmail 및 dovecot 서비스를 시작하고 상시 가동하자.

```
systemctl restart sendmail
systemctl enable sendmail
systemctl restart dovecot
systemctl enable dovecot
```

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image41.png)

- 지금까지 진행한 것은 naver.com 메일 서버를 완성한 것이다. daum.net 메일 서버를 만들기 전에 naver.com 메일 서버가 자체적으로 잘 작동하는지 확인해보자.

#### step 2

<b>Client</b> naver.com 메일 서버가 잘 작동하는지 테스트하자. Client는 lee@naver.com 계정 사용자의 PC다.

- 왼쪽 위의 [현재 활동] [에볼루션]을 선택해서 에볼루션을 시작한다. 초기의 [환영합니다]에서 \<다음\>을 클릭한다.

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image42.png)

- [백업에서 복구]에서는 그냥 \<다음\>을 클릭한다.
- [신상 정보]에서는 [전체 이름]에 적당히 '이네이버'라고 입력하고 [전자메일 주소]에는 lee@naver.com'을 입력한 후 \<다음\>을 클릭한다.

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image43.png)

- 잠시 후 [메일 받기]가 나오면 서버 종류를 [POP]으로 변경하고 [서버]에는 'mail.naver.com'을 입력한다. [사용자이름]은 'lee'를 입력하고 [암호화 방식]은 [TLS, 특정 포트 사용]으로 변경한 후 \<다음\>을 클릭한다.

![image44](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image44.png)

- [받기 옵션]에서는 그냥 \<다음\>을 클릭한다.

- [메일보내기]에서는 [서버]에 'mail.naver.com'을 입력하고 \<다음\>을 클릭한다.

![image45](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image45.png)


- [계정 요약]에서는 [이름]에 '네이버 메일' 등 계정을 식별할 수 있는 이름을 입력하고 \<다음\>을 클릭한다.

![image46](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image46.png)

- [완료]에서는 \<적용\>을 클릭해서 설정을 마친다.

-  [메일-에볼루션] 창이 나온다. 우선 \<보내기/받기\>를 클릭한 후 [인증서 신뢰...]에서 \<계속 허용\>을 클릭해 Server의 인증서를 허용하자.

![image47](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image47.png)

- 만약 [메인 인증 요청] 창이 나오면 사용자 이름과 암호에 'lee'를 입력하고, 아래에 있는 [이 암호를 키모음에 추가]의 체크를 끈 후 \<확인\>을 클릭하자.

![image48](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image48.png)

- 에볼루션의 메인 화면이 실행되면 왼쪽 위의 \<새로 만들기\>를 클릭해서 자신(lee@naver.com)에게적당히 메일을 써보자.

![image49](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image49.png)

- \<보내기/받기\>를 클릭하고 [받은 편지함]을 확인하면 조금 전에 자신이 보낸 메일을 확인할 수 있다. naver.com 메일 서버가 정상적으로 작동하는 상태다.

![image50](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image50.png)


#### step 3

- <code>Server (B)</code> 이번에는 daum.net 메일 서버를 구축한다. 앞의 naver.com 메일 서버 구축과 거의 동일하다.
- <b>dnf -y install sendmail-cf dovecot</b> 명령으로 패키지를 설치한다.

- vi 에디터로 /etc/mail/sendmail.cf 파일을 열고 다음 내용과 같이 수정한다 (vi 에디터에서 행 번호는 'set number'를 입력하면 확인할 수 있다).

```
85행쯤 수정:     Cwlocalhost    -> Cwdaum.net(붙여서 쓸 것)
267행쯤 수정:   0 DaemonPortOptions=Port=smtp, Addr=127.0.0.1, Name=MTA
                        -> 0 DaemonPortOptions=Port=smtp,Name-MTA('ADDR=127.0.0.1,' 부분 삭제)
```

- 외부 네트워크 또는 호스트가 메일을 보낼 수 있도록 허가한다. /etc/mail/access 파일을 vi 에디터내용을 추가한다.

```
naver.com     RELAY     -> naver.com 도메인의 릴레이를 허용한다.
daum.net      RELAY     -> daum.net 도메인의 릴레이를 허용한다.
10.0.2           RELAY     -> 10.0.2.xxx 컴퓨터의 릴레이를 허용한다.
```

![image51](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/4~5%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A9%94%EC%9D%BC%20%EC%84%9C%EB%B2%84/images/image51.png)

- /etc/mail/access 파일을 수정한 후에는 <b>makemap hash /etc/mail/access \< /etc/mail/access</b> 명령을 입력해 적용시킨다.

- /etc/dovecot/conf.d/10-mail.conf 파일을 vi 에디터로 열고 다음 부분을 수정한다.

```
24행쯤 주석(#) 제거:     protocols = imap pop3 lmtp
30행쯤 주석(#) 제거:     listen = *, ::
33행쯤 주석(#) 제거:     base_dir = /var/run/dovecot/
```
- /etc/dovecot/conf.d/10-ssl.conf 파일을 vi 에디터로 열고 다음 부분을 수정한다.

```
8행쯤 수정:   ssl = required -> ssl = yes
```

- /etc/dovecot/conf.d/10-mail.conf 파일을 vi 에디터로 열고 다음 부분을 수정한다.

```
25행쯤 주석(#) 제거:              mail_location = mbox:~/mail:INBOX=/var/mail/%u
121행쯤 주석(#) 제거 후 변경:  mail_access_groups = mail
166행쯤 주석(#) 제거:             lock_method = fcntl 
```

- daum.net 메일 계정 사용자인 kim을 <b>useradd kim</b> 명령으로 생성하자 (<b>passwd kim</b> 명령을 입력해 비밀번호도 kim으로 지정하자). kim의 메일 계정은 kim@daum.net이 될 것이다.

- 다음 명령을 입력해 sendmail 및dovecot 서비스를 시작하고 상시 가동하자.

```
systemctl restart sendmail
systemctl enable sendmail
systemctl restart dovecot
systemctl enable dovecot
```

- 메일 서비스와 관련된 여러 개의 서비스를 실행해야 하므로 <b>systemctl stop firewalld</b> 명령과 <b>systemctl disable firewalld</b> 명령을 입력해 잠시 방화벽을 꺼두자.
