# 프록시 서버의 개념
- 프록시(Proxy)는 단어 그대로 '대리인' 역할을 하는 서버다. 웹 환경에서 프록시 서버의 역할은 웹 클라이언트와 웹 서버 사이에서 요청한 데이터를 전달하는 것이다. 이때 프록시 서버는 웹 서버에서 가져온 데이터를 웹 클라이언트에게 전송한 후 데이터를 캐시에 저장한다. 그리고 웹 클라이언트가 같은 데이터를 요청하면, 웹 서버가 아니라 자신의 캐시에서 해당 데이터를 보낸다. 이를 통해 웹 클라이언트에게 빠르게 필요한 내용을 보낼 수 있다.
- 다음을 통해 작동 방식을 살펴보자.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image1.png)

- ① '웹 브라우저 1'에서 웹 서핑을 요청하면
- ②/③ 프록시 서버가 대신 웹 서버에 접근해 데이터를 가져온다.
- ④ 가져온 데이터를 우선 캐시에 저장해둔다.
- ⑤ '웹 브라우저 1'에게 요청한 데이터를 전송한다.
- ⑥ '웹 브라우저 2'가 웹 서핑을 요청하면 (같은 웹 사이트를 요청한다고 가정)
- ⑦ 프록시 서버는 외부로 나가지 않고 자신의 캐시에 있던 데이터를 가져와서
- ⑧ '웹 브라우저 2'에게 바로 전송한다.
<br><br>
- 이와 같은 방식이므로 웹 클라이언트의 전반적인 웹 서핑 속도가 향상되는 것이다.

> 위 그림의 예에서는 웹(HTTP)의 예로만 표현했지만, 프록시 서버는 FTP 지원한다.

* * *
# 프록시 서버 구현

프록시 서버 중 CentOS에서 제공되는 Squid 프록시 서버를 설치해서 운영해보자.

### 실습1

- Server에 프록시 서버를 설치하고 구현해보자.

#### step 0

- <code>Server</code> Server를 처음 설치 상태로 초기화하자. 
-  부팅하고 root 사용자로 접속한다.

#### step1

<code>Server</code> Squid 프록시 서버를 설치하고 설정하자.

- <b>dnf -y install squid</b> 명령으로 squid 관련 패키지를 설치하자.
- vi 에디터나 gedit으로 설정 파일인 /etc/squid/squid.conf 파일을 다음과 수정하고 저장한다.

```
29행쯤 추가: acl  centos8  src  10.0.2.0/255.255.255.0
57행쯤 추가: http_access allow centos8
65행쯤 주석 제거 후 수정: cache_dir ufs /var/spool/squid  1000 16 256
제일 아래 추가: visible_hostname centos8
```

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image2.png)

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image3.png)

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image4.png)

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image5.png)

- acl은 Access Control List의 약자로, 모든 컴퓨터가 아닌 지정된 컴퓨터나 네트워크만 프록시 서버에 접근할 수 있도록 제한하는 구문이다. 이 예에서는 10.0.2.0 네트워크의 컴퓨터를 centos8이라는 이름으로 지정했다.

- http_access는 allow와 deny를 설정할 수 있는데, 여기서 centos8 이름으로 설정된 네트워크의 접근을 허용하는 cache_dir은 위 그림에 나오는 캐시할 디스크를 지정한다. ufs는 일반적으로 사용되는 스퀴드용 파일시스템으로 지정하며 /var/spool/squid 는 캐시 디렉터리를 적어준다. 1000은 캐시할 데이터 공간을 MB 단위로 지정한다. 16은 캐시에서 사용할 하부 디렉터리 개수, 256은 앞의 16개 디렉터리 안에 다시 생성할 디렉터리 개수를 지정한다. cache_dir에 지정된 값들은 서버 및 네트워크 상황에 맞게 변경해서 사용하면 된다.

- visible_hostname은 네트워크의 이름을 외부에 보이도록 설정하는 것인데 별로 중요하지 않다. 또 62행쯤에 Squid는 기본적으로 3128번 포트를 사용하는 것으로 되어 있다. 필요하다면 이 포트를 8080 등으로 변경해도 된다. 그 외에 squid.conf의 자세한 문법은 http://www.squid-cache.org/Doc/config/ 를 참고하자.

- <b>firewall-cmd --permanent --add-port=3128/tcp</b> 명령과 <b>firewall-cmd --reload</b> 명령으로 관련 포트인 3128번을 허용하자.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image6.png)

- 아직 squid 서비스를 시작하지 말자.

#### step 2

<code>Client</code> 리눅스에서 테스트해보자.

- Client를 처음 설치 상태로 초기화하고 부팅하자.
-  Firefox를 실행한 후 오른쪽 상단의 [三] → [Preferences]를 선택하고, [Preferences] 화면에서 제일 아래로 스크롤해 [Network Proxy] 오른쪽의 \<Settings\>를 클릭한다. [Connection Settings]에서 [Manual proxy configuration]을 선택한 후 [HTTP Proxy]에는 프록시 서버(Server) 주소인 10.0.2.100을, [포트]에는 3128을 입력한다. 그리고 아래에 있는 [Use this proxy server for all protocols]의 체크를 켠다. 설정이 완료되면 \<OK\> 버튼을 클릭해서 마친다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image7.png)

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image8.png)

- 웹 브라우저를 닫고 다시 실행해서 아무 사이트나 들어가보자. 오류 메시지가 나올 것이다. 아직 프록시 서버를 가동하지 않아서 나오는 메시지다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image9.png)

#### step 3

<code>Server</code> Squid 프록시 서버를 가동하자.

- <b>systemctl restart/enable/status squid</b> 명령을 차례로 입력해 squid 서비스를 가동하자.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image10.png)

#### step 4

<code>Client</code> Firefox를 새로 고침하면 웹 서핑이 정상적으로 될 것이다. 이제부터는 프록시서버가 작동하고 웹 데이터는 캐시에 저장될 것이다.

#### step 5
-  Windows 10은 Windows [시작] → [설정]을 클릭하고 [네트워크 및 인터넷]을 클릭한다. 왼쪽 [프록시]를 선택해 [자동으로 설정 검색]을 끄고 [프록시 서버 사용]을 켠 후 주소에는 10.0.2.100을, 포트에는 3128을 입력한다. \<저장\>을 눌러 저장하고 [설정]창을 닫는다.


> 인터넷 익스플로러를 사용하는 환경이라면, 인터넷 익스플로러를 실행한 후 [도구] 아이콘이나 메뉴의 [도구] → [인터넷 옵션]을 선택하고 [연결] 탭을 클릭한다. 그리고 <LAN 설정>을 클릭한 다음 [프록시 서버] 항목에서 [사용자 LAN에 프록시 서버~~]의 체크를 켜고 [주소]에는 10.0.2.100을, [포트]에는 3128을 입력해 프록시서버를 설정한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/14%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%94%84%EB%A1%9D%EC%8B%9C%20%EC%84%9C%EB%B2%84/images/image11.png)

- 이제 Client에서와 마찬가지로 Edge 브라우저로 웹 서핑을 하면 프록시를 거친 상태 작동한다.

- 이것으로 Squid 프록시 서버의 구축과 테스트를 완료했다. 일반적으로 규모가 큰 회사라면 대부분 업무상 동일한 웹 사이트에 접속하는 경우가 많으므로 상당한 효과를 볼 수 있을 것이다. 물론 트래픽이 높다면 프록시 서버도 성능이 좋은 하드웨어를 준비해야 하며, squid.conf 파일도 각 회사의 상황에 맞게 적절히 수정해서 사용해야 효과를 극대화할 수 있다.

