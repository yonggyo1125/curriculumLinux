# DHCP의 개념
- 앞에서 컴퓨터를 잘 아는 사용자 때문에 IP 주소 할당에 문제가 발생하는 경우를 얘기했다. 이를 해결할 수 있는 서버가 DHCP(Dynamic Host Connguration Protocol) 서버다. 그러면 DHCP 서버를 운영할 때의 장점을 파악해보자.

- DHCP 서버가 하는 역할은 자신의 네트워크 안에 있는 클라이언트 컴퓨터가 부팅될 때 자동으로 IP 주소, 서브넷 마스크, 게이트웨이 주소, DNS 서버 주소를 할당해주는 것이다. 그러면 클라이언트 컴퓨터를 사용하는 일반 사용자는 인터넷을 하기 위한 IP 주소와 관련된 정보를 알지 못해도, 인터넷을 사용하는 데 아무런 문제가 없을 것이다. 한마디로 IP 주소가 무슨 말인지 몰라도 인터넷은 자신이 원하는 대로 아무 문제 없이 사용할 수 있다.

- 이와 같이 DHCP 서버의 가장 큰 장점은 관리의 편의성과 이용자의 편의성이라고 할 수 있다. 또, 한정된 IP 주소로 더 많은 IP 주소가 있는 것처럼 활용할 수도 있다. 예를 들어 어느 회사에서 대부분의 직원이 노트북을 사용하고 잦은 출장으로 자리를 비울 때가 많다면, 모든 사용자에게 고정 IP 주소를 주었을 경우 해당 IP 주소를 사용하지 않는 시간이 더 많을 것이다. 이때 DHCP 서버를 운영한다면 필요할 때마다 IP 주소를 할당하게 되므로, 해당 컴퓨터를 사용하지 않을 때 IP 주소를 다른 곳에 활용할 수 있다. 즉 적은 개수의 IP 주소가 있어도 여러 명의 사용자가 필요할 때마다 사용할 수 있다는 의미다. 이는 사설 IP 주소인 경우보다 공인 IP 주소인 경우 훨씬 유용하다.

#### 공인 IP와 사설 IP, 고정 IP와 동적 IP

- 공인 IP와 사설 IP, 고정 IP와 동적 IP의 개념을 명확히 구분하고 넘어가자.

- 공인 IP는 인터넷상에서 공인된 IP 주소다. 즉, 전 세계에 1개밖에 없는 IP 주소다. 예를 들어 실습에서 자주 사용하는 공인된 DNS 서버인 8.8.8.8은 전 세계 어디서든 접근할 수 있는 공인 IP 주소다.
- 사설 IP는 내부 네트워크 안에서만 통용되는 IP 주소다. 예를 들어 VMware 안에 설치된 가상머신들은 모두 사설네트워크 안에 위치한 컴퓨터이므로 사설 IP 주소다(여러분이 지금까지 보아왔던 192.168.xxx.000는 사설 IP 중에서 가장 많이 사용하는 주소 영역이다). 이는 내부 네트워크에서만 통용될 뿐 외부 인터넷에서는 인식하지 못하는 IP 주소다. 그래서 원칙적으로 사설 IP 주소를 사용하는 컴퓨터는 외부 인터넷에 접속할 수 없다. 
- 고정 IP는 컴퓨터 네트워크 정보에 직접 입력해주는 고정된 IP 주소를 말한다. 고정 IP 주소를 알려면 당연히네트워크 관리자에게 문의해야 한다. 고정 IP 주소를 입력한 컴퓨터는 재부팅해도 IP 주소가 변경되지 않는다.동적 IP(또는 유동 IP)는 컴퓨터를 부팅할 때마다 DHCP 서버로부터 얻어오는 IP 주소를 말한다. 그러므로컴퓨터를 부팅할 때마다 IP 주소가 변경될 수 있다.

- 또한 네 개의 용어가 공인 고정 IP, 공인 동적 IP 시설 고정 IP 시설 동적 IP로 섞여서 표현될 수도 있다. 공인고정 IP는 공인된 IP며 고정 IP로 사용되는 것을 말한다. 실습에서 종종 사용하는 주소인 8.8.8.8은 공인고정 IP로 사용하는 것이다. 공인 동적 IP(=공인 유동IP)는 공인 IP이면서, DHCP 서버에게 동적으로 할당받는 IP 주소다. 대표적인 예로 KT, SKT, LG-U+ 등에서 제공하는 초고속 통신망 서비스가 공인 동적 IP의예다. 즉, 초고속통신 서비스를 받는 컴퓨터를 켤 때 할당받는 IP 주소는 켤 때마다 바뀔 수 있지만, 전 세계에서 유일한 공인 IP를 할당받는 것이다.

- 사설 고정 IP는 사설 IP면서도 고정으로 사용되는 IP다. 실습에서 사용되는 Server. Server(B)는 사설 고정IP를 사용한다. 즉 10.0.2.100과 10.0.2.200은 사설 IP지만 고정적으로 할당해놓은 것이다. 사설동적 IP(=사설 유동IP)는 사설 IP를 동적으로 할당받는다는 의미다. 대부분의 DHCP 서버는 이러한 사설 동적 IP를 할당하려고 구성한다(이 책에서 사용하는 Client나 WinClient에 해당된다). 잠시 후 실습에서 구현하는 DHCP 서버도 사설 동적 IP(=사설 유동IP)를 할당하는 데 사용될 것이다.

-  간단히 DHCP 서버의 작동 원리를 파악해보자.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image1.png)

- 위 그림은 DHCP 서버의 작동 순서를 표현한다. 그림에 있는 ①~⑧을 살펴보면 어렵지 않게 DHCP 서버의 작동 방식을 알 수 있을 것이다. 여기서 주목할 점은 PC(DHCP 클라이언트)의 경우 ①번과 ⑧번 컴퓨터의 전원을 켜고 끄기만 하면 나머지는 자동으로 작동한다는 점이다. 즉 사용자는 더 이상 IP 주소와 관련된 정보에 신경쓸 필요가 없으며, 컴퓨터를 켜고 인터넷만 사용하면 된다.

- 여기서 궁금할 만한 사항은 PC는 아직 DHCP 서버의 주소를 모르는데 어떻게 ②번의 IP 주소 요청이 가능하냐는 점이다. DHCP 클라이언트로 설정된 PC는 전원이 켜지면 자신의 네트워크 케이블에 연결된 모든 컴퓨터에 ②번의 IP 주소 요청을 방송 Broadcast한다. 그러면 네트워크에 연결된 컴퓨터 중에서 다른 컴퓨터는 PC의 요청을 무시하고 DHCP 서버만 ④번의 응답을 하게 된다.

- DHCP 서버를 구현했다고 가정한다면, DHCP 클라이언트를 구현할 때는 별도로 설치할 프로그램이 없다. 윈도우에서 DHCP 클라이언트가 되려면, 다음처럼 [Internet Protocol Version4(TCP/IPv4) 속성]에서 [자동으로 IP 주소 받기]와 [자동으로 DNS 서버 주소 받기]를 선택한다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image3.png)

- 리눅스에서 DHCP 클라이언트를 설정하려면 X 윈도가 설치된 환경에서 <b>nm-connection-editor</b>명령을 실행해 [네트워크 설정]을 열고 다음처럼 [IPv4 설정]을 '자동(DHCP)'으로 선택한다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image4.png)

- CentOS를 텍스트 모드에서 DHCP 클라이언트로 설정하려면 /etc/sysconfig/networkscripts/ifcfg-enp0s3 파일의 BOOTPROTO 부분을 BOOTPROTO=dhcp로 수정한다.

> DHCP의 최신 내용을 살펴보거나 소스 파일을 다운로드하려면 https://www.isc.org/software/dhcp 에 접속하자.

* * * 
# DHCP 구현

DHCP 서버를 VMware에서 구현해보자. 우선 이 책에서 구현할 DHCP 서버인 다음 그림을 확인해본다.

다음 그림은 기존에 실습하던 환경과 거의 비슷한 환경이다. 실무 환경에서도 가상 컴퓨터와 가상 허브 Hub 대신 진짜 컴퓨터와 진짜 허브를 사용하는 것 외에는 다음 그림과 같은 환경과 차이가 없을 것이다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image2.png)

- 이번 실습을 진행하기 전에 기존 실습 환경에서 몇 가지를 수정해야 한다. 그림을 잘 보면서 이해해보자.

- VirtualBox 소프트웨어는 자체적으로 게이트웨이, 네임 서버, DHCP 서버의 세 가지 역할을 모두 한다고 이야기했다. 이번 실습에서 게이트웨이와 네임 서버는 VirtualBox가 기존에 제공하던 10.0.2.2를 변경없이 사용할 것이다. 하지만 우리가 구현한 Server (DHCP 서버)가 제대로 작동하는지 확인하려면 VirtualBox가 제공하는 DHCP 서버의 기능은 중지시켜야 한다.

- Client, Server(B), WinClient는 DHCP 클라이언트로 설정할 것이다.VirtualBox 안의 가상머신 네 대는 허브로 연결된 '사설 네트워크' 안에 있는 것과 동일하다. 그러므로 각 클라이언트가 부팅될 때마다 Server는 각 클라이언트에게 네트워크 정보(IP 주소, 게이트웨이 주소, 네임 서버 주소, 서브넷 마스크 등)를 알려줄 것이다.

### 실습1

DHCP 서버를 구현하자. 

#### step 0

<code>호스트 운영체제</code> 세 대의 가상머신을 초기화한다.

- Server, Server(B), Client를 각각 처음 설치 상태로 초기화하자
- 아직은 모두 부팅하지 말자.

#### step 1

<code>Client</code> 우선 Client를 부팅한다.

- 터미널을 열고 <b>nm-connection-editor</b> 명령을 입력한 후 [enp0s3] 더블 클릭한다. 그리고 [IPv4 설정]을 클릭하면 \<자동(DHCP)\>로 설정되어 있을 것이다. 즉 DHCP 서버에서 자동으로 IP 주소를 할당받도록 설정되어 있다. \<취소\>와 \<X\>를 클릭해서 창을 닫자.

- <b>ifconfig enp0s3</b> 명령으로 IP 주소가 자동 할당된 것을 확인하자.

- 설정된 10.0.2.000 (여기에서는 10.0.2.15)는 VirtualBox가 제공하는 DHCP 서버에서 할당받은 IP 주소다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image7.png)

- /etc/resolv.conf 파일도 확인해보자. nameserver (=DNS 서버)의 IP 주소 역시 자동으로 할당받았다. 현 상태에서는 당연히 인터넷이 잘 작동한다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image8.png)

#### step 2

<code>호스트 운영체제</code> 직접 Server를 DHCP 서버로 구축할 것이다. 그러려면 먼저 VirtualBox의 DHCP 서버 기능을 중지하자. 


- VirtualBox 메뉴에서 [파일] -> [환경설정] -> [네트워크] -> 활성화된 NAT 네트워크를 더블클릭한다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image6.png)

- DHCP 설정을 해제하고 [확인] 버튼을 클릭한다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image9.png)

#### step 3

<code>Client</code> 현재는 VMware에서 제공하던 DHCP 서버가 꺼진 상태며, 사설 네트워크 안에 아직 DHCP 서버가 구축되지 않은 상태다.

- DHCP 클라이언트 패키지는 dhcp-client다. <b>rpm -ga dhcp-client</b> 명령으로 설치되어 있는지 확인한다. 기본적으로 이미 설치되어 있을 것이다.
- <b>reboot</b> 명령으로 컴퓨터를 재시작한 후 <b>ifconfig enp0s3</b> 명령으로 IP 주소를 확인해보자. 현재는 DHCP 서버가 없으므로 IP 주소를 할당받지 못했을 것이다.

#### step 4

<code>Server(B)</code> 텍스트 모드에서 DHCP 클라이언트로 지정하자. 

- 부팅하고 root 사용자로 로그인한다.
- ping -c 3 www.google.com 명령을 입력해보자. Server(B)는 설치 시 고정 IP 주소인 10.0.2.200을 할당했으므로 DHCP 서버의 작동과 관계없이 네트워크에 잘 연결되어 있음을 확인할 수 있다.

> ping -c 횟수 IP주소또는URL 명령은 횟수만큼만 ping 요청을 하라는 의미다. 그냥 ping IP주소또는URL 명령을 실행하면 무한대로 시도하며, 취소하려면 [Ctrl] + [C]를 누른다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image10.png)

- vi 에디터로 /etc/sysconfig/network-scripts/ifcfg-enp0s3 파일을 열고 편집한다. 3~4번째 줄쯤의 'BOOTPROTO=none'을 'BOOTPROTO=dhcp'로 변경한 후 저장하고 종료하자. 이는 DHCP 클라이언트 역할을 하도록 설정하는 것이다. 나머지 줄은 무시하고 그냥 둔다.

> 큰 따옴표(")는 생략해도 된다. 리눅스 버전에 따라서 자동으로 붙는 경우도 있다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image11.png)

- 터미널에서 다음 명령을 입력해 설정한 내용을 적용시키고 컴퓨터를 재부팅한다.

```
nmcli connection down enp0s3    -> 네트워크 장치 중지 
nmcli connection up enp0s3        -> 네트워크 장치 시작 
reboot
```

- 다시 root로 로그인하고 <b>ifconfig enp0s3</b> 명령으로 IP 주소를 확인해보자. Server(B) 역시 IP 정보를 얻는 데 실패할 것이다.

#### step 5

<code>Server</code> DHCP 서버를 구축하자.

- 부팅하고 root로 로그인한다.
- <b>dnf -y install dhcp-server</b> 명령으로 DHCP 서버를 설치하자.
-  DHCP 서버의 설정 파일인 /etc/dhcp/dhcpd.conf 를 생성하고 편집해야 한다. gedit으로 /etc/dhcp/dhcpd.conf 를 열자, 필수로 입력해야 하는 기본 정보는 다음과 같다 (#은 주석이므로 해당 줄은 지워도 된다).

```
ddns-update-style interim;
subnet 네트워크주소 netmask 넷마스크값 {
	option routers 게이트웨이주소;
	option subnet-mask 넷마스크정보;
	range dynamic-bootp 시작IP 끝IP;     -> 대략 40대 정도의 PC가 있다고 가정하자.
	option domain-name-servers 네임서버주소;   -> 공인된 구글의 DNS 서버 주소를 사용해보자
	default-lease-time 임대시간(초);
	max-lease-time 최대임대시간(초);
}
```

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image12.png)

>  필요하다면 /usr/share/doc/dhcp-server/dhcpd.conf.example 파일을 복사해서 사용해도 되지만, 복잡하므로 직접 입력하는 편이 낫다.

- 직접 확인했던 자신의 사설 네트워크에 맞는 정보를 입력하자. 입력에 틀린 글자가 없는지 확인한 후 저장하고 닫는다.

- /etc/dhcpd.conf 파일/etc/dhcpd.conf 파일의 중요 내용을 확인해보자. 이 외의 자세한 내용은 <b>'man dhcpd.conf'</b>로 확인하자. 
	- ddns-update-style interim 또는 none   -> 네임서버의 동적 업데이트 옵션이다. 
	- subnet 네트워크주소 netmask 넷마스크값 {}   -> DHCP의 네트워크 주소 지정
		- option routers 게이트웨이IP;    -> 클라이언트에게 알려줄 게이트웨이 IP  주소
		- option subnet-mask 넷마스크정보;  -> 클라이언트에게 알려줄 네트워크의 범위(대개는 C 클래스 255.255.255.0이다)
		- option dynamic-name "도메인이름";    -> 클라이언트에게 알려줄 도메인 이름 정보
		- option domain-name-servers DNS서버IP;   -> 클라이언트에게 알려줄 네임 서버의 주소
		- range dynamic-bootp 시작IP 끝IP;     -> 클라이언트에게 할당한 IP 주소의 범위
		- default-lease-time 임대시간(초);       -> 클라이언트에게 IP 주소를 임대해줄 기본적인 초 단위의 시간
		- max-lease-time 최대임대시간(초);     -> 클라이언트가 하나의 IP 주소를 할당받은 후 보유할 수 있는 최대의 초 단위 시간(이 설정은 특정 컴퓨터가 IP 주소를 고정적으로 보유하는 것을 방지함)
		- host ns {
			hardware Ethernet MAC 주소;
			fixed-address 고정IP주소;
		}
		-> 특정 컴퓨터(랜카드)에게 고정적인 IP 주소를 할당할 때 사용`

-  DHCP 클라이언트가 IP 주소를 대여해 간 정보가 기록되는 파일은 /var/lib/dhcpd/dhcpd.leases 다. 만약 파일이 없다면 touch 명령으로 빈 파일을 생성해야 한다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image13.png)

- <b>systemctl restart/enable/status dhcpd</b> 명령을 차례로 입력해 DHCP 서비스를 시작/확인/상시 가동하자. 만약 서비스 가동을 실패한다면 dhcpd.conf 파일 설정에 이상이 있는 경우가 대부분이므로 다시 확인해본다.

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/13%EC%9D%BC%EC%B0%A8(3h)%20-%20DHCP%20%EC%84%9C%EB%B2%84/images/image14.png)

#### step 6

<code>Client</code> 새로운 IP 정보를 할당받자.

- <b>su -c 'systemctl restart NetworkManager'</b> 명령으로 네트워크를 다시 시작하고, 할당받은 IP 정보를 확인한다. 10.0.2.55~99번 사이의 IP 주소를 할당받았다면 정상이다.
- 웹 브라우저를 실행해 인터넷도 잘 되는지 확인한다.

#### step 7

- <code>Server(B)</code> 텍스트 모드에서 IP 정보를 할당받자.
- <b>systemctl restart NetworkManager</b> 명령으로 네트워크를 다시 시작하고, 할당 받은 IP 정보를 확인한다. 역시 10.0.2.55~99번 사이의 IP 주소를 할당받았다면 정상이다.
- ping -c 3 www.google.com 명령으로 인터넷이 잘 되는지 확인한다.

#### step 8

- <code>Server</code> gedit으로 /var/lib/dhcpd/dhcpd.leases 파일을 열면 다음과 같이 DHCP 클라이언트가 네트워크 정보를 대여해 간 기록이 남아 있을 것이다.


지금까지 DHCP 서버 구현과 DHCP 클라이언트 사용 방법을 확인해보았다. DHCP 서버는 주로 인터넷(internet) 환경이 아닌 회사 내부의 인트라넷 환경에서 작동되는 서버라는 점을 기억하자. 잘 활용하면 네트워크 관리자의 IP 주소 관리 업무가 상당히 줄어들 것이다.




