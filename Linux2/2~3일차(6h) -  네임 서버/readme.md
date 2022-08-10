# 네임 서버의 개념

## 네임 서버 개요

- 네임 서버는 DNS(Domain Name System) 서버라고도 한다. 우리가 웹 브라우저나 FTP 클라이언트를 사용할 때 http://www.nate.com 또는 ftp://mirrors.kernel.org/ 등과 같은 URL을 사용하는데, 실제 원하는 서버에 접근하려면 이 URL을 해당 컴퓨터의 IP 주소로 변환시켜야 한다. 바로 이 일을담당하는 것이 네임 서버 또는 DNS 서버라고 하는 컴퓨터다.

- 이렇게 www.nate.com을 IP 주소로 변환하는 과정을 이름 해석(name resolution)이라고 한다.

```
www.nate.com 120.50.132.112
```

- 네트워크에서 컴퓨터를 구분하는 유일한 방법은 IP 주소다. 즉 인터넷에 연결된 모든 컴퓨터에는 중복되지 않는 IP 주소가 있다. 그러므로 자주 접속하는 웹 서버나 FTP 서버의 IP 주소를 모두 안다면, DNS 서버 (네임 서버)를 사용할 필요가 없다. 오히려 www.nate.com을 120.50.132.112와 같은 IP 주소로 알아내는 과정이 생략되므로 인터넷 속도가 더 빨라질 것이다. 그러나 웹 서핑 시 URL 주소를 사용하지 않고 IP 주소를 외워서 사용하는 경우는 특수한 목적 외에거의 없을 것이다.

- 네임 서버의 변천사를 나름대로 가정해보았다. 요목조목 따진다면 일부는 틀린 얘기라고 할 수도 있겠지만, 네임 서버의 전반적인 이해를 돕기 위해 가정한 이야기이므로 그냥 넘어가주기 바란다. 인터넷이 도입되던 시절에는 인터넷에 연결된 컴퓨터가 그리 많지 않았다. 그래서 인터넷을 통해 상대 컴퓨터에 접속하기 위해 아마 메모지 같은 곳에 IP 주소를 적어 놓았을지도 모른다. 어차피 접속할 컴퓨터가 몇 대 되지 않았으므로, 가까운 사람 몇몇의 전화번호는 수첩을 찾지 않고도 외우듯이 IP 주소도 자연스럽게 외워졌을 것이다.

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

- 위 그림 처럼 사용자는 10.10.10.10이라는 네임 서버의 IP 주소만 알면(=114라는 전화번호만알면) 언제든지 해당하는 URL (굽네 치킨)의 IP 주소(전화번호)를 알아낼 수 있다.

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

#### step 3

Server(B) 텍스트 모드에서 설정해보자.

-  Server(B)를 처음 설치 상태로 초기화하자.
-  root 사용자로 접속한다vi 에디터로 /etc/resolv.conf 파일을 열고 다음을 참고해 에서 구축한 네임 서버로 변경한 후 vi 에디터를 종료한다.

```
nameserver 8.8.8.8      -> nameserver 10.0.2.100
```

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image26.png)

- nslookup 명령으로 네임서버가 잘 작동하는지 확인하자.

```
nslookup
server    -> 10.0.2.100
www.nate.com
exit
```

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image27.png)

#### step4

Server(B)는 Firefox와 같은 웹 브라우저를 사용할 수 없지만, 텍스트 기반의 웹 브라우저를 사용하면 접속할 수 있다.

- 먼저 <b>dnf -y install --enablerepo=powertools elinks</b> 명령을 입력해 elinks 패키지를 설치하자.
- <b>elinks</b> 명령을 입력하자. 환영 메시지가 나오면 [Enter]를 누른다.

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image28.png)

- 접속할 URL을 입력하자. 한글은 정상적으로 보이지 않으므로 영문 사이트를 입력하자. www.kernel.org를 입력하고 Tab을 눌러 \<OK\>로 이동한 후 [Enter]를 누른다.

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image29.png)

- 텍스트 모드로 사이트에 접속되는 것을 확인할 수 있다. 화살표 키와 [Enter]를 이용하면 웹 서핑할 수 있다. 직접 해보자.

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image30.png)

-  [Esc]를 누르면 왼쪽 위에 메뉴가 나온다. 살펴보면 일반 웹 브라우저와 비슷한 메뉴다. [Tab], 화살표 키,[Enter]를 이용해 메뉴를 선택하고 실행할 수 있다.

- elinks를 종료하려면 [File] → [Exit]를 선택한다.

#### step 5

- WinClient에서 Server에 설정한 네임 서버를 이용하게 하자
- [제어판] → [네트워크 및 인터넷] → [네트워크 상태 및 작업 보기] → [Ethernet0]을 클릭해서 [이더넷상태]를 열자.

- [이더넷 상태]에서 \<속성\> → [인터넷 프로토콜 버전 4(TCP/IPv4)] → [속성]을 선택한 후 [다음 DNS서버 주소 사용]을 선택해 'ServerIP주소'를 입력하고 \<확인\> 및 \<닫기\>를 클릭해 창을 모두 닫는다.

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image31.png)

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image32.png)

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image33.png)

- 웹 브라우저를 실행해서 아무 웹 사이트나 접속해보자.

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image34.png)

- 다시 원상태로 돌려놓자. 


## 마스터 네임 서버

- 마스터 네임 서버(Master Nameserver)는 john.com과 같은 도메인에 속해 있는 컴퓨터들의 이름을 관리하고, 외부에서 www.john.com이나 ftp.john.com 등의 컴퓨터 IP 주소를 알고자 할 때 해당 컴퓨터의 IP 주소를 알려주는 네임 서버를 말한다. 
- 그러므로 일반적으로 john.com이라는 도메인으로 인터넷 서비스를 하려면 john.com 네임 서버를 구축해 외부에서 www.john.com이나 ftp.john.com 등으로 접속할 수 있게 해야 한다.

![image35](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image35.png)

#### 위 그림의 '마스터 네임 서버 구성도'에 대한 설명은 다음과 같다. 

- (1) 우선 테스트하기 위해 Server(B)에 FTP 서버를 설치하고, Server에는 네임 서버와 웹 서버를 설치한다. Server의 네임 서버 설정에서 www.john.com은 Server의 IP 주소인 10.0.2.100 으로 설정하고 ftp.john.com은 Server(B)의 IP 주소인 10.0.2.200으로 설정한다.

- (2) 구성이 완료되면 Client에서 www.nate.com의 접속을 시도할 때 다음과 같은 순서로 진행된다. 
	- ① 설정된 네임 서버인 10.0.2.100 에게 www.nate.com의 IP 주소를 요청한다.
	- ② 10.0.2.100 은 자신의 DB를 검색해 www.nate.com이 있는지 확인한다. 해당 내용이 없을 것이므로 외부 인터넷에서 www.nate.com의 IP 주소를 알아온다.
	- ③ 알아온 www.nate.com의 IP 주소를 Client에게 알려준다(Server는 마치 자기가 원래 알고 있었던 척한다).

- (3) 지금까지의 과정은 캐싱 전용 네임 서버와 큰 차이가 없다. 이번에는 Client에서 www.john.com에 접속을 시도할 때의 과정을 알아보자. 다음과 같은 순서로 진행된다.
	- ① 설정된 네임 서버인 10.0.2.100에게 www.john.com의 IP 주소를 요청한다.
	- ② 10.0.2.100은 자신의 DB를 검색해 www.john.com이 있는지 확인한다. 그런데 john.com은 자신이 관리하는 도메인이므로, www.john.com의 IP 주소(10.0.2.100)와 ftp.john.com의 IP 주소(10.0.2.200)를 갖고 있다. 그러므로 외부 인터넷으로 나갈 필요 없이 바로 Client에게 해당 IP 주소를 알려준다.

- (4) 다음은 마지막으로 위 그림의 왼쪽 위에 표현한 외부 '인터넷상에 있는 컴퓨터'에서 ftp.john.com에 접속할 때의 순서다.
	- ① 외부 인터넷상의 컴퓨터는 자신의 로컬 네임 서버 (그림에는 나와 있지 않다. 그냥 '로컬 네임 서버 A'라고 부르겠다)에게 ftp.john.com의 IP 주소를 요청한다.
	- ② 로컬 네임 서버 A는 아마도 ftp.john.com의 IP 주소를 모를 것이므로 'ROOT 네임 서버'에게 IP 주소를 요청할 것이다. ROOT 네임 서버는 'COM 네임 서버'의 주소를 알려주며 그쪽에 요청하도록 한다.
	- ③ 로컬 네임 서버 A는 다시 COM 네임 서버에게 의뢰한다. COM 네임 서버는 john.com의 도메인을 관리하는 john.com 네임 서버의 IP 주소인 10.0.2.100을 로컬 네임 서버 A에게 알려준다.
	- ④ 로컬 네임 서버 A는 john.com 네임 서버인 10.0.2.100에게 ftp.john.com의 IP 주소를 요청한다.
	- ⑤ john.com 네임 서버는 자신의 DB에 ftp.john.com의 IP 주소가 있으므로 ftp.john.com의 IP 주소인 10.0.2.200을 알려준다.
	- ⑥ 로컬 네임 서버 A는 ftp.john.com의 IP 주소인 10.0.2.200을 요청했던 인터넷상의 컴퓨터에게 알려준다.
	- ⑦ 인터넷상의 컴퓨터는 10.0.2.200(Server(B))으로 접속한다.

- 이렇게 자신이 별도로 관리하는 도메인이 있으며 외부에서 자신이 관리하는 컴퓨터의 IP 주소를 물어볼 때, 자신의 DB에서 찾아서 알려주는 네임 서버를 '마스터(master) 네임 서버'라고 부른다.

### 실습 3

- Server에 john.com의 마스터 네임 서버를 설치하고 운영해보자.

#### step 0

- <code>Server</code> \<실습 2\>에 이어서 실습한다.

#### step 1

- <code>Server</code> 웹 서버를 설정하자. 
- <b>rpm -qa httpd</b> 명령을 입력해 웹 서버가 설치되었는지 확인한다. 아마 설치되어 있지 않을 것이다. <b>dnf -y install httpd</b> 명령을 입력해 설치한다.
- <b>systemctl status httpd</b> 명령을 입력해 웹 서비스(httpd)가 작동하는지 확인하고, 정지되어 있다면 <b>systemctl start httpd</b> 명령을 입력해 웹 서비스를 시작한다. 그리고 다시 웹 서비스가 잘 작동하는지 확인한다.

![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image36.png)

- <b>firewall-config</b> 명령을 입력해 [방화벽 설정]을 실행한다. [설정]에서 [영구적]을 선택한 후 [영역]에서 [public]이 선택된 상태로 오른쪽 [서비스] 탭 [http]와 [https]의 체크를 켜서 웹 서버를 열자. 설정을 적용하기 위해 메뉴의 [옵션] → [Firewalld 다시 불러오기]를 선택한 후 [방화벽 설정]을 닫는다.

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image37.png)

- <b>gedit /var/www/html/index.html</b> 명령을 입력해 /var/www/html/ 디렉터리에 index.html 파일을 만든다. 그리고 '\<h1\> CentOS 웹 서버 입니다. \</h1\>'을 입력한 후 저장하고 닫는다.

- 이로써 아주 간단한 웹 서버 구축이 완료되었다.

#### step 2

- Server(B) FTP 서버를 설치하고 설정한다.
- <b>dnf -y install vsftpd</b> 명령을 입력해 FTP 서버를 설치한다.
- <b>firewall-cmd --permanent --add-service=ftp</b> 명령을 입력해서 FTP 서비스의 방화벽 설정을 허용한다. 또 <b>firewall-cmd --reload</b> 명령으로 설정 내용을 적용시킨다. 'success' 메시지가 나오면 잘 설정된 것이다.
- /var/ftp/ 디렉터리로 이동한 후 <b>vi welcome.msg</b> 명령을 입력해 welcome.msg라는 빈 파일을 생성하자. welcome.msg 파일 안에는 다음 내용을 채운 후 저장하고 닫는다.
```
####################
Welcome this is ftp server
####################
```

- vi 에디터로 /etc/vsftpd/vsftpd.conf 파일을 열어서 제일 위에 banner_file=/var/ftp/welcome.msg'를 추가한 후 저장하고 닫는다

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image38.png)

> 지금 한 작업은 외부에서 FTP 서버로 접속했을 때 /var/ftp/welcome.msg 파일의 내용을 환영 메시지로 보여주라는 의미다.

- <b>systemctl restart vsftpd</b> 명령을 입력해 FTP 서버를 시작한다.이로써 간단한 FTP 서버가 구축되었다.

#### step 3

<code>Server</code> john.com 도메인에 대한 설정을 해준다.

- vi 에디터나 gedit으로 /etc/named.conf 파일을 열어서 맨 아래에 다음 내용을 추가한 후 저장하고닫는다.

> 네임 서버는 설정 파일이 한글자라도 틀릴 경우 데몬 자체가 가동하지 않을 수 있으므로 주의해서 입력해야 한다. 물론 대소문자도 모두 정확히 구분되어야 한다.

```
zone "john.com" IN {
    type master;
	file "john.com.db";
	allow-update { none; };
};
```

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image39.png)

<table>
	<tr>
		<td>
			<h3>/etc/named.conf 파일</h3>
			<ul>
				<li>/etc/named.conf 파일은 네임 서버 서비스가 시작될 때 제일 먼저 읽는 파일이다.</li>
				<li>
					설정 형식 중에서 중요한 부분은 다음과 같다.<br>
					<pre>
						options {
							listen-on port 53 { any; }      -> 네임 서버에 접속이 허용된 컴퓨터의 IP 주소
							directory "디렉토리이름" ;    -> 네임 서버 DB 파일이 들어 있는 디렉토리
							dump-file "덤프파일이름" ;   -> 정보가 갱신될 때 저장되는 파일 
							statistics-file "통계파일이름" ; -> 통계 처리 용도의 파일
							allow-query { 컴퓨터; }          -> 도메인 이름의 쿼리가 허용된 컴퓨터 또는 IP 주소
						};
						zone "도메인이름" IN {
							type hint 또는 master 또는 slave;    -> 마스터 네임 서버는 master
							file "파일이름";       -> options의 directory에 생성될 "도메인 이름"의 상세 설정 파일
							allow-update { IP 주소 } 또는 { none };   -> 2차 네임 서버의 주소. 생략하면 none으로 됨
						};
					</pre>
				</li>			
			</ul>	
		</td>
	</tr>
</table>

- <b>named-checkconf</b> 명령을 입력해 입력한 내용이 문법상 틀리지 않는지 확인해보자. 아무 메시지도 안 나오면 문법상 틀린 것이 없다는 뜻이다. 문법이 틀렸을 경우 행 번호와 오류 내용이 출력된다.

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image40.png)

- 우선 /var/named/ 디렉터리로 이동한 후 <b>touch john.com.db</b> 명령을 입력해 john.com.db라는 이름의 빈 파일을 생성한다. 이 파일을 포워드 존 파일 또는 정방향 영역 파일이라고 부른다.

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image41.png)

- vi나 gedit으로 john.com.db 파일을 열고 다음 내용을 입력한다.

```
$TTL        3H
@   SOA   @      root.   ( 2  1D  1H  1W   1H )
      IN      NS    @
      IN      A      10.0.2.100	  

www   IN   A      10.0.2.100
ftp      IN   A      10.0.2.200
```

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image42.png)

> 이번 실습의 경우 10.0.2.100은 네임 서버 겸 웹 서버 역할을 할 것이며 10.0.2.200은 FTP 서버 역할을 할 것이다.

- <b>named-checkzone john.com john.com.db</b> 명령을 입력해 설정한 파일의 문법에 이상이 없는지 확인하자 (명령은 <b>named-checkzone 도메인이름 설정파일이름</b> 형태다).

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image43.png)

- 포워드 존 파일
- 포워드 존 파일의 문법을 몇 개 요약하면 다음과 같다.
	- ; (세미콜론): 주석을 의미한다.
	- STTL: Time To Live의 약자로, www.john.com의 호스트 이름을 질의해갔을 때 질의해간 다른 네임 서버가 해당 IP 주소를 캐시에 저장하는 시간을 말한다. 3H는 3시간(Hour)을 의미한다.
	- @: /etc/named.conf 에 정의된 john.com을 의미(john.com으로 고쳐 써도 됨)한다.
	- IN: 클래스 이름으로 internet을 의미한다.
	- SOA: Start Of Authority의 약자로 권한 시작을 뜻한다. 또 괄호 안의 숫자는 시간을 의미하는데 차례로 serial(버전 정보), refresh(상위 네임 서버에 업데이트된 정보를 요청하는 간격). retry(상위 네임 서버에문제가 발생했을 때 재접속 간격), expire(상위 네임 서버에 접속하지 못할 경우 이전 정보를 파기하는 간격), minimum (이 시간 이후 정보가 삭제됨)을 말한다. 여기서 H는 Hour, D는 Day, W는 Week의 약자다.
	- NS: Name Server의 약자로 설정된 도메인의 네임 서버 역할을 하는 컴퓨터를 지정한다.
	- MX: Mail Exchanger의 약자로, 메일 서버 컴퓨터를 설정한다. 
	- A: 호스트 이름에 상응하는 IP 주소를 지정한다.
	- CNAME: 호스트 이름에 별칭을 부여할 때 사용한다. 

- 설정한 내용을 적용하기 위해 <b>systemctl restart named</b> 명령을 입력해 네임 서비스를 재시작하고 <b>systemctl status named</b> 명령을 입력해 확인한다.

![image44](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image44.png)

- <b>firewall-config</b> 명령을 입력해 [방화벽 설정]을 실행한다. [설정]에서 [영구적]을 선택한 후 [서비스탭의 [dns]가 체크됐는지 확인한다(\<실습 2\> 에서 이미 해줬다).

- 이렇게 해서 Server (B)는 FTP 서버로 구축했고, Server는 네임 서버와 웹 서버 용도로 구축했다. 이제 Client에서 작동을 확인한다.

#### step 4

- Client 마스터 네임 서버의 정상적인 작동을 확인한다.
- 터미널에서 <b>cat /etc/resolv.conf</b> 명령을 입력해 네임 서버가 Server인 10.0.2.100으로 되어있는지 확인한다(\<실습 2\>에서 이미 변경했다).
- 웹 브라우저에서 www.john.com으로 접속해보자. 이번 실습의 Server에 만든 index.html 홈페이지가 열릴 것이다.

![image45](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image45.png)

- 터미널에서 <b>su -c 'dnf -y install ftp'</b> 명령으로 FTP 클라이언트 패키지를 설치한 후 <b>ftp ftp.john.com</b> 명령을 입력해 FTP 서버에 접속해보자. 환영 메시지를 보면 우리가 Server (B)에 구축한 FTP 서버에 접속할 수 있는 것을 확인할 수 있다(사용자는 centos로 로그인한다)

![image46](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image46.png)

## 라운드 로빈 방식의 네임 서버

- 네이버, 다음과 같은 포털 사이트 웹 서버에는 수십만 이상의 접속이 동시에 이루어질 것이다. 따라서 웹 서버를 1대가 아닌 여러 대로 운영해서, 웹 클라이언트가 서비스를 요청할 경우 교대로 서비스를 실행할 것이다. 그러면 웹 서버의 부하를 여러 대가 공평하게 나눌 수 있다. 이러한 방식을 라운드 로빈(Round Robin) 방식이라고 부른다.

- 예를 들어 외부 사용자는 결국 john.com 네임 서버에 www.john.com의 IP 주소를 요청할 것이다. 이때 www.john.com에 해당하는 웹 서버를 3대 운영한다고 가정하고 각각의 IP가 1.1.1.1, 1․1․1.2, 1.1.1.3이라면, john.com 네임 서버는 물어오는 순서대로 1.1.1.1, 1․1.1.2, 1.1.1.3을 차례로 알려준다. 그러면 3대의 웹 서버에 부하가 공평하게 나뉜다.

![image47](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image47.png)

- 호스트 운영체제의 Windows PowerShell이나 명령 프롬프트에서 다음과 같이 <b>nslookup</b> 명령을 입력해 확인해보면, 네이버 같은 웹 사이트도 여러 대의 웹 서버를 운영한다는 것을 알 수 있다.

![image48](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image48.png)

- 이번 실습은 여러 대의 웹 서버를 설치해서 운영해야 한다. 하지만 환경이 완전하지 않을 것이므로, 이미 인터넷에 구현된 다른 웹 사이트를 우리가 구현한 웹 서버라고 간주하고 실습을 진행하겠다. 그렇게 하면 라운드 로빈 방식이 더욱 확실하게 눈에 보일 것이다.

- 즉 www.john.com 접속 시 A, B, C 3개의 웹 사이트를 차례로 보여주는 방식으로 할 것이다.

### 실습4

- 라운드 로빈 방식의 네임 서버를 구현해보자.

#### step 0

\<실습 3\>에 이어서 진행한다.

#### step 1

- Server를 라운드 로빈 방식의 네임 서버로 설정하자.
- 기존에 구축된 웹 서버의 IP 주소를 몇 개 확인해보자. 이번 예에서는 <b>nslookup</b> 명령을 입력하여 www.danawa.com, www.nate.com, www.hanbit.co.kr 3개의 IP 주소를 확인할 것이다(웹 사이트 3개가 달라도 관계없다. 접속되는 아무 웹 사이트의 IP 주소를 확인하자.)

![image49](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image49.png)

이렇게 확인한 3개의 IP 주소(19,205.194.11, 120.50.131.112, 218.38.58.195)를 www.john.com의 웹 서버 3 대라고 가정하자.

gedit으로 /var/named/john.com.db 파일을 다음과 같이 수정하고 저장한 후 닫는다. 기존에 있던 'www IN A 10.0.2.100' 행은 삭제했으며 'webserver.john.com.'의 제일 뒤에 '.'이 있는 것에 주의하자.

```
$TTL        3H
@   SOA   @          root.   ( 2  1D  1H  1W   1H )
      IN      NS        @
      IN      A          10.0.2.100
	  
ftp      IN   A          10.0.2.200
www   IN   CNAME   webserver.john.com.
webserver  100        IN         A     119.205.194.11
               200        IN         A      120.50.131.112
               300        IN         A      210.38.58.195
```

![image50](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image50.png)

>  CNAME은 Canonical NAME의 의미로 기준이 되는 이름이며, CNAME 행 아래 3개 행이 기준에 해당한다. 100/200/300은 단순한 차례를 나타내는 것이며 서로 다른 숫자면 아무거나 관계없다.

-  변경 사항을 적용하기 위해 <b>systemctl restart named</b> 명령을 입력하여 네임 서버를 다시 가동한다.
- <b>nslookup</b> 명령을 입력한 다음 <b>server 10.0.2.100</b> 명령을 입력하고 www.john.com의 정보를 확인해본다.

![image51](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/2~3%EC%9D%BC%EC%B0%A8(6h)%20-%20%20%EB%84%A4%EC%9E%84%20%EC%84%9C%EB%B2%84/images/image51.png)

#### step 2

Client 외부에서 라운드 로빈의 작동을 테스트한다.

- 웹 브라우저를 실행해 www.john.com에 접속해본다.
- 웹 브라우저를 닫고 다시 실행해서 www.john.com에 접속해본다. 이렇게 여러 번 반복하면 3개의 사이트가 골고루 돌아가면서 나타날 것이다(잘 안 되면 웹 브라우저를 닫고 다시 실행해본다).

- 이번 실습에서는 라운드 로빈 방식의 작동을 확인하기 위해 www.john.com 접속 시 세 사이트로 접속되는지 확인해보았지만, 실제 상황이라면 웹 서버의 IP 주소가 다를 뿐 www.john.com에 접속하면 당연히모두 같은 웹 페이지가 나와야 한다.

- 지금까지 네임 서버를 다양한 방법으로 구현해보았다. 앞으로 사용된 네트워크 서버는 네임 서버와 같이 사용되어야만 가치가 있다. 예를 들어 웹 서버를 구축했을 때, 웹 클라이언트 사용자에게 http://10.0.2.100/ 과 같은 IP 주소로 웹 서버를 접속하도록 알려줄 수는 없을 것이다. 꼭 http://www.john.com/ 과 같은 URL로 접속하도록 알려줘야 한다. 그러려면 네임 서버의 설정 (특히 정방향 영역 혹은 포워드 존)이 반드시 선행되어야 한다.

> 역방향 영역<br>지금 설정한 내용은 도메인을 IP 주소로 변경하는 정방향 영역을 다뤘다. 반대로 IP 주소를 통해 도메인을 알 수도 있는데, 이를 역방향 영역 또는 리버스 존Reverse Zone이라고 한다. 실습에서는 역방향 영역을 별도로 설정하지 않아도 문제가 없으므로 생략했지만, 필요하다면 직접 인터넷을 검색해서 학습하기를 권장한다.
