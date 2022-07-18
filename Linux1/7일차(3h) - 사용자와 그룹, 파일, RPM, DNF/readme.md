# 사용자와 그룹
- 리눅스는 다중 사용자 시스템(multi-user system)이다. 즉 1대의 리눅스에 사용자 여러 명이 동시에 접속해서 사용할 수 있는 시스템이다. 
- 리눅스를 설치하면 기본적으로 root라는 이름을 가진 수퍼 유저superuser가 있다. 이 root 사용자는 시스템의 모든 작업을 실행할 수 있는 권한이 있다. 또한 시스템에 접속할 수 있는 사용자를 생성할 수 있는 권한도 있다.

- 그런데 모든 사용자는 혼자서 존재하는 것이 아니라 하나 이상의 그룹에 소속되어 있어야 한다. 예를 들면 회사에서 '홍길동'이라는 직원이 '전산실'과 같은 어느 부서에 소속된 것과 같다고 생각할 수있다.

- 우선 gedit이나 vi 에디터로 "/etc/passwd" 파일을 열면 다음과 같이 된다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image1.png)

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image2.png)


- 여러 명의 사용자가 보일 것이다. 제일 위의 root 사용자부터 제일 아래의 바로 위인 tcpdump 사용자까지는 리눅스에서 기본적으로 존재하는 표준 사용자다.

- 지금은 제일 위에 있는 root 사용자와 제일 아래 부분의 설치 직후 생성된 centos 사용자를 보고 의미를 파악해보자.

- 각 행의 의미는 다음과 같다.

```
사용자 이름:암호:사용자 ID:사용자가 소속된 그룹 ID:전체 이름:홈 디렉터리:기본 셸
```

- 제일 아래의 centos 사용자를 살펴보면, 사용자 이름은 centos 암호가 x로 표시되는데 이는 "/etc/shadow" 파일에 비밀번호가 지정되어 있다는 의미다. 그리고 centos의 사용자 id는 1000번이고, centos가 속한 그룹의 id는 1000번이다. 전체 이름도 centos로 사용하며 centos 사용자의 홈 디렉터리는 "/home/centos"이고 로그인 시 제공되는 셸은 /bin/bash다
- root 사용자의 행을 살펴보면 사용자 id와 그룹 id가 0번으로 설정되어 있음을 확인할 수 있다. 이번에는 "/etc/group" 파일을 확인해보자.


![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image3.png)

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image4.png)

- 각 행의 의미는 다음과 같다.

```
그룹이름:비밀번호:그룹 id:그룹에 속한 사용자 이름
```

- 마지막 '그룹에 속한 사용자 이름은 참조로 사용된다. 즉 해당 부분에 아무것도 써 있지 않다고 해서 그룹에 소속된 사용자가 반드시 없다는 뜻은 아니다. 필자의 경우에도 제일 첫 행 root 그룹에는 실제로 root 사용자가 속해 있으나 여기에는 표현되어 있지 않다. 
- 앞서 살펴본 "/etc/passwd" 파일에서는 centos 사용자가 속한 그룹이 1000번으로 표현되었다. 즉 "/etc/group" 파일에서도 centos 그룹의 ID가 1000번이므로 centos 그룹에는 centos 사용자가 속해 있는 것이다. 
- 사용자 및 그룹과 관련된 명령어는 다음과 같은 것들이 있다. 

#### useradd(또는 addUser)

- 새로운 사용자를 추가해준다. 
- 이 명령을 실행하면 "/etc/passwd", "/etc/shadow", "/etc/group" 또는 파일에 새로운 행이 추가된다.
- 사용 예

```
# useradd newuser      -> newuser라는 이름의 사용자 생성
# useradd -u 1111 newuser     -> newuser 사용자를 생성하면서 사용자 ID를 1111로 지정
# useradd -g mygroup newuser     -> newuser 사용자를 생성하면서 mygroup 그룹에 newuser 사용자를 포함시킴(mygroup 그룹을 먼저 만들어놓아야 함)
# useradd -d /newhome newuser     -> newuser 사용자를 생성하면서 홈 디렉토리를 /newhome으로 지정
# useradd -s /bin/csh newuser 사용자를 생성하면서 기본 셀을 /bin/csh로 지정
```

#### passwd

- 사용자의 비밀번호를 지정하거나 변경한다.
- 사용 예 

```
# passwd newuser      -> newuser 사용자의 비밀번호 지정(또는 변경)
```


#### usermod 

- 사용자의 속성을 변경한다. 옵션은 useradd와 동일하다.
- 사용 예

```
# usermod -g root newuser    -> newuser 사용자의 그룹을 root 그룹으로 변경
```

#### userdel
-  사용자를 삭제한다.
- 사용 예 

```
# userdel newuser     -> newuser 사용자 삭제
# userdel -r newuser   -> newuser 사용자를 삭제하면서 홈 디렉토리까지 삭제
```

#### chage 

- 사용자의 암호를 주기적으로 변경하도록 설정한다.
- 사용 예

```
# chage -l newuser           -> newuser 사용자에 설정된 사항 확인
# chage -m 2 newuser       -> newuser 사용자에 설정한 암호를 사용해야 하는 최소 일자(즉, 변경 후 최소 2일은 사용해야 함)
# chage -M 30                 -> newuser 사용자에 설정한 암호를 사용할 수 있는 최대 일자(즉, 변경 후 최대 30일까지 사용할 수 있음)
# chage -E 2026/12/12 newuser      -> newuser 사용자에 설정한 암호가 만료되는 날짜(즉, 2026/12/12까지만 사용할 수 있음)
# chage -W 19 newuser          -> newuser 사용자에 설정한 암호가 만료되기 전에 경고하는 기간. 지정하지 않을 경우 기본값은 7일(즉, 이와 같이 설정하면 암호가 만료되기 10일 전부터 경고 메시지가 나감)
```

#### groups

- 사용자가 소속된 그룹을 보여준다.
- 사용 예

```
# groups     -> 현재 사용자가 소속된 그룹을 보여줌
# group newuser     -> newuser가 소속된 그룹을 보여줌
```

#### groupadd

- 새로운 그룹을 생성한다.
- 사용 예

```
#groupadd newgroup     -> newgroup이라는 그룹을 생성
#groupadd -g 2222 newgroup    -> newgroup이라는 그룹을 생성하면서 그룹 ID를 2222로 지정
```

#### groupmod

- 그룹의 속성을 변경한다.
- 사용 예

```
# groupmod -n mygroup newgroup   -> newgroup 그룹의 이름을  mygroup으로 변경
```

#### groupdel

- 그룹을 삭제한다.
- 사용 예

```
# groupdel newgroup    -> newgroup 그룹 삭제(단, 해당 그룹을 주요 그룹으로 지정한 사용자가 없어야 함)
```

> 사용자는 주요 그룹 1개와 보조 그룹 여러 개에 가입할 수 있다. 일례로 useradd -g main -G sub user 명령은 user1을 생성하면서 main 그룹을 주요 그룹으로, sub 그룹을 보조 그룹으로 가입시킨다.


#### gpasswd

- 그룹의 암호를 설정하거나 그룹 관리를 수행한다.
- 사용 예

```
# gpasswd newgroup    -> newgroup 그룹의 암호 저장
# gpasswd -A newuser newgroup    -> newuser 사용자를 newgroup 그룹의 관리자로 지정
# gpasswd -a user1 newgroup        -> user1을 newgroup 그룹의 사용자로 추가
# gpasswd -d newuser newgroup    -> user1을 newgroup 그룹의 사용자에서 제거
```

## 실습1

### step 0
Server를 처음 설치 상태로 초기화하자

- root 사용자로 접속한다. 
- 바탕 화면의 왼쪽 위 [현재 활동] →[터미널] 을 선택해서 터미널을 연다.

### step 1

새로운 사용자를 만들어보자 (사용자 생성 작업은 root 사용자만 할 수 있다).

- useradd user1 명령을 입력해 user1 사용자를 만들자.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image5.png)

- "tail /etc/passwd" 명령을 입력해 user1 사용자가 추가되었는지 확인한다(tail은 파일의 마지막 10행을 보여주는 명령이다).
	- 제일 마지막 행에 사용자가 추가된 것이 보인다. 사용자 이름은 앞에서 지정한 user1으로 되어 있다. 그리고 암호는 "/etc/shadow" 파일에 지정되어 있다. 3번째 열에서 user1의 ID는 1001 번으로 되어 있는데, 이는 그 앞에 있는 centos의 1000번 다음에 자동으로 1을 더해서 할당된 것이다. 그룹 ID도 1001번으로 지정되어 있다. 
	- 여기서 주의할 점은 그룹 이름이 아닌 그룹 ID가 지정되어 있다는 점이다. 왜 그런지는 잠시 후 다시 살펴보겠다. 사용자의 홈 디렉터리는 기본 설정인 '/home/사용자이름으로 지정되었고, 셸은 기본 설정인 "/bin/bash"로 지정되었다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image6.png)	
	

- user 사용자는 그룹을 별도로 지정하지 않았다. 우선 "tail -5 /etc/group" 명령을 입력해 그룹을 확인해보자.
	- 제일 마지막 행에 그룹이 추가되었다. 그룹 이름을 보니 사용자 이름과 동일한 user 으로 되어 있으며, 그룹 ID는 자동으로 마지막 그룹 번호인 1000에서 1이 증가한 1001로 생성되었다.
	- 결론적으로 useradd 명령을 실행해 별도의 그룹을 지정하지 않으면, 자동으로 사용자 이름과 동일한 그룹이 생성되고 새로운 사용자는 생성된 그룹에 자동으로 포함된다. 즉 새로 생성된 그룹(여기서는 user1)은 소속된 사용자가 1명인그룹이 된다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image7.png)	

- 많은 사용자를 관리할 때 지금과 같은 방식으로 관리하면 '사용자 이름 = 그룹 이름'이 되어 관리하기불편하다(직원 이름이 '홍길동'인데 직원의 부서 이름도 '홍길동'이면 좀 이상하다). <b>그래서 사용자를 관리할경우 먼저 그룹을 만들고 사용자를 만든 그룹에 속하도록 생성하는 것이 바람직하다.</b>

#### step 2

그룹을 별도로 생성하고 해당 그룹에 다수의 사용자를 포함시켜 관리해보자.

- 먼저 user 사용자를 삭제한다. 그리고 centosGroup 그룹을 먼저 만든다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image8.png)	

- 새로운 user1, user2 사용자를 만들면서 그룹을 centosGroup 그룹으로 지정해준다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image9.png)	

- "/etc/passwd" 파일을 확인해보니 그룹 ID가 모두 1001로 되어 있다. "/etc/group" 파일에서 1001번은centosGroup임을 알 수 있다.

- "/etc/shadow" 파일을 확인해보면 제일 아래에 user1, user2라는 두 사용자가 추가되었음을 알 수 있다. 그런데 centos의 경우 암호가 코드화되어 들어 있지만, user1 user2는 해당 부분에 '!!'라는 표시만되어 있다. 이는 아직 암호가 지정되어 있지 않다는 의미다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image10.png)	

- user1 사용자와 user2 사용자의 암호를 지정하자. 둘 다 간단하게 '1234'로 입력한다.

> 간단한 암호 입력 시 경고는 나오지만, root 사용자가 암호를 지정해줄 경우에는 간단한 암호도 지정할 수 있다. 단, 일반 사용자가 자신의 암호를 변경할 때는 간단한 암호가 아닌 8글자 이상으로 영어 사전에 등록되지 않은 단어를 사용해야 한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image11.png)	


- 다시 /etc/shadow 파일을 확인하면 user1과 user2 사용자에 암호가 지정된 것을 알 수 있다. 그런데 재미있는 점은 앞서 두 사용자의 암호를 모두 '1234'로 입력했으나 코드화된 암호는 서로 다르다는것이다. 이는 "/etc/shadow" 파일을 살펴보더라도 암호를 알 수 없다는 것을 의미한다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image12.png)	

- 이번에는 userl 사용자의 홈 디렉터리인 "/home/user1"과 "/etc/skel" 디렉터리를 비교해보자. 두 디렉터리에 동일한 파일이 들어 있을 것이다. 즉 새로운 사용자를 생성하면 해당 사용자의 홈 디렉터리 기본 설정은 '/home/사용자이름'으로 지정되며, "/etc/skel" 디렉터리의 모든 내용을 사용자의 홈 디렉터리에 복사하는 작업이 발생한다. 그러므로 앞으로 생성하는 사용자에게 특정한 파일 등을 배포하고 싶은 경우 "/etc/skel" 디렉터리에 넣어두면 된다.

> 이름에서 예측할 수 있듯이 '/skel' 디렉터리는 skeleton (뼈대)의 약자다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image13.png)	


#### step 3
- 연습한 사용자 및 그룹을 삭제한다.

```
# userdel -r user1
# userdel -r user2
groupdel centosGroup
```

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image14.png)	

# 파일과 디렉토리의 소유권과 허가권

- 리눅스는 각각의 파일과 디렉터리마다 소유권과 허가권이라는 속성이 있다. root 사용자가 자신의 홈 디렉터리에서 <b>touch sample.txt</b> 명령을 실행해 빈 파일을 만들고 <b>Is -I</b> 명령을 실행하면 다음과 같이 나타날 것이다.

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image15.png)	


- 방금 생성한 sample.txt 파일 정보를 다음과 같이 간략히 나타냈다.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image16.png)	


- 표시된 정보의 의미를 각 항목별로 확인해보자.

### 파일 유형

- 파일이 어떤 종류인지 나타낸다. 디렉터리인 경우 'd'가 일반적인 파일인 경우 '-'가 표시된다. 그 외에 b(블록 디바이스), c(문자 디바이스), |(링크) 등이 있다.


> 'b'나'c'는 디바이스(장치)를 뜻한다. <b>Is -I /dev | more</b> 명령을 실행해서 확인해보면 b나 c가 많이 보일 것이다. b는 블록디바이스(Block Device)를 의미하며 대표적인 것으로 하드디스크 플로피 디스크 CD/DVD 등의 저장장치가 있다. c는 문자 디비이스(Character Device)를 의미하며 대표적인 것으로 마우스, 키보드 프린터 등의 입출력장치가 있다. 또 |은 링크(Link)를 뜻한다. 링크란 Windows의 '바로가기 아이콘'과 비슷한 개념으로 연결된 파일을 의미한다. 이때 실제 파일은 다른 곳에 존재한다는 것을 기억하자.

### 파일 허가권

- 파일 허가권(pemission)은 rw-, r--, r-- 3개씩 끊어서 인식하면 된다. r은 read, w는 write, x는 execute의 약자다. 즉 rw-는 읽거나 쓸 수 있지만 실행할 수는 없다는 의미며 rwx로 표시되면 읽고, 쓰고, 실행이 가능한 파일이라는 의미다.

- 또한 첫 번째 rw-는 소유자(user)의 파일 접근 권한을 두 번째 r--는 그룹(group)의 파일 접근 권한을, 세 번째 r--는 그 외 사용자(other)의 파일 접근 권한을 의미한다. 풀어서 얘기하면 sample.txt 파일의 소유자는 읽거나 쓸 수 있고 그룹은 읽을 수만 있으며 그 외 사용자도 읽을 수만 있도록 허가되어 있다는 의미다.

- sample.txt 파일의 허가권을 다음과 같이 숫자로도 표현할 수 있다.

<table>
	<thead>
		<tr>
			<th colspan='3'>소유자(User)</th>
			<th colspan='3'>그룹(Group)</th>
			<th colspan='3'>그 외 사용자(Other)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>r</td>
			<td>w</td>
			<td>-</td>
			<td>r</td>
			<td>-</td>
			<td>-</td>
			<td>r</td>
			<td>-</td>
			<td>-</td>
		</tr>
		<tr>
			<td>4</td>
			<td>2</td>
			<td>0</td>
			<td>4</td>
			<td>0</td>
			<td>0</td>
			<td>4</td>
			<td>0</td>
			<td>0</td>
		</tr>
		<tr>
			<td colspan='3'>6</td>
			<td colspan='3'>4</td>
			<td colspan='3'>4</td>	
		</tr>
	</tbody>
</table>

- 소유자의 허가권인 이라는 숫자는 2진수 110 이므로 rw-로 표현할 수 있고, 그룹의 허가권인 4 라는 숫자는 2진수 100이므로 r--로, 그 외 사용자의 허가권인 4 라는 숫자도 2진수로 100이므로 r--로 표현되는 것이다. 몇 가지 예를 들면, 파일 허가권이 754 라는 것은 rwxr-xr--가 되므로 소유자는 읽고/쓰고/실행할 수 있고, 그룹은 읽고/실행할 수만 있으며 그 외 사용자는 읽을 수만 있다는 것을 의미한다. 참고로 <b>디렉터리 (=폴더)의 경우 해당 디렉터리로 이동하려면 반드시 실행 (x)권한이 있어야 한다. 그래서 디렉터리는 일반적으로 소유자/그룹/기타 사용자 모두에게 실행 (x) 권한이 설정되어 있을 것이다.</b>

#### 파일 확장명

- Windows의 경우 \*.exe는 실행 파일, \*.txt는 텍스트 파일 등과 같이 확장명으로 해당 파일의 종류를 판단하지만, <b>리눅스는 확장자에 별 의미를 두지 않는다.</b> 즉 실행 파일이든 텍스트 파일이든 모두 일반적으로 확장명을 갖지 않으며, 확장명을 갖더라도 편리함을 위해서일 뿐 확장명이 파일의 종류를 판단하는 절대적인 의미는 아니다. 그래서 해당 파일이 어떤 파일인지 알려면 file 명령을 사용해야 한다.

- 파일의 허가권을 변경하는 명령어로 chmod 명령이 있다. 이 명령어는 root 사용자 또는 해당 파일의 소유자만 실행할 수 있다. 일례로 <b>chmod 777 sample.txt</b> 명령을 실행하면 sample.txt 파일은 모든 사용자가 읽고 쓰고, 실행할 수 있는 파일이 된다.

> 파일의 허가권을 실행할 수 있도록 설정되어 있어도, 파일이 실제로 실행 가능한 코드가 아니라면 실행 시 오류가 발생할 것이다. Windows에서 그림 파일인 mypic.jpg 파일을 실행 파일인 mypic.exe로 확장명을 변경할 수 있지만, mypic.exe가 실제로 실행되지 않는 것과 같은 이치다.

- chmod 명령을 상대 모드(symbolic method)로도 사용할 수 있다. <b>chmod u+x 파일이름</b> 명령은 '소유자(User)에게 실행(execute) 권한을 허가하라 (+)'는 의미다. 몇 가지 예를 들면, u-wx는 사용자에게 쓰기와 실행 권한을 제거하라는 의미며, g+rx는 그룹에게 읽기와 실행 권한을 허가하라는 의미고, o+rwx는 그 외 사용자에게 읽기/쓰기/실행 권한을 허가하라는 의미다.


### 파일 소유권

- 파일 소유권(ownership)은 파일을 소유한 사용자와 그룹을 의미한다. sample.txt 파일은 root라는 이름의 사용자가 소유자며, 그룹도 root로 되어 있다. 파일의 소유권을 바꾸는 명령어는 chown이다. 사용법은 <b>chown 새로운사용자이름(.새로운그룹이름) 파일이름</b> 명령의 형식으로 사용하면 된다. 예를 들어 <b>chown centos sample.txt</b> 명령은 sample.txt 파일의 소유자를 centos 사용자로 바꾸라는 의미고, <b>chown centos.centos sample.txt</b> 명령은 파일의 그룹도 centos 그룹으로 바꾸라는 의미다. 또한 <b>chgrp centos sample.txt</b> 명령은 그룹만 centos 그룹으로 변경하라는 의미다.


## 실습2

파일의 허가권 및 소유권을 확실히 이해하자.

### step 0

Server를 실행해 root 사용자로 접속한다.

- 터미널을 열고 연습용 파일을 하나 생성하자. <b>vi test</b> 명령을 입력한 후 "I" 또는 "A"를 눌러 다음 내용을 쓴 다음 ':wq'를 입력해 내용을 저장하고 vi 에디터를 종료한다. 아직 vi 에디터에 익숙하지 않다면 gedit test 명령을 입력해 gedit을 사용해도 관계없다 (한/영 전환은 [shift] + Space bar)다).



```
안녕하세요? 그냥 연습 파일입니다.
ls /car
```

- Is -I test 명령를 입력해 파일의 속성을 확인하자.

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image17.png)	

- 이 파일은 허가권이 rw-r--r--로 설정되어 있고 소유자는 root 사용자이며 그룹은 root 그룹으로 되어있다. 즉 root 사용자는 이 파일을 rw- (읽고, 쓰고) 할 수 있고 x (실행) 할 수 없다. 또 root 그룹 및 그 외 사용자는 r-- (읽기)만 가능하다.

### step 1

파일의 속성을 변경해보자.

- test 파일을 실행한다. 

```
whoami   -> 현재 사용자가 누구인지 알려줌
./test       -> 현재 디렉토리의 test 파일 실행('./'는 현재 디렉토리에 있는 파일을 의미함)
```

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image18.png)	

- 허가가 거부되었다는 메시지가 나왔다. 현재 사용자인 root의 실행 권한이 rw--이므로 실행할 수 없기 때문이다.

- 이 파일을 실행할 수 있도록 rwxr-xr-x (755)로 변경하기 위해 <b>chmod 755 test</b> 명령을 입력한다. 그리고 <b>Is -I test</b> 명령을 입력해 test 파일의 변경 사항이 있는지 확인한다. 마지막으로 <b>./test</b> 명령을 입력해 다시 파일을 실행해본다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image19.png)	

- 일단 실행이 되었다. 하지만 첫 번쨰 행인 '안녕하세요~~'는 명령이 아니고 오류가 발생했고, 두 번째 행인 'ls /var'은 실행되어 /var 디렉토리의 내용이 출력되었다. 이렇듯 실행 코드가 없는 파일을 실행되도록 변경하는 것은 주의해야 한다.

### step 2

이번에는 소유권을 변경해보자.

- 먼저 <b>chown centos test</b> 명령을 입력해 test 파일의 소유권을 centos 사용자로 변경한다.

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image20.png)	

- <b>chgrp centos test</b> 명령을 입력해 그룹도 centos 그룹으로 변경한다.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image21.png)	

- 사용자와 그룹을 한꺼번에 바꾸려면 <b>chown centos.centos test</b> 또는 <b>chown centos:centos test</b> 명령을 입력한다.

- 이제는 centos 사용자로 접속한 후 test 파일의 속성을 모두 읽기/쓰기/실행(777)할 수 있도록 변경한다.

```
su - centos    -> centos 사용자로 접속(root)가 접속할 경우 암호를 물어보지 않음)
pwd             -> 현재 디렉토리의 확인. 사용자 홈 디렉토리가 나올 것임
ls -l /root/test
ls -ld /root    -> /root 디렉토리의 속성 확인
```

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image22.png)

- 그런데 앞에서 test 파일의 소유권을 centos에게 확실히 넘겨줬는데도 centos 사용자는 "/root/test" 디렉터리 접근이 거부되었다. 그 이유는 "/root" 디렉터리의 속성이 r-xr-x---로 되어 있기 때문이다. 마지막 '---'가 기타 사용자의 허가권인데, 아무런 읽기/쓰기/실행 권한이 허가되지 않았으므로 centos 사용자는 '/root' 디렉터리의 접근이 거부된 것이다. 그래서 '/root' 디렉터리 안에 있는 test 파일의 소유가 centos 사용자에게 있더라도 사용할 수 없다.

- 우선 다시 root 사용자로 test 파일을 "/home/centos" 디렉터리로 옮긴 후 다시 허가권을 변경한다.

```
exit       -> 다시 원래 접속한 사용자(이 경우에는 root)로 돌아감
mv test -centos    -> -centos는 centos 사용자의 홈 디렉토리(/home/centos와 동일)
su - centos
ls -l test
chmod 777 test
ls -l test
```

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image23.png)

- 별 이상 없이 잘 실행되었다.


- 이번에는 <b>chown root.root test</b> 명령을 입력해 test의 소유권을 다시 root 사용자에게 돌려준다.

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image24.png)

- 그런데 명령을 허용하지 않는다는 메시지가 나온다. 정상적인 상황이다. 만약 이 test 파일이 심각한 바이러스 파일이고 지금 명령이 실행되었다면 centos 사용자가 마음대로 root 사용자에게 바이러스 파일을 전달하게 되는 것이다. 그러므로 <b>파일의 소유권을 바꾸는 chown 명령은 root 사용자만 실행할 수 있다.</b> 

- exit 명령을 입력해 다시 root 사용자로 돌아온다.

### 링크

- 파일의 링크(Link)는 <b>하드 링크 Hard Link와 심볼릭 링크(symbolic Link)</b> 2가지가 있다. 아래 그림을 보면, 원본 파일이 inode1을 사용할 때 하드 링크를 생성하면 '하드 링크 파일'만 하나 생성되며 같은 inode1을 사용하게 된다. 하드 링크를 생성하려면 <b>In 링크대상파일이름 링크파일이름</b> 명령을 실행한다.

#### inode

- <b>inode</b>는 리눅스/유닉스의 파일 시스템에서 사용하는 자료구조를 말하는데, <b>파일이나 디렉터리의 여러 가지 정보</b>가 있다. 모든 파일이나 디렉터리는 각자 1개씩의 inode가 있으며 <b>각 inode에는 해당 파일의 소유권 허기권, 파일 종류 등의 정보와 해당 파일의 실제 데이터 위치(주소)도 있다.</b> 이러한 inode가 모여 있는 공간이 <b>inode 블록</b>이며 일반적으로 전체 디스크 공간의 1% 정도 차지한다. <b>Data 블록은 실제 데이터가 저장된 디스크 공간</b>으로 전체 디스크의 대부분을 차지한다.

- <b>원본 파일에 심볼릭 링크를 생성하면 새로운 inode2를 만들고, 데이터는 원본 파일과 연결되는 효과를 갖는다.</b> 일반적으로 사용자는 주로 심볼릭 링크를 사용하며, Windows의 바로 가기 아이콘도 심볼릭 링크에 해당된다. 심볼릭 링크를 생성하려면 <b>In -s 링크대상파일이름 링크파일이름</b> 명령을 실행한다. 개념이 잘 이해되지 않는다면 실습을 통해 이해해보자.

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image25.png)

#### 하드 링크와 심볼릭 링크의 비교


## 실습3

하드 링크와 심볼릭 링크를 생성해보자. 위 그림을 참고하면서 진행한다. 

### step 0

- Server를 실행하자.

### step 1

- "/root/linktest" 디렉터리를 만들고 그 안에 basefile이란 파일을 만들자. 그리고 vi 에디터나 gedit을 이용해 “파일 링크를 실습하기 위한 원본 파일입니다."를 입력하고 저장한 후 cat 명령을 사용해 파일 내용을 확인하자.

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image26.png)

### step 2

하드 링크와 심볼릭 링크를 확인해보자.

-  In 명령어와 옵션을 조합해 하드 링크 및 심볼릭 링크 파일을 만들자

```
ln basefile hardfile   -> 하드 링크 생성
ln -s basefile softlink  -> 심볼릭 링크(=소프트 링크) 생성
ls -il  -> -il 옵션은 inode 번호를 제일 앞에 출력
cat hardlink   -> 하드 링크의 내용 확인
cat softlink    -> 소프트 링크의 내용 확인
```

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image27.png)

- 앞에 나온 그림 보면서 결과 창을 확인하자. 
- 원본 파일(basefile)은 inode가 inode1(35462204번)으로 지정되어 있다. 그리고 하드 링크 파일(hardlink)도 그림과 마찬가지로 inode1(35462204번)으로 지정되어 있다. 
- 그러나 심볼릭 링크 파일(softlink)은 inode2(35462203번)로 다르게 지정되어 있다. 
- 원본 파일(basefile)과 하드 링크 파일(hardlink)은 Data 블록에 같은 원본 파일 데이터를 사용하므로 크기가 61바이트로 동일하며, 심볼릭 링크 파일(softlink)은 별도의 원본 파일 포인터를 갖기 때문에 8바이트로 크기가 다르다.
	
- 파일 이름에서도 심볼릭 링크 파일 (softlink)은 원본 파일 (basefile)을 지정한다는 의미로 화살표(→)가 표시되어 있다.
	
- 원본 파일 (basefile)을 다른 곳으로 이동시키고 하드 링크 파일(hardlink)과 심볼릭 링크 파일(softlink)을 확인해보자.

```
mv basefile ../     -> basefile을 앞 디렉토리(..)로 이동
ls -il
 car hardlink
 cat softlink
```

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image28.png)


- 결과를 보면 하드링크는 디렉토리 원본 파일이 없어져도 아무 이상이 없고, 심볼릭 링크는 디렉토리에서 원본파일이 없어지면 연결이 끊어진다.

- 원본 파일을 현재 디렉토리로 가져와서 다시 한 번 확인해보면 심볼릭 링크가 원상태로 복구되었음을 확인할 수 있다.

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image29.png)


# 리눅스 관리자를 위한 명령어
 
## 프로그램 설치를 위한 RPM

- CentOS에서 패키지 (프로그램 모음 또는 꾸러미)를 설치하는 데 가장 많이 사용되는 것은 RPM과 DNF(또는 YUM)다. 
- DNF(또는 YUM)이 나오기 전에는 주로 RPM(Redhat Package Manager)이 사용되었으나, DNF는 RPM의 개념과 기능을 포함하기 때문에 최신 버전 CentOS에서는 DNF를 사용하면 된다.
- 그러나 <b>DNF가 별도로 존재한다기보다 RPM을 포함한 확장 개념에 가까우므로 먼저 RPM의 개념을 익혀야 한다.</b>

### RPM

- 초창기 리눅스의 경우 새로운 프로그램을 설치하기가 꽤 어려웠기 때문에, 초보자에게는 프로그램을 설치하는 것조차 하나의 난제였다.  
- 이 점을 개선하여 레드햇(RedHat)사에서 Windows의 setup.exe와 같이 프로그램 설치 후 바로 실행할 수 있는 설치 파일을 제작했다.
- 설치 파일의 확장명은 \*.rpm이며 이를 '패키지(package)'라고 부른다.

### 파일의 의미
- CentOS-Stream8 DVD ISO 파일을 연결하면 자동으로 마운트 되는 폴더 "/run/media/root/CentOS-Stream-8-x86_64/BaseOS/Packages/"에는 많은 rpm 파일이 존재한다. 그 중 압축 프로그램인 gzip에 대해 살펴보자.

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image30.png)

- 우선 rpm 파일의 형식은 일반적으로 다음과 같다(패키지에 따라 형식이 좀 다를 수 있다).

```
패키지이름-버전-릴리즈번호.CentOS버전.아키텍쳐.rpm
```

- CentOS8 DVD에 포함된 gzip은 다음과 같다.
	- 패키지 이름: gzip  -> 패키지(프로그램)의 이름이다.
		- 패키지 이름은 gzip처럼 단순할 수도 있고, 하이픈(-)으로 연결되어 긴 이름으로 존재할 수도 있다. 예를 들어 main-pages-4.15-6.el8.x86_64.rpm 패키지 파일의 패키지 이름은 main-pages까지다. 즉, 버전 바로 앞까지가 패키지 이름이다.
		
	- 버전: 1.9   -> 대부분 2자리 또는 3자리 수로 구성된다. 주 버전, 부버전, 패치 버전 순서며, 당연히 숫자가 높을 수록 최신이다.
	- 릴리즈 번호 : 13  -> 문제점을 개선할 때마다 붙여지는 번호다.
	- CentOS 버전 : el8  -> CentOS 8에서 배포할 경우 붙여진다. el8은 Redhat Enterprise Linux 8을 의미한다.
	
		- el8은 Redhat Enterprise Linux 8 또는 CentOS 8용을 의미하지만, 꼭 CentOS 8에만 설치할 수 있는 것은 아니며 일반적으로 다른 버전의 CentOS나 다른 리눅스에도 설치할 수 있다.
		
	- 아키텍처: x86_64 -> x86 계열의 64bit CPU를 의미한다. 즉, 이 파일을 설치할 수 있는 CPU를 뜻한다.
		- 아키텍처 부분에 올 수 있는 것은 다음과 같다. 강의에서는 x86_64 또는 noarch용을 사용한다.
		- i386, i486, i586, i686 : 인텔 또는 AMD 계열의 32bit CPU  -> 구형 CPU
		- x86_64 : 인텔 또는 AMD 계열의 64bit CPU    -> 가장 보편적으로 사용되는 CPU
		- alpha/sparc/ia64: 미국 DEC사의 알파 (ALPHA) 프로세서 썬 마이크로 시스템즈의 스팍(SPARC) 프로세서, 인텔의 아이테니엄(Itanium) 프로세서로 모두 CPU 명령어의 개수를 줄여 하드웨어 구조를 좀 더 간단하게 만드는 RISC (Reduced Instruction Set Computer) 설계 방식 CPU를 의미한다.   -> 잘 사용하지 않음.
		- src : 소스 파일 패키지 설치 후에는 컴파일을 별도로 해줘야 한다.
		- noarch : 모든 CPU에 설치 가능하다(NO ARCHitecture).
			
### 자주 사용하는 rpm 명령어 옵션

#### 설치

```
rpm -Uvh 패키지파일이름.rpm
```

- U (대문자)  -> 기존에 패키지가 설치되지 않았다면 일반적인 설치를 진행하고, 패키지가 설치되어있다면 업그레이드한다(설치되어 있을 경우 i 옵션은 오류가 발생하므로 U 옵션이더 편하다).
- v   -> 설치 과정 확인
- h   -> 설치 진행 과정을 #기호로 화면에 출력

#### 삭제

```
rpm -e 패키지이름 
```
- e  -> erase (지움)의 약자

#### 이미 설치된 패키지 조회

- rpm -qa 패키지이름   -> 시스템에 패키지가 설치되어 있는지 확인
- rpm -qf 파일의 절대경로 -> 이미 설치된 파일이 어느 패키지에 포함된 것인지 확인
- rpm -ql 패키지이름  -> 특정 패키지에 어떤 파일이 포함되었는지 확인
- rpm -qi 패키지이름  -> 설치된 패키지의 상세 정보

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image31.png)

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image32.png)


- CentOS에서는 설치 시 RPM보다 더 편리한 DNF를 제공하므로 RPM을 사용할 일이 많이 줄었지만, 이미 설치된 패키지 정보를 보는 데는 앞에 나온 4가지 질의 옵션을 자주 사용한다. 잘 기억해놓

#### 아직 설치되지 않은 rpm 파일 조회

- rpm -qlp 패키지파일이름.rpm   -> 패키지 파일에 어떤 파일들이 포함되었는지 확인 
- rpm -qip 패키지파일이름.rpm   -> 패키지 파일의 상세 정보

> 특히 <b>rpm -qip 패키지파일이름.rpm</b> 명령은 패키지를 설치하기 전, rpm 파일 안에 해당 기능이 포함되었는지 미리 확인하는 데 유용하게 사용할 수 있다.

### RPM의 단점

- 예전 리눅스의 프로그램 설치보다는 획기적으로 편리해졌지만, rpm 명령어 역시 단점이 있다. 
- 가장 큰 문제점은 '의존성'이다. 간단한 예로 CentOS의 기본 웹 브라우저인 Firefox는 당연히 X 윈도상에서 가동된다. 그런데, X 윈도가 설치되지 않은 상태에서 Firefox를 설치한다면? Firefox는 X 윈도에 의존성이 있으므로 설치가 되지 않을 것이다.

- 이러한 불편을 해결한 것이 dnf 명령이다. dnf 명령은 잠시 후에 알아보고, 이번에는 rpm 명령으로 프로그램을 설치하는 실습을 진행하자.

### 실습4
- rpm 패키지를 이용해서 프로그램을 설치해본다.

#### step0

- Server를 실행하자.

#### step 1

DVD에 있는 간단한 rpm 패키지를 설치하자 (DVD가 마운트되어 있지 않다면 마운트 한다).

- 터미널을 연다. 명령어를 편리하게 사용할 수 있는 mc 패키지를 설치할 계획이다. rpm -qi mc 명령으로 이미 설치되어 있는지 확인하고, 설치되어 있지 않다면 <b>"cd /run/media/root/Ce[Tab]/App[Tab]/Pac[Tab]/"</b> 명령을 입력해 해당 rpm 패키지가 있는 디렉터리로 이동한 후 "<b>rpm -qip mc-[Tab]</b>" 명령을 입력해 해당 rpm 파일에 기능이 포함되어 있는지 미리 확인한다.

> DVD에는 주로 기본 설치 패키지가 들어 있는 BaseOS 폴더와 주로 X 윈도 응용 프로그램 등의 추가 설치 패키지가 들어있는 AppStream 폴더로 구분되어 있다.

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image33.png)

- mc 패키지를 <b>rpm -Uvh mc-[Tab]</b> 명령을 입력해 설치해보자.

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image34.png)

- <b>rpm -qi mc</b> 명령을 입력해 설치한 패키지의 정보를 확인한다.

![image35](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image35.png)

- 그 외에도 <b>rpm -ql mc</b> 명령을 입력하면 이 mc 패키지와 관련된 파일의 목록을 보여준다.

- 터미널에서 <b>mc</b> 명령을 입력하면 실행된다. 마우스를 사용해서 파일을 선택할 수도 있다. <b>exit</b> 명령을 입력하면 mc가 종료된다.

![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image36.png)

- 이제 mc 패키지를 제거하자 패키지를 제기할 때는 배기지 파일이 필요 없다. 즉 /rum/media/root/CentOS-Stream-8-x86_64/AppStream/Packages/ 디렉터리가 아닌 다른 아무 디렉터리에서 제기해도 된다.

- <b>rpm -e mc</b> 명령을 입력하면 된다. 즉 pm 파일 이름이 아닌 패키지 이름만 쓰면 된다.

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image37.png)

- 성공적으로 제거되면 아무 메시지도 나오지 않는다.

#### step2

의존성 문제가 있는 rpm 파일을 설치해보자.

- mysql-errmsg 패키지를 설치해보자 (패키지의 기능은 중요하지 않다). 패키지를 설치하기 위해 <b>rpm-Uvh mysql-err[Tab]</b> 명령을 입력하자. 하지만 의존성 문제로 설치되지 않을 것이다. 즉 mysql-errmsg패키지가 설치되려면 관련 있는 다른 패키지를 먼저 설치해야 한다.

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image38.png)

- <b>의존성 문제를 해결하기 위해 메시지에 특정 파일명이나 패키지가 필요하다고 나오기는 했지만, 해당파일이나 패키지를 설치하는 데 또다시 어떤 패키지가 의존성이 있을 수도 있다.</b> 또 어떤 rpm 파일이 필요한지 알아내더라도 해당 rpm 파일이 CentOS 8 DVD에 들어 있지 않을 수도 있다. 이러한 문제를 한 번에해결하기 위해 CentOS에서는 "dnf"라는 명령을 제공한다.

> <b>rpm-qRp 패키지파일이름.rpm</b> 명령을 실행해 의존성 관련 정보를 미리 살펴볼 수 있지만, 어떤 패키지를 설치해야 하는지 정확히 알아내는 것은 좀 복잡하다.

- 이 외에도 강제로 패키지를 설치하는 '--force' 옵션과 의존성을 무시하고 설치하는 '--nodeps' 옵션도 사용할 수 있으나, 이러한 옵션은 정상 설치를 보장할 수 없으므로 주의해서 사용해야 한다.

## 편리하게 패키지를 설치하는 DNF

- RPM은 분명히 유용하지만 앞 실습에서 보았듯이 의존성 문제로 불편한 점이 발생한다. 이를 해결하기 위해 제공하는 것이 DNF Danditied yum 명령어다. DNF는 RPM과 별도라기보다 rpm 패키지를 설치하는 편리한 도구라고 생각하면 된다.

>  CentOS 7까지는 패키지 설치 관리자로 YUM (Yellow Dog Updater, Modified)을 사용했으나, CentOS 8부터는 YUM의 기능이 대폭 개선된 DNF를 주로 사용한다(그래서 DNF를 Dandified Yum으로도 부르는 것 같다). DNF는 YUM과 사용법이 거의 비슷하며 저장소(Repository) 또한 동일하게 "/etc/yum.repos.d/"를 사용하기 때문에, 이전 버전의 centos 사용자도 yum 명령 대신 dnf 명령으로만 변경하면 특별히 사용법을 새로 익힐 필요가 없다. 필요하다면 yum 명령을 계속 사용할 수 있지만 dnf 명령을 사용하는 것이 속도 등에서 더 효율적이다.


### DNF

- dnf 명령은 rpm 명령의 패키지 의존성 문제를 완전히 해결해준다. 즉 특정 패키지를 설치하고자 할 때, 의존성이 있는 다른 패키지를 자동으로 먼저 설치하는 인공지능(?)을 갖춘 명령어다. 
- rpm 명령어는 설치하려는 rpm 파일이 DVD에 있거나 인터넷에서 미리 다운로드한 후 설치해야 한다. 하지만 DNF는 CentOS 프로젝트가 제공하는 rpm 파일 저장소 Repository에서 설치할 rpm 파일은 물론, 해당 파일과 의존성이 있는 다른 rpm 파일까지 인터넷을 통해 모두 알아서 다운로드한 후 자동으로 설치까지 해준다.
- 그러므로 사용자는 rpm 패키지 설치 시 의존성 문제를 고민하지 않아도 된다. 단, '인터넷을 통해' 다운로드한 후 설치하게 되므로 당연히 인터넷에 정상적으로 연결된 상태여야 한다.

- 또한, 추가적으로 궁금해 할만한 사항은 '저장소의 URL은 어떻게 아는가?'라는 문제다. 이 저장소의 URL은 "/etc/yum.repos.d/" 디렉터리의 파일에 저장되어 있다. 이 저장소는 잠시 후 상세히 살펴보고 일단 사용법을 알아보자.

### DNF의 기본 사용법
- DNF의 기본 사용법은 무척 간단하며 대개는 이 기본 사용법으로 충분하다.

#### 기본 설치 방법

```
dnf -f install 패키지이름
```
- 패키지를 설치한 때 사용한다. dnf install은 패키지를 다운로드한 후 사용자에게 설치 여부를 묻는 부분이 나온다. 여기서 -y 옵션을 싸주면 사용자에게 yes/no를 묻는 부분에서 무조건 ves를 입력한 것으로 간주하고 자동으로 넘어가므로 편리하다.

> 주의할 점은 rpm 패키지 파일이 아닌 패키지 이름만 적어야 한다는 것이다. 예를 들어 앞에서 설치한 mc 패키지의 경우 <b>dnf -y install mc</b>까지만 적어줘야 한다. 만약 <b>dnf -y install mc-4.8.19-9.el8.x86_64.rpm</b> 명령으로 전체 rpm 패키지 파일 이름을 적으면 로컬에 있는 rpm 파일을 설치하려고 시도할 것이다.

#### rpm 파일 설치 방법

```
dnf install rpm파일이름.rpm
```

- rpm 파일을 설치하고자 한다면 <b>rpm -Uvh rpm파일이름.rpm</b> 명령 대신 <b>dnf install rpm파일이름.rpm</b> 명령을 실행해 패키지를 설치할 수 있다. dnf가 rpm 명령보다 좋은 점은 <b>현재 디렉터리의 rpm 파일에 의존성 문제가 있을 때, 문제를 해결할 수 있는 파일을 인터넷에서 다운로드하여 설치한다는 점</b>이다. 앞으로 갖고 있는 rpm 파일을 설치할 때는 <b>rpm -Uvh rpm파일이름.rpm</b> 명령 대신 사용한다.

#### 업데이트 가능한 목록 보기

```
dnf check-update
```

- 시스템에 설치된 패키지 중에서 업데이트가 가능한 패키지의 목록을 출력한다. 이 명령을 실행하기 전에 <b>dnf clean all</b> 명령을 실행해서 기존의 dnf 관련 임시 파일을 지우는 것이 좋다.


#### 업데이트

```
dnf update 패키지이름
```

- 소개는 하지만 별로 사용할 필요가 없다. <b>dnf install 패키지이름</b> 명령을 실행하면 기존에 설치되지 않은 패키지는 새로 설치(install)하고, 이미 설치되어 있으면 업데이트한다. 물론 설치가 되어 있고 업데이트할 것이 없다면 그냥 실행을 끝낸다.

- 아무런 옵션을 정하지 않고 <b>dnf update</b> 명령만 실행하면 업데이트 가능한 모든 패키지를 업데이트하므로 시간이 무척 오래 걸릴 것이다.

#### 삭제

```
dnf remove 패키지이름
```

- 기존에 설치된 패키지를 제거한다.

#### 정보 확인

```
dnf info 패키지이름
```

- 패키지의 요약 정보를 보여준다.

### 실습5

- 의존성 문제가 있는 패키지를 dnf 명령으로 설치해본다. 앞 \<실습 4\>에서 설치에 실패한 mysql-errmsg패키지를 설치해보겠다.

#### step 0

Server를 실행하고 root 사용자로 접속한다. 

- 이번 실습은 모두 인터넷에서 패키지 파일을 다운로드한 후 설치하므로 CentOS DVD가 없어도 된다. 단, 네트워크는 꼭 정상적으로 작동해야 한다. DVD가 연결되어 있다면 지금 연결을 끊자.


#### step 1

앞 실습에서 설치에 실패한 mysql-errmsg 패키지를 설치하자.

- 먼저 <b>dnf info mysql-errmsg</b> 명령을 입력해 설치할 패키지의 정보를 확인해보자. 입력 후 CentOS저장소(Repository) 에 접속하느라 시간이 좀 걸릴 수 있다.

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image39.png)

- 해당 패키지를 설치하기 위해 <b>dnf install mysql-errmsg</b> 명령을 입력한다. 인터넷상에서 의존성 있는목록을 확인한 후 몇 개를 설치해야 하는지 확인한다.

> 패키지(Package)가 한글 '꾸러미'로 해석되어 있다.

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image40.png)

- 지금 설치할(Installing) mysql-errmsg 패키지의 경우, 먼저 의존성 있는 종속성 설치=Installing for dependencies) mariadb-connector-c-config 및 mysql-common 패키지 2개가 설치되어야 한다는 메시지가 나왔다. 총 3개의 패키지가 설치되고 총 다운로드 크기와 설치 크기(=설치 이후 크기)까지 나타낸다.

- 여기서 설치하겠다는 'y'를 입력하면 관련 패키지를 모두 다운로드한 후 자동으로 설치한다. 패키지 크기에 따라 설치 시간이 달라질 것이다. 설치가 완료되면 제일 아래 행에 '완료되었습니다!'라는 메시지가 나온다.

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image41.png)

>  'y'를 입력하면 CentOS 프로젝트에서 운영하는 사이트에 접속을 시도한다. 그런데 종종 해당 사이트에 문제가 생겨서 접속이 안 될 수 있다. 그럴 경우 dnf 명령어는 자동으로 다른 미러 사이트(Mirror Site)에 접속을 시도한다. 메시지 중에서 Tring other mirror'라는 메시지가 나오면 정상적으로 접속되는 미러 사이트를 찾는 과정임을 알아두자.

#### step2

그런데 패키지를 설치한 것이 확실하다면 확인 메세지에서 'y'를 입력을 생략하는 것이 훨씬 편리하다.

- 이번에는 앞에서 rpm으로 설치했던 mc 패키지를 dnf로 설치한다. <b>dnf -y install mc</b> 명령을 입력해 설치해보다.

- 설치가 끝날 때까지 아무것도 묻지 않고 설치를 완료할 것이다. 앞으로 대부분의 패키지 설치는 지금과 같은 방식으로 편리하게 진행할 것이다.

#### step3

- 이번에는 <b>dnf -y remove mc</b> 명령을 입력해 설치된 패키지를 삭제해보자.

### DNF 고급 사용법

- 패키지 설치는 대부분 앞에서 사용한 <b>dnf -y install 패키지이름</b> 명령을 실행하는 것으로 충분하다. 그 외에 추가로 알아두면 좋은 것들을 확인하고 이어서 간단한 실습을 해본다.

#### 패키지 그룹 설치

```
dnf groupinstall "패키지그룹이름"
```

- 패키지 그룹 설치는 패키지 그룹에 포함된 패키지들을 통째로 설치할 때 사용할 수 있다.
- 패키지 그룹의 종류는 <b>dnf grouplist</b> 명령으로 확인할 수 있다. 
- 설치 시 패키지 그룹의 이름은 띄어쓰기가 많으므로큰따옴표("") 안에 써야 한다

####  패키지 리스트 확인

```
dnf list 패키지이름
```

- CentOS에서 제공하는 패키지 리스트를 보여준다. 일례로 <b>dnf list all</b> 명령을 실행하면 모든 패키지 목록을 보여주며, <b>dnf list httpd</b> 명령을 실행하면 httpd라는 이름이 들어간 패키지 목록을 보여준다. 그리고 <b>dnf list available</b> 명령을 실행하면 현재 설치 가능한 목록을 모두 보여준다.


#### 특정 파일이 속한 패키지 이름 확인


```
dnf provides 파일이름
```

- 특정 파일이 어느 패키지에 들어 있는지 확인할 수 있다. 
- 예를 들어 <b>dnf provides ifconfig</b> 명령은 ifconfig 명령이 들어 있는 패키지를 알려준다.

#### GPG 키 검사 생략

```
dnf install --nogpgcheck rpm파일이름.rpm
```

- CentOS 8에서 인증되지 않은 rpm 파일을 dnf install로 설치하면 설치되지 않는 경우도 있다. 
- 그런 때 '--nogpgcheck' 옵션을 사용하면 GPG 키 인증을 생략하므로 설치할 수 있다.

#### 기존 저장소 목록 지우기

```
dnf clean all
```

- 기존에 다운로드한 패키지 목록을 지운 다음 <b>dnf install 패키지이름</b> 명령을 실행하면 패키지 목록을 다시 다운로드한다.

### DNF의 작동 방식과 설정 파일

- dnf 명령어와 관련된 설정 파일은 "/etc/yum.conf"와 "/etc/yum.repos.d/" 디렉터리가 있다. yum.conf 파일은 특별히 설정을 변경할 것이 없으므로 앞으로도 신경 쓸 필요 없다. 중요한 것은 "/etc/yum.repos.d/" 디렉터리에 있는 여러 개의 파일이다. 각 파일에는 dnf 명령을 실행했을 때 인터넷에서 해당 패키지 파일을 검색하는 네트워크 주소가 들어 있기 때문이다.

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image42.png)

- 앞의 \<실습 5\>에서 설치한 mysql-errmsg 패키지를 예로 위 그림의 흐름도를 살펴보자. 
- 먼저 ①에서 dnf install mysql-errmsg 패키지 설치 명령을 입력하면, 
- ②에서 자동으로 "/etc/yum.repos.d/" 디렉터리의 repo 파일을 확인한다. 
- 몇 개의 파일 중 핵심 파일은 CentOS-Base.repo 파일과 CentOS-AppStream.repo 파일이다. 이 파일에는 'CentOS 8 패키지 저장소'의 인터넷 주소가 적혀 있다. 
- 그리고 ③, ④와 같이 전체 패키지 목록 파일을 요청하고 다운로드한다. 
- 여기서 주의할 점은 실제 패키지 파일을 다운로드하는 것이 아니며, 패키지의 이름이 들어 있는 목록만 가져온다는 것이다.

- 그리고 다운로드한 패키지 목록 파일을 근거로 사용자가 요청한 mysql-errmsg 패키지와 의존성있는 패키지 목록을 이와 같이 화면에 출력한다. 
- 그림 ⑩에서 사용자가 패키지 목록을 확인하고 설치할 의향이 있다면 모를 입력해 실제 패키지 다운로드를 요청하고 ①에서 해당 패키지 파일 (rpm 파일)을 다운로드해 자동으로 설치한다. 이 흐름에서 독자는 dnt 명령어와 y 입력하면 되며 나머지는 모두 자동으로 처리된다. 또 <b>dnf -y install</b> 패키지파일 명령을 실행하면까지 모두 한 번에 처리된다.

> CentOS 8 패키지 저장소'는 CentOS 사이트(contos.org)뿐 아니라 전 세계적으로 수백 개의 동일한 저장소가 제공된다. 당연한 말이지만, 저장소가 한 곳이라면 셀 수 없을 정도로 많이 설치된 CentOS에서 실행하는 dnf 명령어 실행을 감당할 수 없을 것이다. 방금 설명한 동일한 저장소는 대학 연구소 기업체 등에서 자발적으로 참여해 구축하고 있으며 우리나라도 카카오 네이버 등 몇몇 기업에서 참여하고 있다. 이러한 동일 저장소를 미러 (mirror) 사이트라고 하며 "https://www.centos.org/download/mirrors/"에서 미러 사이트의 주소를 확인할 수 있다.

- 하지만 그러한 것을 신경 쓸 필요 없이 <b>dnf -y install 패키지이름</b> 명령만 실행하면 미러 사이트 중 가장 적절한 곳에 자동으로 접속해서 다운로드한다.

- 이제 repo 파일이 어떻게 구성되었는지 살펴보자. "/etc/yum.repos.d/CentOS-Stream-BaseOS.repo" 파일을 gedit로 열어보면 다음과 같다. 우선 화장명인 repo는 Repository (저장소)의 약자다.

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/7%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%99%80%20%EA%B7%B8%EB%A3%B9%2C%20%ED%8C%8C%EC%9D%BC%2C%20RPM%2C%20DNF/images/image43.png)


#### '#' 
- 주석이므로 없는 것과 마찬가지다.

#### name

- 저장소의 이름이다. 보기 편한 것으로 아무 이름이나 지정해도 되며 별로 중요하지 않다.


#### baseurl

- URL이 적혀 있어야 한다. http, ftp, file 3가지 중 하나가 오면 된다. 독자가 저장소의 URL을 정확히 안다면 직접 적어도 된다. 
- 여러 개가 나올 수 있는데, 지금처럼 baseurl 다음에 여러 URL이 이어져 나오면 앞의 주소가 응답하지 않을 경우 다음 주소를 확인하는 방식으로 패키지를 검색한다.

#### gpgcheck

- 패키지의 GPG 서명을 확인할지 여부를 1 (사용), 0(사용 안 함)으로 지정할 수 있다. 1로 지정할 경우, 이어서 gpgkey 항목을 반드시 설정해야 한다
> GPG 서명은 GnuPG(Gnu Privacy Guard)라고도 부르는데, rpm 패키지를 인증할 때 암호화된 서명을 사용하는 방법이다. CentOS 프로젝트에서 제공하는 rpm 패키지는 GPG 서명을 함으로써 잘못된 패키지가 설치되는 일을 방지한다. 더 상세한 내용은 "https://www.gnupg.org/"를 참조하자.

#### gpgkey

- 앞의 gpgcheck가 1일 경우 아스키 GPG 키가 들어 있는 저장소의 URL이 적혀 있으면 된다.


#### mirrorlist

- baseurl에 설정 값(URL)이 생략되어 있으면 그 대신 mirrorlist에 적힌 URL이 사용된다. 이 mirrorlist의 URL에는 전 세계에 분포된 여러 개의 저장소가 연결되어 있다.

#### enabled

- 이 저장소를 사용할지의 여부를 1 (사용), 0 (사용 안함)으로 지정할 수 있다. 이 행을 생략하면 기본값은 1이다.

- 이 중에서 꼭 필요한 것은 [식별자]와 name, baseurl, gpgcheck 정도다. 지금까지 repo 파일 안의 내용을 길게 설명했는데, 사실 이 내용을 잘 몰라도 CentOS의 dnf 명령을 사용하는 데 별 문제가 없다.

- 기본으로 제공되는 repo 파일은 특별히 변경하지 않는 것이 바람직하지만, 만약 시간이 오래 지나서 CentOS 8의 URL이 변경된다면 dnf 명령어가 작동하지 않을 수 있다. 이럴 때는 직접 이 파일의 내용을 수정해주면 된다. 그럼 이 파일을 직접 변경하는 방법을 실습해보자.

# 실습6

- DNF의 고급 기능을 실습해보자.

### step0

- \<code\>Server\</code> Server를 처음 설치 상태로 초기화하자 
