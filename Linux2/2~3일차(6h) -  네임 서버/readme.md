# 네임 서버의 개념

## 네임 서버 개요

- 네임 서버는 DNS(Domain Name System) 서버라고도 한다. 우리가 웹 브라우저나 FTP 클라이언트를 사용할 때 http://www.nate.com 또는 ftp://mirrors.kernel.org/ 등과 같은 URL을 사용하는데, 실제 원하는 서버에 접근하려면 이 URL을 해당 컴퓨터의 IP 주소로 변환시켜야 한다. 바로 이 일을담당하는 것이 네임 서버 또는 DNS 서버라고 하는 컴퓨터다.

- 이렇게 www.nate.com을 IP 주소로 변환하는 과정을 이름 해석(name resolution)이라고 한다.

```
www.nate.com 120.50.132.112
```

- 네트워크에서 컴퓨터를 구분하는 유일한 방법은 IP 주소다. 즉 인터넷에 연결된 모든 컴퓨터에는 중복되지 않는 IP 주소가 있다. 그러므로 자주 접속하는 웹 서버나 FTP 서버의 IP 주소를 모두 안다면, DNS 서버 (네임 서버)를 사용할 필요가 없다. 오히려 www.nate.com을 120.50.132.112와 같은 IP 주소로 알아내는 과정이 생략되므로 인터넷 속도가 더 빨라질 것이다. 그러나 웹 서핑 시 URL 주소를 사용하지 않고 IP 주소를 외워서 사용하는 경우는 특수한 목적 외에거의 없을 것이다.

- 네임 서버의 변천사를 필자 나름대로 가정해보았다. 요목조목 따진다면 일부는 틀린 얘기라고 할 수도 있겠지만, 네임 서버의 전반적인 이해를 돕기 위해 가정한 이야기이므로 그냥 넘어가주기 바란다. 인터넷이 도입되던 시절에는 인터넷에 연결된 컴퓨터가 그리 많지 않았다. 그래서 인터넷을 통해 상대 컴퓨터에 접속하기 위해 아마 메모지 같은 곳에 IP 주소를 적어 놓았을지도 모른다. 어차피 접속할 컴퓨터가 몇 대 되지 않았으므로, 가까운 사람 몇몇의 전화번호는 수첩을 찾지 않고도 외우듯이 IP 주소도 자연스럽게 외워졌을 것이다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image1.png)

- 인터넷에 연결된 컴퓨터가 수십, 수백 대가 되자 수첩에 적어놓는 방식이나 외우는 방식으로는 한계를 느꼈을 것이다. 이에 펜으로 적어두던 수첩을 각자의 컴퓨터에 저장해놓는 방식으로 생각을 전환했다. 이 파일이 'hosts' 파일이다.

- hosts 파일의 예를 보면 다음과 같다.

```
102.54.94.97  rhino.acme.com
38.25.63.10   x.acme.com
127.0.0.1      localhost
::1              localhost
```

- hosts 파일은 Windows에서는 C:\Windows\system32\drivers\etc\hosts로, 리눅스에서는 /etc/hosts 로 존재한다. 지금도 hosts 파일은 종종 사용된다.

- hosts 파일이 존재함에 따라 웹 브라우저에서 URL 주소를 입력했을 때 hosts 파일을 검색하여 해당 URL에 대응하는 IP 주소를 얻을 수 있게 되었다. 예를 들어 웹 브라우저에서 rhino.acme.com을 입력하면 102.54.94.97의 IP를 얻게 되어 해당 컴퓨터로 접속할 수 있다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image2.png)

- 이렇듯 어느 정도 규모에서는 hosts 파일이 해결책일 수 있었다. 하지만 네트워크상의 컴퓨터가 기하급수적으로 늘어나면서 모든 IP 정보를 파일 하나에 기록하는 것은 무리가 되었다. 또한 이전에 1.1.1.1이라는 IP를 가진 컴퓨터 이름이 AAA였는데 IP가 1.1.1.2로 바뀌었다면, 사용자는 직접 자신의 hosts 파일을 열어 새로운 정보로 수정해야 했다. 전화번호와 비교하면, hosts 파일은 각각의 가정에 있는 전화번호부와 같은 역할을 하는 것이다. 꽤 많은 정보를 넣을 수 있지만, 새로 생기는 전화번호나 변경되는 전화번호는 실시간으로 확인할 수 없다. 또한 전 세계의 모든 전화번호를 전화번호부에 넣을 수도 없다.

- 그래서 이름 해석(name resolution)을 전문으로 하는 서버 컴퓨터가 필요해졌고, 이를 네임 서버 또는 DNS서버라고 부르게 되었다. 역시 전화번호와 비교한다면 아마도 전화 안내 서비스인 114와 같은 역할을 한다고 볼 수 있을 것이다. 예를 들어 114 안내 전화는 언제든지 '굽네 치킨'이라는 이름(URL이라고 생각하자)으로 물어보면, '굽네 치킨'의 전화번호(IP 주소)를 나에게 정확히 알려준다.

- 네임 서버는 인터넷에서 변화하는 모든 컴퓨터의 URL과 IP 정보를 거의 실시간으로 제공하므로,사용자는 더 이상 URL에 해당하는 IP 주소를 신경 쓸 필요가 없어졌다. URL만 알면 어디서든 해당컴퓨터에 접속할 수 있게 되었다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image3.png)

- 위 그림 처럼 사용자는 10.10.10.10이라는 네임 서버의 IP 주소만 알면(=114라는 전화번호만알면) 언제든지 해당하는 URL (굽네 치킨)의 IP 주소(전화번호)를 알아낼 수 있다.https://obank.kbstar.com/quics?page=C019088&QSL=F&_ga=2.135219638.684008459.1659855496-2106537425.1649812300

### 실습1

/etc/hosts 파일의 설정과 네임 서버 설정을 확인해보자.

#### step 0

- Server를 처음 설치 상태로 초기화하자.
- 부팅한다. root 사용자로 접속하고 터미널을 하나 연다.

#### step 1

- 현재 PC가 사용하는 네임 서버의 IP 정보를 확인해보자. <b>nslookup</b> 명령을 입력한 다음 'server'를 입력해 현재 Server에 설정된 네임 서버를 확인하자. 이어서 www.nate.com, www.kernel.org 을 차례로 입력해 IP 주소를 확인해보자.

```
nslookup
server     -> 현재 설정된 네임 서버의 IP 주소 확인
www.nate.com   -> 네이트 웹 서버의 IP 주소 확인
www.daum.net   -> daum.net 웹 서버의 IP 주소 확인
dm.n-mk.kr   -> d.n-mk.kr 웹 서버의 IP 주소 확인
exit
```

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image4.png)

> 각 회사마다 웹 서버를 운영하는 몇 가지 방식이 있다. 이번 예에서 네이트는 하나의 IP 주소만 보이지만, 여러 번 실행하면계속 다른 IP 주소를 보여줄 수도 있다. 컴퓨터의 IP 주소는 관리자가 언제든 변경할 수 있으므로 결과가 다를 수 있다.

#### step 2

- 조금 전 확인한 네임 서버인 8.8.8.8 를 확인해보자.
- cat /etc/resolv.conf 명령을 입력해 네임 서버가 설정된 파일을 확인하자.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image5.png)


- 웹 브라우저에서 www.naver.com 이 잘 접속되는지 확인해보자. 아마도 네트워크에 특별한 문제가 없는 이상 잘 접속될 것이다.

#### step 3

네임 서버에 문제가 생기거나 주소를 잘못 입력했을 때 어떻게 작동하는지 확인해보자.

- vi 에디터나 gedit으로 /etc/resolv.conf를 열어서 다음과 같이 nameserver 부분을 주석 처리하고 저장한 후 닫는다(즉 네임 서버가 고장난 것으로 생각하면 된다).

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image6.png)

> 이 파일은 수정해도 상관없지만, 컴퓨터가 재부팅되거나 네트워크가 재시작되면 다시 /etc/sysconfig/networkscripts/ifcfg-enp0s3 파일에 설정된 내용으로 초기화된다.

- 웹 브라우저를 닫았다가 다시 실행해서dm.n-mk.com에 접속해보자. 다음과 같은 메시지와 함께 접속되지 않을 것이다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image7.png)

이번에는 주소창에 dm.n-mk.com 이 아닌, IP 주소(121.170.234.107)를 직접 입력해보자. 잘 접속될 것이다 네임 서버에 URL을 물어보지 않고 바로 IP 주소로 접속했기 때문이다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image8.png)

- 여기서 한 가지 확실히 할 점은, 네임 서버의 경우 URL 주소를 IP 주소로 변환해주는 편리한 서비스를 제공할 뿐, 직접적으로 컴퓨터와 연결된 네트워크에 영향을 미치지는 않는다는 것이다. 
- 다시 말해 지금 실습에서 확인했듯이 네임 서버가 없어도 IP 주소만 안다면 인터넷은 정상적으로 작동한다. 단, 지금처럼 접속할 웹 서버의 IP 주소를 아는 경우가 거의 없기 때문에 실질적으로는 인터넷을 정상적으로 사용할 수 없어서 네트워크도 안 되는 것처럼 느껴지는 것뿐이다.


#### step 4

- 이번에는 /etc/hosts 파일을 활용해보자.
- vi나 gedit으로 /etc/hosts 파일을 열어서 조금 전에 확인한 dm.n-mk.com 웹 사이트의 IP 주소(121.170.234.107)를 추가한 후 저장하고 닫자.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image9.png)

- 웹 브라우저를 닫고 다시 실행해서 dm.n-mk.kr에 접속하자. 접속이 잘 될 것이다. 하지만 그 외의 사이트는 계속 URL로 접속되지 않을 것이다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image10.png)

- 주소창에 URL을 입력했을 때 웹 브라우저는 /etc/resolv.conf 파일에 적혀 있는 nameserver를 통해 IP 주소를 얻기 전 /etc/hosts 파일을 조사하고, 해당하는 URL 주소와 IP 정보가 있는지 확인한다는 것을 알 수 있다.

#### step 5

- 이번에는 웹 브라우저를 속여 URL을 입력했을 때 다른 사이트에 접속하게 만들어보자.
- 다음과 같이 /etc/hosts 파일의 dm.n-mk.kr에 해당하는 IP 주소를 엉뚱한 사이트의 IP 주소(211.119.131.32, 한양사이버대학교 IP 주소)로 변경하고 저장하자.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image11.png)

- 웹 브라우저를 닫았다가 다시 실행해서 dm.n-mk.kr에 접속한다. 그러면 엉뚱한(?) 사이트에 접속할 것이다.
- \<실습 1\>에서 어느 정도 파악했겠지만, URL을 입력했을 때 어떻게 IP 주소를 획득하는지 정리하고 넘어가자.

#### IP 주소를 얻는 내부 흐름도

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image12.png)

- (1) 사용자가 웹 브라우저 등에서 URL을 입력한다(FTP나 ping 등의 명령도 모두 해당됨).
- (2) /etc/host.conf 파일을 조회해 우선순위가 무엇인지를 확인한다.

> /etc/host.conf 파일에는 URL 입력 시 IP 주소를 얻기 위해 먼저 확인해야 할 것이 결정되어 있다. 기본적으로 'orderhosts, bind'라고 입력됐거나 생략됐으면 먼저 /etc/hosts 파일을 찾아본다. /etc/hosts 파일에도 관련 정보가 없으면bind (DNS 클라이언트, 즉 /etc/resolv.conf 에 설정된 네임 서버에 질의하라는 의미)를 이용한다. 만약 네임 서버에 먼저질의한 후 없을 경우 /etc/hosts 파일을 확인하게 하고 싶으면 'order bind, hosts'로 변경한다. 또 'multi on'은 /etc/hosts 파일에 여러 개의 URL을 사용할 수 있다는 의미다.

- (3) 우선순위가 /etc/hosts 파일이므로 열어서 www.nate.com의 IP 주소가 적혀 있는지 확인한다.
- (4) /etc/hosts 파일에 www.nate.com의 IP 주소가 적혀 있다면, 네임 서버에 물어볼 필요 없이 IP 주소를 획득해서 해당하는 IP 주소로 연결한다(\<실습 1\>의 step 5 에서 웹 브라우저를 이렇게 속였다).
- (5) /etc/hosts 파일에 www.nate.com의 IP 주소가 없다면 /etc/resolv.conf 파일을 확인해서 'nameserver 네임서버IP' 부분이 있는지 확인한다.
- (6) /etc/resolv.conf 파일에 'nameserver 네임서버IP' 부분이 없다면,
- (7) IP 주소를 획득하는 데 실패하므로 www.nate.com의 IP 주소를 알 수 없다.
- (8) /etc/resolv.conf 파일에 'nameserver 네임서버IP' 부분이 적혀 있다면,
- (9) 해당 네임 서버에 www.nate.com의 IP 주소를 질의한다.

> 지금은 단순히 네임 서버에 www.nate.com을 질의해서 알려주는 과정을 간단히 표현했지만, 실제로는 더 복잡한 과정을거친다. 이는 잠시 후 살펴볼 네임 서버 구축에서 상세히 알아보도록 하고 일단은 네임 서버가 www.nate.com의 IP 주소를 알려주는 것을 응답한다고 생각하자.

- (10) 네임 서버가 www.nate.com의 IP 주소를 알면 알려준다.
- (11) 네임 서버가 응답하지 않거나 www.nate.com의 IP 주소를 알 수가 없다.

- 이 과정을 잘 살펴보면 실습 마지막 부분에서 dm-n.kr.com을 입력했는데 다른 엉뚱한 사이트가 나온 이유를 알 수 있을 것이다. 그 이유는 ①, ②, ③, ④의 과정만 거쳤기 때문이다.여기서 알 수 있는 사실은, 웹 브라우저는 최종적으로 얻은 IP 주소가 www.nate.com의 진짜 IP주소 앞 실습과 같이 가짜 IP 주소든 검증할 능력이 없으며, 단지 /etc/hosts 파일 또는 네임 서버가 알려준 IP 주소로 접속을 시도하는 것뿐이라는 점이다.

* * * 

# 네임 서버 구축

## 도메인 이름 체계

- 네트워크에 연결된 컴퓨터를 구분하는 유일한 방법은 IP 주소다. 따라서 웹 브라우저로 웹 서버에 접속하려면 120.50.132.112 등과 같은 IP 주소를 알아야 한다.

- 이러한 IP 주소는 외우기 어려우므로, 각 컴퓨터의 IP 주소에 외우기 쉬운 이름을 부여하면 된다.

- 예를 들어 1.1.1.1은 john이라는 이름으로, 2.2.2.2는 bann이라는 이름으로 관리하면 앞으로john이라는 컴퓨터를 찾아갈 때 자동으로 1.1.1.1이라고 알 수 있다(휴대전화에 전화번호를 저장한 후 전화번호를 외우지 않고 그 이름으로 전화를 거는 것과 같은 이야기다).

- 한 발 더 나아가서 IP 주소와 이름을 관리하는 전용 컴퓨터가 있을 경우 '이름 관리 전용 컴퓨터'의 IP 주소만 알면 다른 여러 가지 IP 주소를 모르더라도 언제든지 이름 관리 전용 컴퓨터'에서 확인할수 있다. 앞에서 굽네 치킨의 전화번호를 모르더라도 114 전화번호만 알면 되는 것과 비슷한 원리다. 이제 이름 관리 전용 컴퓨터'(앞으로는 네임 서버라고 부른다)에 관해 이야기해보자.

- 인터넷 초창기에는 전 세계 인터넷에 연결된 컴퓨터가 그렇게 많지 않았으므로, 1대의 네임 서버만으로도 IP 주소와 이름을 충분히 관리할 수 있었다. 하지만 인터넷이 폭발적으로 확장되면서 인터넷에 연결된 컴퓨터는 기하급수적으로 늘어났고, 몇 대의 네임 서버로는 실시간으로 생겼다 없어지는 인터넷상의 컴퓨터를 도저히 관리할 수 없게 되었다.

- 그래서 다음과 같은 트리 구조 형태의 도메인 이름 체계가 고안되었다. 음영이 들어간 사각형을 네임 서버 컴퓨터라고 생각하자. 또, 음영이 없는 사각형은 실제로 운영되는 컴퓨터라고 보면된다. 즉 ROOT(.) 네임 서버는 1단계 네임 서버인 com 네임 서버, net 네임 서버, org 네임 서버, edu 네임 서버 등과 국가 도메인인 kr, fr, sp 등을 관리한다. 그리고 1단계 네임 서버는 자신의 하위에 있는 2단계 네임 서버를 관리한다. 예를 들어 com 네임 서버는 nate, google, naver 등 2단계 도메인을 관리하는 네임 서버들만 관리하면 되는 것이다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image13.png)

- 네이트(회사 이름)의 도메인 이름은 무엇인가? 이 질문에 종종 www.nate.com이라고 대답하지만, 틀린 말이다. 네이트의 도메인 이름은 'nate.com'이다. www.nate.com은 nate.com 도메인에 속한 컴퓨터다(아마도 웹 서버 컴퓨터일 것이다).

## 로컬 네임 서버가 작동하는 순서

- 리눅스에는 각자 사용하는 네임 서버가 /etc/resolv.conf 파일에 'nameserver IP주소' 형식으로 설정되어 있다. 이 네임 서버를 로컬 네임 서버라고 부른다. 그래서 www.nate.com의 IP 주소를 요구하면 이 로컬 네임 서버에 질문하는 것이다.

- 그런데 로컬 네임 서버는 의외로 아는 것이 별로 없다. 로컬 네임 서버 혼자서 전 세계 모든 컴퓨터의 도메인 이름을 관리할 수는 없기 때문이다. 따라서 로컬 네임 서버는 자신이 아는 도메인 이름이면 바로 알려주지만, 자신이 모를 경우에는(이런 경우가 대부분일 것이다) 다음과 같은 작업을 수행한다.

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image14.png)

- (1) PC의 웹 브라우저 주소창에서 www.nate.com을 입력한다.

- (2) PC가 리눅스일 경우 /etc/resolv.conf 파일을 열어서 'nameserver 네임서버IP' 부분을 찾아 로컬 네임 서버 컴퓨터를 알아낸다.

- (3) 로컬 네임 서버에 www.nate.com의 IP 주소를 물어본다.
- (4) 로컬 네임 서버는 자신의 캐시 DB를 검색해 www.nate.com의 정보가 들어 있는지 확인한다(만약 정보가 있다면 바로 응답하지만 대개는 정보가 없다).
- (5) 로컬 네임 서버가 'ROOT 네임 서버'에 www.nate.com의 주소를 물어본다.
- (6) 'ROOT 네임 서버'도 www.nate.com의 주소를 모르므로 'com 네임 서버'의 주소를 알려주면서 'com 네임 서버'에 물어보라고 한다.
- (7) 로컬 네임 서버가 'com 네임 서버'에 www.nate.com의 주소를 물어본다.

- (8) 'com 네임 서버'도 www.nate.com의 주소를 모르므로 'nate.com'을 관리하는 네임 서버의 주소를 알려주면서 'nate.com' 네임 서버에 물어보라고 한다.

- (9) 로컬 네임 서버가 'nate.com 네임 서버'에 www.nate.com의 주소를 물어본다.
- (10) nate.com 네임 서버는 네이트에서 구축한 네임 서버이므로 ○○○.nate.com이라는 이름을 가진 컴퓨터의 목록이 모두 있다. www.nate.com의 IP 주소도 알기 때문에 IP 주소를 알려준다. 
- (11) 로컬 네임 서버는 www.nate.com의 IP 주소를 요구한 PC에 IP 주소를 알려준다.

> 여기서 기억할 점은 'nate.com 네임 서버'는 현재 자신의 캐시 DB에 적혀 있는 것을 알려줄 뿐이며, 실제 111.111.111.111 컴퓨터가 작동하는지는 관심을 두지 않는다. 즉, 자신이 잘못된 정보를 알고 있더라도 그대로 알려준다(114 안내 담당자가 고객이 질문한 '굽네 치킨'이 영업 중인지 확인하지 않고 그냥 자신이 아는 전화번호를 알려주는 것과 같은 이야기다).

- (12) PC는 획득한 IP 주소로 접속을 시도한다.

## 캐싱 전용 네임 서버

- 캐싱 전용 네임 서버(Caching-only Nameserver)는 PC에서 URL로 IP 주소를 얻고자 할 때 해당하는 URL의 IP 주소를 알려주는 네임 서버를 말한다. 예로 들면 '로컬 네임 서버'라고 지칭한 컴퓨터가 캐싱 전용 네임 서버의 역할을 수행한다. 

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image15.png)

### 실습2

Server를 캐싱 전용 네임 서버로 구축하자. 그리고 Client와 Server(B)에서 직접 구축한 Server를 네임 서버로 사용하자.

#### step 0

- Server를 처음 설치 상태로 초기화하자.
- 부팅한다. root 사용자로 접속하고 터미널을 하나 연다

#### step 1

Server에 네임 서버를 설치하고 관련된 설정을 한다.

- <b>dnf -y install bind bind-chroot</b> 명령을 입력해 네임 서버와 관련된 패키지를 설치하자.
- 캐싱 전용 네임 서버와 관련된 설정 파일인 /etc/named.conf 를 vi 에디터로 열어서 수정하고 저장하자.

> gedit을 써도 관계없지만 행 번호가 보이지 않으므로 지금은 vi 에디터가 더 편하다. vi 에디터에서 행 번호를 보려면 ':set number'를 입력한다.

```
11행쯤 수정: listen-on port 53 [127.0.0.1; ];     ->    listen-on port 53 [ any; ];
12행쯤 수정: listen-on-v6 port 53 [ ::1; ];    -> listen-on-v6 port 53 [ none; ];
19행쯤 수정: allow-query  [ localhost; ];     -> allow-query   [ any; ];
34행쯤 수정: dnssec-validation yes;       -> dnssec-validation no;
```

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image16.png)

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image17.png)

- 지금 편집한 내용은 VirtualBox 네트워크 주소 안에 있는 모든 컴퓨터가 네임 서버를 사용할 수 있게 설정하는 것이다.

- 다음 명령을 참고해 서비스를 작동하자. 네임 서버의 서비스(=데몬) 이름은 'named'다.

```
systemctl restart named     -> 재시작(stop + start)
systemctl enable named    -> 네임 서버 상시 가동
systemctl status named     -> 네임 서버 상태 확인
```

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image18.png)

> 서비스와 소켓<br>서비스(=데몬)와 관련된 스크립트 파일은 /usr/lib/systemd/system/ 디렉터리에 있다. 파일 이름은 대부분 '서비스이름.service'인데 지금 네임 서버는 named.service 파일이다. 이 파일을 실행/중지하는 방법은 <b>systemctl start/stop 서비스이름</b> 명령이다. 그리고 이 서비스를 부팅 시 자동으로 작동하게 하려면 <b>systemctl enable 서비스이름</b> 명령을 실행한다. 그러면 /usr/lib/systemd/system/named.service 파일이 /etc/systemd/system/multi-user.target.wants/named.service 링크 파일로 생성된다. CentOS가 부팅되면 /etc/systemd/system/multi-user.target.wants/ 디렉터리의 링크 파일들을 자동으로가동시켜 준다.

- <b>firewall-config</b> 명령을 입력해 [방화벽 설정]을 실행한다. [설정]에서 [영구적]을 선택한 후 [영]에서[public]이 선택된 상태로 오른쪽 [서비스] 탭 [dns]의 체크를 켜서 DNS 서버를 열어주자. 설정을 적용하기위해 메뉴의 [옵션] - [Firewalld 다시 불러오기]를 선택한 후 [방화벽 설정]을 닫는다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image19.png)

- 네임 서버가 잘 작동하는지는 <b>dig @네임서버IP 조회할URL</b> 형식으로 확인할 수 있다. 여기서는 <b>dig@10.0.2.100 www.nate.com</b> 명령을 입력해 간단히 테스트해보자.

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image20.png)

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image21.png)

- <b>nslookup</b> 명령을 이용하는 방법도 있다. 다음 명령을 입력해 테스트할 수 있다.

```
nslookup
server 테스트할 네임 서버IP     -> 여기서는 우리가 구축한 10.0.2.100 입력
조회할 URL    -> 여기서는 www.nate.com 입력
exit
```

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image22.png)

#### step 2

Client를 실행한 후 앞에서 구축한 Server를 네임 서버로 사용해보자.

- 필요하다면 Client를 초기화하자.
- 다음 명령을 입력해 Server에서 구축한 네임 서버가 잘 가동하는지 확인해보자.

```
nslookup
server 네임서버IP     -> 네임 서버를 우리가 구축한 10.0.2.100으로 사용한다.
www.nate.com
exit
```

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image23.png)

- 네임 서버가 작동되는 것을 확인했으므로 네임 서버를 고정해서 지정하자. <b>su-c 'gedit /etc/resolv.conf'</b> 명령을 입력해 에디터로 /etc/resolv.conf 파일을 열고 Server의 IP 주소인 10.0.2.100 으로 변경한 후 저장하고 닫는다 (root 사용자 권한을 얻은 후 수정해야 한다).

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image24.png)

- 웹 브라우저로 아무 웹 사이트나 접속해보자. 이제는 다음과 같이 변경된 캐싱 전용 네임 서버를 이용해서 웹 서핑하는 것이다.

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image25.png)
