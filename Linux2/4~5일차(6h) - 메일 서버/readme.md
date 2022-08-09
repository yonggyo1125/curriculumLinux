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

