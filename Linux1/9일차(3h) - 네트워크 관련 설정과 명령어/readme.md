# 네트워크 관련 설정과 명령어

## 네트워크 관련 필수 개념

- 네트워크와 관련된 내용은 상당히 방대하다. 모든 것을 이야기하기에는 적절하지 않으므로, 더 깊은 네트워크 지식은 다른 책이나 인터넷을 통해 학습하자. 여기에서는 후반부의 네트워크서버 구축을 위한 최소한의 네트워크 관련 개념과 명령어 위주로 살펴본다. 그래도 처음 네트워크를 접한다면 좀 어렵게 느껴질 수 있으므로, 모두 외우지는 않더라도 계속 실습에서 나오는 개념만큼은 확실히 파악하자.

### TCP/IP
- 컴퓨터끼리 네트워크상으로 의사소통하는 약속을 '프로토콜'이라고 부르는데, 그중 가장 널리 사용되는 프로토콜의 종류 중 하나다.

-  통신의 전송/수신을 다루는 TCP(Transmission Control Protocol)와 데이터 통신을 다루는 IP(Internet Protocol)로 구성된다.

### 호스트 이름과 도메인 이름

- 호스트 이름(host name)은 각각의 컴퓨터에 지정된 이름을 말한다.
- 도메인 이름(또는 도메인 주소) domain name은 hanbit.co.kr과 같은 형식으로 표기하며 kr은 한국, co는 회사, hanbit은 단체/회사 이름을 의미한다.
- 예) 호스트 이름이 this이고 도메인 이름이 hanbit.co.kr이라면 전체 이름은 this.hanbit.co.kr로 붙여서 부른다. 이를 FQDN(Fully Qualified Domain Name)이라고 한다. 즉 같은 회사(도메인)에서 this.hanbit.co.kr이라는 호스트(=컴퓨터)는 중복되지 않는다.

### IP 주소

- 각 컴퓨터의 랜 카드(Lan Card) (네트워크 카드(NIC. Nerwork Interface Card))에 부여되며 중복되지 않는 유일한 주소다.
- 즉 네트워크에 연결된 모든 컴퓨터는 고유한 IP 주소가 있으며, 이는 서로 다르기 때문에 특정 컴퓨터의 IP 주소를 알면 그 컴퓨터가 전 세계 어디에 있든지 접속할 수 있다는 개념이다(사설 IP 주소는 예외). 
- 4바이트로 이루어져 있으며 각 자리는 0\~255까지의 숫자가 올 수 있다. 예를 들어 Server의 IP 주소는 10.0.2.100이고, 모든 컴퓨터에서 자기 자신을 의미하는 IP 주소는 127.0.0.1이다.

### 네트워크 주소

- 같은 네트워크에 속해 있는 공통 주소다.

- 예를 들어 Server의 IP 주소는 10.0.2,100, Server(B)는 10.0.2.200, Client는 10․0․2.131(수강생 마다 다를 수 있음), 호스트 컴퓨터는 10.0.2.1이다. 이 네 대의 컴퓨터는 같은 네트워크에 있으며 서브넷 마스크는 C클래스(255.255.255.0)를 사용하므로 공통된 네트워크 주소는 앞 3자리인 10.0.2.0이 된다.

### 사설 네트워크

10.02.xxx.000의 주소 영역은 사설 네트워크(Private network)의 주소다. 사설 네트워크는 외부와 분리된 내부의 별도 네트워크를 의미하며, 주로 공인된 IP 주소가 부족할 때 많이 사용한다. 우리가 VirtualBox 설치한 컴퓨터들도 사설 네트워크의 IP 주소인 10.0.2,000를 할당한 것이다. 사설 네트워크 구축은 뒤에서 실습해본다.

### 브로드캐스트 주소

- 내부 네트워크의 모든 컴퓨터가 수신하는 주소를 말한다.
- 현재 주소의 제일 끝자리를 255로 바꾼 주소다(C클래스의 경우).
- 예를 들어 실습환경의 broadcast 주소는 10.0.2.255다.

> 브로드캐스트 주소를 좀 더 쉽게 비유하자면, 아파트의 스피커 또는 마을의 확성기 정도로 생각할 수 있다. 예를 들어 아파트 경비실에서 "차량 번호 7777 차를 다른 곳으로 이동시켜주세요"라고 말한다면 아파트 집집마다 스피커를 통해 전달된다. 하지만 모두가 다 응답하는 것은 아니다. 자신과 관련된 것이라면 반응을 보이겠지만, 자신과 관련이 없다면 그냥 무시하고 지나칠 것이다. 브로드캐스트 주소도 이런 아파트의 스피커처럼 모든 컴퓨터가 들을 수 있는 주소라고 생각하면 쉽게 이해할 수 있다.

### 게이트웨이(Gateway)

- 내부 네트워크를 외부로 연결하기 위한 컴퓨터 또는 장비다.
- Server, Server(B), Client 등 내부 네트워크에 있는 컴퓨터끼리 통신할 경우 외부로 나갈 필요가 없으므로 게이트웨이가 없어도 되지만, 인터넷을 사용하기 위해 외부에 접속하려면 반드시 게이트웨이의 IP 주소를 알아야 한다. 게이트웨이는 쉽게 말해 '외부 네트워크로 나가기 위한 통로'쯤으로 생각하면 된다. 그러므로 게이트웨이에는 내부로 향하는 문(네트워크 카드)과 외부로 향하는 문(네트워크 카드)이 있어야 한다. 즉, 두 개의 네트워크 카드가 장착되어 있어야 한다.
- 우리의 경우 게이트웨이 주소는 10.0.2.2로 고정되어 있다. 
- 게이트웨이를 별도로 추가하는 명령어 형식은 다음과 같다.

```
# route add default gw 게이트웨이 주소 dev 장치이름
```

- 예를 들어, 게이트웨이가 10.0.2.254로 변경되었을 때는 다음과 같이 사용한다.

```
# route add default gw 10.0.2.254 dev enp0s3
```

### 넷마스크와 클래스

- 넷마스크(Netmask): 네트워크의 규모를 결정한다.
- 강의에서는 사설 네트워크에서 C 클래스(class)를 사용하므로 넷마스크를 255.255.255.0으로 한다. 
- 설정한 환경에서는 10.0.2.0~10,0.2.255까지 256개의 IP 주소를 사용할 수 있지만, 그중에서 네트워크 주소인 10.0.2.0, 브로드캐스트 주소인 10.0.2.255, 게이트웨이로 사용할 IP 주소(10.0.2.2)를 제외하면 총 253대의 컴퓨터를 네트워크 내부에서 연결할 수 있다.


### 네트워크 클래스

- 만약 우리의 사설 네트워크에 253대가 넘는 컴퓨터를 설치하고자 한다면 넷마스크를 255.255.0.0으로 변경해 B 클래스로 사용하면 된다. 그러면 총 65536(2^16)개의 IP 주소를 사용할 수 있으며, 네트워크 주소는 10.0.0.0이 된다. 또 A 클래스로 변경하려면 255.0.0.0을 사용하면 된다.

### DNS 서버 주소

- 인터넷 사용 시 www.daum.net과 같은 URL을 해당 컴퓨터의 IP 주소로 변환해주는 서버 컴퓨터를 말한다.

- DNS(Domain Name System) 서버 (=네임 서버)의 주소를 사용하지 않거나 잘못 입력되어 있으면 웹 사이트에 정상적으로 접속되지 않으므로 올바른 정보를 설정해야 한다.

- 설정 파일은 "/etc/resolv.conf" 며, 내용 중에 'nameserver DNS서버IP' 형식으로 설정되어 있다.

### 리눅스에서의 네트워크 장치 이름

- 랜카드(NIC)가 리눅스에 장착되었을 때 CentOS 8을 설치하면 자동으로 이 장치의 이름을 enp0s3으로 인식한다.

- 이 랜카드의 이름은 앞으로 네트워크 정보를 파악하거나 네트워크를 정지 또는 가동할 때 자주 사용한다. 예를 들어 다음과 같은 명령을 종종 사용하게 될 것이다.

```
ifconfig enp0s3    -> 네트워크 설정 정보 출력
ifup enp0s3        -> 네트워크 장치 가동
ifdown enp0s3    -> 네트워크 장치 정지
```

- 만약 ifup, ifdown 명령어가 없다면 다음과 같이 설치한다.

```
dnf -y install NetworkManager-initscripts-up-down
```

## 중요한 네트워크 관련 명령어

- 네트워크와 관련된 명령어는 많지만, 이 책에서 주로 사용할 명령어는 몇 개 되지 않는다. 실습에서도 살펴보겠지만 이 정도는 꼭 외우도록 하자.

### nmtui

Network Manager Text User Interface의 약자로, 네트워크와 관련된 작업 대부분은 이 명령을 기반으로 실행할 수 있다

- 자동 IP 주소 또는 고정 IP 주소 사용 결정
- IP 주소, 서브넷 마스크, 게이트웨이 정보 입력
- DNS 정보 입력
- 네트워크 카드 드라이버 설정
- 네트워크 장치 (enp0s3) 설정

#### nmtui 명령과 ifcfg-enp0s3 파일

- nmtui 명령은 그놈(GNOME) 그래픽 모드를 제공하지 않는다. X 윈도의 그래픽 모드를 완전하게 사용해서 네트워크를 설정하려면 <b>gnome-control-center network</b> 명령 또는 <b>nm-connection-editor</b> 명령을 사용한다. 
- 하지만 이 명령어들은 Server(B)와 같은 텍스트 모드에서 사용할 수 없으므로 독자는 되도록 nmtui를 사용거나 직접 ifcfg-enp0s3 파일을 편집해서 네트워크를 설정하는 것을 권장한다.


### systemctl start/stop/restart/status NetworkManager

- 네트워크 설정을 변경한 후 변경된 내용을 시스템에 적용시키는 명령어다. 
- 그러므로 <b>nmtui</b> 명령을 실행한 후 또는 직접 <b>ifcfg-enp0s3</b> 파일을 편집한 후에는 꼭 <b>systemctl restart NetworkManager</b> 명령을실행 해야 한다고 기억하면 된다. 
- restart 옵션은 stop 옵션과 start 옵션이 합쳐진 것이다. status 옵션은 현재의 작동(active) 또는 정지(inactive) 상태를 표시한다.

### ifup 장치이름

- 해당 장치를 작동시키는 명령어다. 만약 네트워크 장치가 장착되었으나 작동하지 않는다면 이 명령어로네트워크 장치를 작동시킬 수 있다. 장치 이름에는 주로 enp0s3 이 사용된다.

### ifdown 장치이름

- ifup과 반대로 네트워크 장치를 끄는 명령어다.

### ifconfig 장치이름

- 해당 장치의 IP 주소와 관련 정보를 출력하는 명령어다.


### nslookup

- DNS 서버의 작동을 테스트하는 명령어다.


### ping IP 주소 또는 URL

- 해당 컴퓨터가 네트워크상에서 응답하는지 테스트하는 간편한 명령어다. 
- 즉, 상대 컴퓨터가 아무런 이상 없이 작동되는지를 네트워크상에서 체크할 때 주로 사용된다.


## 네트워크 설정과 관련된 주요 파일

- nmtui 명령을 실행하고 나서 변경되는 관련 파일들이다. 중요한 파일들이므로 꼭 알아두자.

### /etc/sysconfig/network

- 네트워크의 기본 정보가 설정되어 있는 파일이며 네트워크 사용 여부가 써 있다.


### /etc/sysconfig/network-scripts/ifcfg-enp0s3

- enp0s3 장치에 설정된 네트워크 정보가 모두 들어 있는 파일이다.

### /etc/resolv.conf

- DNS 서버의 정보와 호스트 이름이 들어 있는 파일이다.

### /etc/hosts

- 현재 컴퓨터의 호스트 이름과 FQDN이 들어 있는 파일이다.

> nmtui 명령을 사용하지 않아도 위 4개의 파일을 직접 편집하면 동일한 효과를 낼 수 있다.

## 실습1

nmtui 명령어 및 이와 관련된 설정 파일을 확인해보자.

#### step0

- Server를 처음 설치 상태로 초기화하자
- root 사용자로 접속한다. 
- 바탕 화면 왼쪽 위의 [현재 활동] →[터미널]을 선택해서 터미널을 연다.

#### step1

- <b>nmtui</b> 명령을 입력해서 IP 정보 등을 확인해보자.
- 다음을 참고하여 설정했던 네트워크 정보를 확인해보자 (이제부터는 키보드의 [Tab] 또는 화살표키, [Enter]를 사용해야 한다)

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image1.png)

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image2.png)

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image3.png)


- 장치의 이름은 enp0s3 IP 주소는 10.0.2.100/24, 게이트웨이 주소는 10,0.2.2로 설정되어 있다. IP 주소 뒤에 24가 붙은 것은 서브넷 마스크가 255.255.255.0으로 설정된 것과 동일한 의미다.

- 몇 가지를 수정하자. 주소를 10.0.2.55/24로 변경해보자. 그리고 모두 살펴봤으면 Tab을 여러 번 눌러 제일 아래 \<OK\>로 이동한 후 [Enter]를 누른다([Shift] + [Tab])을 누르면 반대 방향으로 이동한다.


![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image4.png)

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image5.png)

#### step2

관련 파일을 확인해보자.

- <b>cat /etc/sysconfig/network</b> 명령을 입력해 network 파일의 내용을 확인하자. 아무것도 안 써져 있거나 'NETWORKING=YES'라고 된 것은 네트워크를 사용하겠다는 의미다 (#은 주석이다).

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image6.png)

- 이번에는 <b>cat /etc/sysconfig/network-scripts/ifcfg-enp0s3</b> 명령을 입력해 ifcfg-enp0s3 파일을 확인한다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image7.png)

> UUID(Universal Unique IDentifier)는 개체에 부여하는 128bit로 구성된 고유한 번호며, 네트워크상에서 유일한 장치(또는 개체)로 구분하기 위한 식별자로 사용된다. 앞으로 다른 부분에서도 나올 수 있는데 특별히 신경 쓰지 않아도 된다.

- <b>nmtui</b> 명령을 실행해서 확인했던 정보의 대부분이 이 파일에 들어 있다. IP 주소는 IPADDR(또는 IPADDR0) 부분에 기본 게이트웨이는 GATEWAY (또는 GATEWAY0) 부분에, DNS 서버는 DNS1 (또는 DNS2) 부분에 들어 있는 것을 확인할 수 있다. 만약 NETMASK 부분이 생략되었다면 기본적으로 255.255.255.0이라는 것을 의미한다.

- 앞서 실습에서는 이 파일을 직접 편집했었다. 즉 <b>nmtui</b> 명령을 사용하지 않고 지금 열어본 "/etc/sysconfig/network-scripts/ifcfg-enp0s3" 파일을 직접 편집해도 똑같은 결과를 얻을 수 있다.
- 만약 파일을 수정했거나 <b>nmtui</b>로 내용을 수정했다면 <b>systemctl restart NetworkManager</b> 명령을 입력해야 변경한 내용이 적용된다. <b>systemctl restart NetworkManager</b> 명령을 실행하자.

#### ifconfig 명령과 route 명령

- 네트워크 정보를 설정하기 위해 <b>nmtui</b> 명령어나 에디터에서 직접 설정하는 방법 외에 ifconfig나 route 명령어로 설정할 수도 있다. root 사용자 권한으로 다음 명령을 차례로 실행하면 된다.

```
ifconfig enp0s3 10.0.2.100 netmask 255.255.255.0 broadcast 10.0.2.255 up
route add -net 10.0.2.0 netmask 255.255.255.0 enp0s3
route add default gw 10.0.2.2 dev enp0s3
```

- DNS 서버가 설정된 파일은 "/etc/resolv.conf"다. <b>vi /etc/resolv.conf</b> 명령을 입력해 resolv.conf 파일에 DNS 서버를 추가로 입력해보자. 
- 마지막 행에 'nameserver 168.126.63.1'을 추가하면 된다 (vi 에디터 사용이 아직 어렵다면 gedit을 사용한다). 
- 이렇게 하면 처음에 나온 DNS 서버 (=네임 서버)인 8.8.8.8이 작동하지 않더라도 두 번째 DNS 서버인 168.126.63.1 을 사용하게 된다. 
- 저장하고 에디터를 종료하자.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image8.png)

> 168.126.63.1과 168.126.63.2는 KT(한국 통신)에서 제공하는 DNS 서버(네임 서버)다. 전 세계 어디서든 이 주소를 사용해도 된다. 앞으로도 자주 사용되는 주소이므로 168.126.63.1 정도는 외우자. 이 외에도 SK 브로드밴드의219.250.36.130과 210.220.163.82, LG 유플러스의 164.126.101.2와 203.248.252.2를 사용해도 된다.

- 주의할 점은 systemctl restart NetworkManager 명령 후 다시 ifcfg-enp0s3 파일에 설정된 내용으로 변경된다는 것이다. 그러므로 영구적으로 DNS 설정을 변경하고 싶다면 <b>nmtui</b> 명령으로 DNS를 변경하거나 직접 ifcfg-enp0s3 파일을 편집해야 한다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image9.png)

#### step3

- 이번에는 인터넷이 안 될 경우 DNS 서버 고장 때문인지 아니면 다른 문제 때문인지 확인해본다. DNS 서버를 직접 구축한 후 잘 작동하는지 테스트할 때도 사용하는 방법이다.


- 바탕 화면 왼쪽 위에 있는 [현재 활동] →[Firefox 웹 브라우저]를 선택한 후 www.nate.com에 접속해보자. 별 문제가 없다면 정상적으로 접속될 것이다.

- 이번에는 DNS 서버에 문제를 발생시키자. vi 에디터나 gedit으로 /etc/resolv.conf 파일을 열어서 8.8.8.8을 100.100.100,100으로 고친 후 저장하고 닫는다 (DNS 서버가 고장난 것이든 /etc/resolv.conf 파일의 IP 주소를 잘못 입력한 것이든 어차피 DNS 서버가 응답하지 않는 것은 마찬가지다).

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image10.png)

- 웹 브라우저를 닫고 다시 실행한 후 www.nate.com에 다시 들어가보자. 한참을 기다려도 접속이 안될 것이다. 그런데 이렇게 인터넷이 안 될 경우 DNS 서버 문제 때문인지, IP 설정이 잘못됐기 때문인지 바로 알기가 어렵다. 여기서는 DNS 서버가 원인을 발생시킨 것인지 파악해본다

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image11.png)

#### step4

우선 /etc/resolv.conf 파일에 설정된 DNS 서버 주소(100,100.100.100) 외에 다른 DNS 서버의 주소를알아야 한다. 가장 일반적으로 사용되는 DNS 서버 주소인 KT의 168.126.63.1 또는 Google의 8.8.8.8을사용하자.

- 터미널에서 <b>nslookup</b> 명령을 입력하면 프롬프트가 \>로 바뀐다. <b>server</b> 명령을 입력해서 나오는 결과가 현재 Server에 설정된 DNS 서버 주소다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image12.png)

- 예상했겠지만 기본으로 설정된 DNS 서버 주소는 /etc/resolv.conf 파일에 설정된 잘못된 주소인100.100.100.100이 된다.

- www.nate.com을 입력하자. 잠시 후 다음과 같은 오류 메시지가 나온다. 현재 설정된 DNS서버 주소(100,100.100.100)가 응답하지 않기 때문이다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image13.png)

-  server 새로운DNS서버IP주소 명령을 입력해 DNS 서버 주소를 변경하고 다시 www.nate.com을 입력해보자. 새로운 DNS 서버 주소는 확실히 작동하는 KT의 168.126.63.1을 사용한다.

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image14.png)

- 이와 같이 <b>nslookup</b> 명령을 사용해 DNS 서버 주소를 변경한 후 네트워크가 잘 응답한다면 /etc/resolv.conf 파일에 설정된 DNS 서버에 문제가 있는 것이며, 그 외 네트워크 설정에는 문제가 없는 것이다. <b>exit</b> 명령을 입력해서 nslookup을 종료한다.

> www.nate.com의 경우 IP 주소 1개에만 연결되어 있으나, 웹 사이트에 따라서는 여러 개의 IP 주소에 URL이 연결되어 있을 수도 있다. 이는 라운드 로빈 방식과 관련이 있는데 뒤에서 살펴본다.
 
- 이제 방금 정상 작동을 확인한 KT의 168.126.63.1(또는 Goggle의 8.8.8.8)을 vi 에디터나 gedit으로 /etc/resolv.conf 파일에 입력한 후 저장한다.

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image15.png)

- 웹 브라우저를 닫고 다시 실행해서 웹 접속이 정상적으로 되는지 확인한다.


#### DNS 서버 역할

- DNS 서버의 역할은 URL 이름을 IP 주소로 변경하는 것이다. 예를 들어 웹 브라우저에서 https://www.nate.com 을 입력하면 바로 네이트 홈페이지로 접속되는 것이 아니라 /etc/resolv.conf 파일에 설정된 DNS 서버에게 www.nate.com URL의 IP 주소를 물어본다. DNS 서버가 해당 URL에 해당하는 IP 주소를 알려주면 그때서야 비로소 알아낸 IP 주소의 컴퓨터로 접속하는 것이다(아마도 이 IP 주소가 네이트 웹 서버 IP 주소일 것이다).

- 이러한 과정을 거치는 이유는 네트워크상에 있는 컴퓨터를 구분할 때 www.nate.com과 같은 URL이 아닌 IP 주소가 중복되지 않는 유일한 식별자이기 때문이다.

- 개념이 조금 어려울 수도 있겠으나 더 상세한 내용은 [네임 서버](https://github.com/yonggyo1125/curriculumLinux/tree/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84) 에서 설명한다. 
- 결론적으로 DNS 서버가 고장난 경우 www.nate.com같은 URL을 사용해서는 웹 서버에 접속할 수 없다는 사실을 기억하자.

#### /etc/resolv.conf 파일

- IP 주소 게이트웨이 주소 등의 정보를 변경한 후에는 <b>systemctl restart NetworkManager</b> 명령을 실행해야 시스템에 적용되지만 /etc/resolv.conf 의 nameserver 부분을 수정한 후에는 <b>systemctl restart NetworkManager</b> 명령을 실행할 필요가 없다. <b>그 이유는 웹 브라우저 또는 nslookup 명령을 사용해 URL을 조회할 경우 실시간으로 /etc/resolv.conf 파일을 열어서 확인하기 때문이다.</b>

## 네트워크 보안을 위한 SELinux

- SELinuxSecunty Enhanced Linux는 보안에 취약한 리눅스를 보호하기 위해 탄생했다. 시스템에서 보안에 영향을 미치는 서비스, 권한 등을 제어할 수 있다.

- SELinux 환경에서는 해커가 어떤 경로로 시스템 침입에 성공하든, 침입한 경로의 애플리케이션 사용 이상의 권한을 얻지 못한다. 예를 들어 FTP 서버의 경로로 침입할 경우 FTP와 관련된 디렉터리나 파일 외에는 다른 서버에 접근할 수 없으므로 해킹에 대한 피해를 FTP 서버만으로 제한할 수 있다. 즉 만약의 사태가 발생해도 피해를 최소화할 수 있다.

- SELinux의 사용 여부는 강제(enforcing), 허용(permissive), 비활성(disabled) 이라는 3가지 레벨 중 선택할 수 있으며, 설정 파일은 /etc/sysconfig/selinux 파일이다. CentOS 8을 설치하면 강제 (enforcing) 기본 설정되어 있다.


- 우리는 앞서 설정에서 Server, Server(B)의 SELinux 기능을 비활성disabled으로 변경했다. 이는 SELinux 사용 시 추후 네트워크 서비스가 원활하지 않을 수 있기 때문에, 먼저 CentOS 리눅스를 잘 배우고 나서 보안을 고려하려고 설정한 것이다. 여기서도 알 수 있듯이 보안을 강화하면 여러 가지 불편한 점이 발생할 수 있고, 반대로 보안을 약화하면 편리해지지만 위험이 따를 수 있다. /etc/sysconfig/selinux 를 직접 편집하지 않고 <b>system-config-selinux</b> 명령을 실행하여 설정할 수도 있다.

> system-config-selinux 명령을 사용하려면 먼저 policycoreutils-gui 패키지를 설치해야 한다.


![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/9%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B4%80%EB%A0%A8%20%EC%84%A4%EC%A0%95%EA%B3%BC%20%EB%AA%85%EB%A0%B9%EC%96%B4/images/image16.png)

- 먼저 가장 강력한 강제(enforcing)를 살펴보자. 강제는 시스템 보안에 영향을 미치는 기능이 감지되면아예 그 기능이 작동되지 않도록 시스템에서 막는다. 
- 허용(permissive)은 시스템 보안에 영향을 미치는 기능이 감지되면 허용은 하되 사용 내용이 로그에 남고 화면상에도 출력된다. 
- 비활성화(disabled)는SELinux를 사용하지 않는 것이어서 당연히 보안에 취약해진다.

- 설정을 변경한 후에는 컴퓨터를 재부팅해야 한다. 하지만 추후 실무에서 보안이 강화된 서비스를 제공하려면 잘 알아둘 필요가있으므로 man 페이지나 다른 관련 사이트, 보안 관련 서적 등을 참조하자.

- 비록 실습에서는 SELinux를 비활성(disabled)으로 설정해놓았지만 실무에서는 귀찮더라도 최소 허용(permissive)이나 강제(enforcing)로 설정해서 사용하는 것이 바람직하다.