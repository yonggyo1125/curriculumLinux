# 리눅스 기본 개념

## 시작과 종료 
- 리눅스를 시작하려면 당연히 컴퓨터의 전원을 켜야 한다. 앞서 설치한 Server와 Client를 부팅하면 X 윈도가 자동으로 실행된다.

> X 윈도(X Window) Microsoft사의 Windows와 같은 GUI를 리눅스에 제공한다. 그런데 Windows의 경우 그래픽 모드가 없으면 운영이 거의 불가능하지만, 리눅스의 X 윈도는 하나의 편리한 유틸리티일 뿐이지 반드시 필요한 것은 아니다. 앞서 설치한 Server (B)의 경우처럼 X 윈도를 설치하지 않아도 잘 운영된다.

- CentOS는 이 X 윈도를 사용하기 위해 기본적으로 GNOME(그놈)이라는 데스크톱 환경을 제공한다.

- X 윈도 환경에서 접속하려면 Server는 root 사용자로, Client는 centos 사용자로 접속한다. 이제 X 윈도로 접속한 후 시스템을 종료하는 몇 가지 방법을 살펴보자.

	- 바탕 화면 오른쪽 상단 [전원 아이콘] → [전원 아이콘] → \<컴퓨터 끄기\>
		- X 윈도 환경에서 바로 시스템을 종료하는 가장 간단한 방법이다.
		
		![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image1.png)
		
		![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image2.png)
		
	- 터미널/콘솔에서 시스템 종료 명령 실행
		- <b>poweroff, shutdown -P now, halt -p 및 init 0</b> 명령을 실행하면 된다. '-P' 또는 '-p' 옵션은 시스템 종료를 의미한다(init 0의 의미는 잠시 후 설명한다).
		
		![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image3.png)
		
> 대소문자 및 사용자 구분<br>유닉스/리눅스에서는 대문자와 소문자를 명확히 구분한다는 점을 기억해야 한다. 사소하지만 이를 무시하면 실습이 원활하게 진행되지 않을 것이다. 또 기억해야 할 점은 일반 사용자가 관리자(root 사용자) 권한을 얻으려면 <b>su -</b> 명령 또는 <b>su</b> 명령을 실행한 후 root 사용자의 암호를 입력해야 한다는 것이다. 참고로 root 사용자와 일반 사용자를 구분하려면 프롬프트의 표식을 확인한다. <b>'#'이면 root 사용자 '$'면 일반 사용자</b>라고 보면 된다.

- shutdown 명령의 옵션 중 'now' 부분에 시간을 지정하면 지정한 시간에 시스템을 종료한다. 예를 들면 다음과 같다.

```
# shutdow -P +10      -> 10분 후 종료(P: poweroff)
# shutdown -r 22:00   -> 오후 10시에 재부팅(r: reboot)
# shutdown -c           -> 예약된 shutdown 취소(c: cancel)
# shutdown -k +15     -> 현재 접속한 사용자에게 15분 후 종료된다는 메시지를 보내지만 실제로는 종료되지 않음
```

## 시스템 재부팅

- CentOS를 재부팅하려면 \<컴퓨터 끄기\> 대신 \<다시 시작\> 버튼을 클릭하면 된다. 명령을 실행해 재부팅하려면 <b>shutdown -r now, reboot, init 6</b> 등의 명령을 사용한다.

## 로그아웃

- 로그아웃(Logout)은 시스템 종료와 의미가 다르다. <b>현재 사용자의 시스템 접속을 끝낸다는 뜻이지 시스템을 종료한다는 의미가 아니다.</b> 리눅스는 여러 명의 사용자가 동시에 접속해서 사용하는 다중 사용자Multi-User 시스템이므로 자신만 접속을 끝내는 로그아웃이 필요하다. 만약 관리자가 자신이 사용하지 않는다고 시스템을 종료시켜 버리면, 시스템에 접속된 많은 사용자는 작업 중에 컴퓨터가 종료되는 황당한 경험을 하게 될 것이다.

- X 윈도에서 로그아웃하려면 오른쪽 위의 전원 모양 아이콘을 클릭한 후 사용자 이름을 확장하고 \[로그아웃\]을 선택한다. Server (B)와 같은 텍스트 모드에서 로그아웃하려면 logout 또는 exit 명령을실행한다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image4.png)


## 가상 콘솔

- 가상 콘솔이란 '가상의 모니터'라고 생각하면 이해하기 쉽다. CentOS는 총 6개의 가상 콘솔을 제공한다. 즉, 컴퓨터 한 대에 모니터 여섯 개가 연결된 효과를 낼 수 있다는 의미다.

- Server를 부팅하면 X 윈도가 자동으로 실행된다. 이 X 윈도가 가동된 화면은 6개의 가상 콘솔 중첫 번째라고 생각하면 된다. 나머지 2~6번 가상 콘솔은 텍스트 모드로 제공된다. 각각의 가상 콘솔로 이동하는 단축키는 [Ctrl] + [Alt] + [F1] ~ [F6]이다. 현재는 2번 가상 콘솔을 보는 상태며, 3번 가상 콘솔로 변경하려면 [Ctrl] + [Alt] + [F3]을 누른다. 다시 X 윈도 화면으로 돌아오려면 [Ctrl + [Alt] + [F2]를눌러서 2번 가상 콘솔로 변경한다. 


### 실습1

- 여러 명의 사용자가 동시에 리눅스에 접속해 있을 때 시스템이 어떻게 종료되는지 확인해보자.

- shutdown 명령을 실행했을 때 다른 사용자에게 어떻게 메시지가 전달되는지 확인해보자.
	- <code>2번 가상 콘솔: root 사용자</code> [Ctrl] + [Alt] + [F3]을 1초 정도 꾹 누른다. 그러면 텍스트 모드의 2번째 가상 콘솔이 나온다. root 사용자(암호는 password)로 접속하자. root 사용자의 프롬프트는 #으로 표시된다.
	
	> [F3]을 눌러서 나오는 것은 2번째 콘솔로 [F4]를 눌러서 나오는 것은 3번째 콘솔로 취급하자.

	
	![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image5.png)

	- 화면에 2번째 콘솔을 의미하는 'tty2'가 표시되어 있다.
	
	- <code>3번 가상 콘솔: centos 사용자</code> 이번에는 [Ctrl] + [All + [F4]를 눌러서 텍스트 모드의 3번째 가상 콘솔이 나오도록 하고, centos 사용자(암호는 centos)로 접속하자. root 사용자 외 다른 모든 사용자의 프롬프트는 $로 표시된다.
	
	![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image6.png)
	
	- <code>2번 가상 콘솔: root 사용자</code> 다시 [Ctrl] + [Alt] + [F3]을 누르고 shutdown -h +5 명령을 입력한다. 이는 시스템을 5분 후에 종료한다는 의미다. 5분 후에 종료된다는 메시지가 나온다.
	
	![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image7.png)
	
	- <code>3번 가상 콘솔: centos 사용자</code> 다시 [Ctrl] + [Alt] + [F4]를 누르면 root 사용자에게 메시지가 왔으며, 5분 후 종료된다는 내용을 확인할 수 있다. [Enter]를 누르면 centos 사용자는 5분 동안 현재 실행 중인 작업을 마무리할 수 있다 (이 경고 메시지는 매분 나타난다).
	
	![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image8.png)
	
	- <code>2번 가상 콘솔: root 사용자</code> 다시 [Ctrl] + [Alt + [F3]을 누른다. 5분이 경과하기 전에 shutdown -c 명령을 입력하면 예약된 shutdown 명령 실행을 취소할 수 있다.
	
	![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image9.png)
	
	- <code>3번 가상 콘솔: centos 사용자</code> 다시 [Ctrl + [Alt] + [F4]를 눌러 4번째 가상 콘솔을 확인하면 shutdown 명령 실행이 취소되었다는 메시지가 보일 것이다.
	
	![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image10.png)
	
- 이번에는 root 사용자가 시스템을 종료하지 않고, 다른 사용자가 시스템 접속을 로그아웃하도록 유도하는 shutdown 명령을 사용해보자. 이 방법은 root 사용자가 시스템 유지 관리 등의 목적으로 다른 사용자의 로그아웃을 유도할 때 사용할 수 있다.
	- <code>2번 가상 콘솔: root 사용자</code> 다시 [ctrl] + [All] + [F3]을 누른 후 <b>shutdown -k +10</b> 명령을 입력한다. 10분 후 시스템이 종료된다는 메시지가 나오지만 실제로는 종료되지 않고, 즉시 내부적으로 shutdown 명령 실행이 취소된다.
	
	![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image11.png)
	
	- <code>3번 가상 콘솔: centos 사용자</code> 다시 [Ctrl] + [Alt + [F4]를 눌러 3번째 가상 콘솔을 확인하면 centos 사용자에게도 시스템이 종료된다는 메시지가 나온다(기다리면 계속 반복적으로 메시지가 나온다). 하지만 centos 사용자는 이 메시지가 진짜로 종료된다는 것인지 그냥 가짜로 종료된다는 것인지 확인할 수 없으므로, 빨리 현재 작업을 마무리하고 로그아웃하게 될 것이다 ([Enter]를 누르면 프롬프트가 나오고 빨리 현재 작업을 마무리할 수 있다).
	
	![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image12.png)
	
- 2번 가상 콘솔과 3번 가상 콘솔에서 모두 logout 명령을 입력해 로그아웃한 후 [Ctrl] + [All] + [F2]를 눌러 다시 원래의 콘솔인 X 윈도 화면으로 돌아온다.


## 런레벨

- 앞에서 시스템을 종료하는 init 0 명령과 재부팅하는 init 6 명령을 언급했다. init 명령 뒤에 붙는 숫자를 런레벨(RunLevel)이라고 부른다. 리눅스는 <b>시스템이 가동되는 방법</b>을 <b>7가지 런레벨</b>로 나눌 수 있으며, 런레벨은 다음과 같다.

|런레벨|영문 모드|설명|비고|
|----|----|------|----|
|0|Power Off|종료 모드||
|1|Rescue|시스템 복구 모드|단일 사용자 모드|
|2|Multi-User||사용하지 않음|
|3|Multi-User|텍스트 모드의 다중 사용자 모드||
|4|Multi-User||사용하지 않음|
|5|Graphical|그래픽 모드의 다중 사용자 모드||
|6|Reboot|||

> 일반적으로 런레벨 3번을 Multi-User 모드로 사용한다. 2번과 4번은 CentOS 8에서 사용하지 않지만 호환성을 위해 런 레벨 3번과 동일한 것으로 취급한다.

- 위 표에 나온 런레벨 모드를 확인하려면 "/lib/systemd/system" 디렉터리의 runlevel?.target 파일을 확인한다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image13.png)

- 7개의 runlevel?.target 파일은 링크 파일이다. 각각의 링크 파일은 실제 파일과 연결되어 있다. 예를 들어 runlevel0.target 파일은 실제로 poweroff.target 파일을 가리킨다.

> 링크 파일(Linked File)은 Windows의 '바로 가기 아이콘과 비슷한 개념이다. 즉 실제 파일이 있는 것은 아니며 다른 파일을 가리키는 개념이다.


- 앞에서 설명한 <b>init  0</b> 명령은 '지금 즉시 런레벨 0번으로 시스템을 전환하라'는 의미며, 런레벨 0번은 종료 모드를 의미하므로 결국 '지금 즉시 시스템을 종료하라'는 의미다. 또한 <b>init 6</b> 명령은 '지금 즉시 재부팅하라'는 의미다.


- 우리가 설치한 Server와 Client는 부팅 시 자동으로 X 윈도가 시작되므로 런레벨 5번으로 지정된다. Server(B)는 텍스트 모드로 시작되므로 런레벨이 3번으로 지정된다.

- 현재 시스템에 설정된 런레벨은 링크 파일인 "/etc/systemd/system/default.target" 을 확인하면 알 수 있다.  

> 이전 버전의 CentOS 리눅스에서는 "/etc/inittab" 파일에 런레벨이 설정되어 있었지만, 지금은 호환성을 유지하기 위해 주석 (Remark)이 있는 빈 파일만 남아 있다. 실제로 런레벨을 설정할 때는 \<실습 2\>의 방식을 사용해야 한다.

### 실습2
시스템에 설정된 런레벨을 변경해보자.

- step0 
	- Server 가상머신을 사용하자.
	- 바탕 화면의 왼쪽 위 [현재 활동] → [터미널]을 선택해서 터미널을 연다.

- step1
	- 터미널에서 현재 설정된 런레벨을 확인하자.
	- cd 명령을 입력한 다음, 이어서 <b>Is -l /etc/systemd/system/default.target</b> 명령을 입력해 default.target에 연결된 파일을 확인하자. <b>default.target은 시스템에 기본으로 설정된 런레벨이 지정</b>되어 있다.
	
	![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image14.png)
		
	- 결과를 보면 링크 파일인 default.target은 그래픽 모드로 부팅하도록 설정하는 "/lib/systemd/system/" 디렉터리의 <b>graphical.target</b>을 가리킨다. 즉 Server 가상머신은 처음 부팅 시 그래픽 환경으로 부팅되도록 설정되어 있다.
	
- step2
	- 부팅 시 텍스트 모드로 부팅되도록 런레벨을 변경하자.
	- <b>In -sf/lib/systemd/system/multi-user.target /etc/systemd/system/default.target</b> 명령으로 default.target이 가리키는 파일을 텍스트 모드로 부팅되는 런레벨 3번인 multi-user.target으로 변경하자. <b>Is -l /etc/systemd/system/default.target</b> 명령을 입력하면 파일에 설정된 내용을 확인할 수 있다 (In 명령은 링크 파일을 만드는 명령어이며 잠시 후 배운다).
	
	![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image15.png)
	
	- reboot 명령을 입력해 시스템을 재부팅하자.
	
- step3
	- 이제는 Server (B)와 같이 텍스트 모드로 부팅된다.
	- root 사용자로 접속한다.
	-  X 윈도를 실행하려면 startx 명령을 입력한다.
	
	![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image16.png)
	
	- 잠시 기다리면 X 윈도가 실행되고, 폴더 이름을 영문으로 변경하겠냐는 메시지가 나온다. <Keep Old Names>를 클릭한다 (영문 모드의 X 윈도로 부팅되므로 기존의 한글 폴더 이름을 변경하겠냐는 메시지다).
	
	![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image17.png)
	
> 폴더와 디렉터리는 동일한 용어라고 생각해도 된다. Windows에서는 주로 폴더(Folder)라고 부르고, 유닉스/리눅스에서는 디렉터리(Directory)라고 부를 뿐이다. 현재는 혼용해서 많이 사용한다. 앞으로 필자도 필요에 따라 적절한 용어로 혼용해서 사용할 것이다.
	
- 영문이라는 점만 다를 뿐 동일한 그놈GNOME 화면이 나올 것이다. 왼쪽 위의 [Activities] → [Terminal]을 선택해서 터미널을 열고 다음 명령을 입력해 원래 상태인 그래픽 모드로 부팅하자.

```
ln -sf /lib/systemd/system/graphical.target  /etc/systemd/system/default.target

reboot
```

- step4
	- 재부팅 후 원래대로 한글 그놈GNOME 화면이 나올 것이다.


## 자동완성과 히스토리

- 자동 완성이란, 파일 이름의 일부만 입력하고 Tab을 눌러 나머지 파일 이름 또는 폴더 이름을 자동으로 완성하는 기능을 말한다. 예를 들어 터미널에서 "/etc/sysconfig/network-scripts/" 디렉터리로 이동할 때 "cd /etc/sysconfig/network-scripts" 명령을 모두 입력해도 되지만, cd /et[Tab] sysco[Tab] network[Tab] 형태로 입력하면 파일이나 디렉터리 이름이 자동으로 완성된다.
- 도스 키(Dos Key)란 이전에 입력한 명령을 "위아래 방향키"를 눌러 다시 나타나게 하는 것을 말한다. 앞으로 자주 사용할 기능이므로 간단한 실습을 통해 익혀보자.

### 실습3

자동 완성 기능과 도스 키 기능을 사용해보자.

- step0
	- Server를 실행해서 root 사용자로 접속하자.
	
- step1
	- 먼저 <b>도스 키</b>를 사용해보자.
	-  바탕 화면 왼쪽 위의 [현재 활동] →[터미널]을 선택해서 터미널을 연다.
	- 터미널에서 "위아래 방향키"를 여러 번 눌러보자. 이전에 실행했던 명령들이 나올 것이다. 필요한 명령을 선택한 다음 Enter를 누르면 바로 실행된다.
	
	![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image18.png)
	
	- 기존에 사용했던 명령을 모두 보려면 history 명령을 입력한다.
	
	![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image19.png)
	
	- 저장되었던 명령을 모두 삭제하려면 history -c 명령을 입력한다.
	
	![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image20.png)
	
- step2
	- 자동 완성 기능을 사용해보자. 앞으로 계속 사용되므로 잘 기억해두자
	-  먼저 현재 디렉터리에 있는 파일을 확인한다(사용하는 명령은 잠시 후 자세히 설명한다).
	
	```
	cd             -> 현재 사용자의 홈 디렉토리로 이동
	ls              -> 파일 확인
	cat a[Tab]   -> 파일 내용 출력
	```
	- 위에서 'a'만 입력한 후 Tab을 누르니 자동으로 anaconda-ks.cfg가 완성되었다. 이러한 기능이 자동 완성이다. 즉 파일이나 디렉터리 이름의 일부만 입력해도 자동으로 나머지가 완성된다. 
	
	![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image21.png)
	
	- 비슷한 이름이 여러 개 있을 때 자동 완성 기능을 사용하는 방법을 살펴보자. 먼저 <b>cd /etc</b> 명령를 입력해 /etc 디렉터리로 이동한다.
	- 현재 디렉터리는 /etc인데, 하위 디렉터리인 sysconfig 디렉터리로 이동하고자 한다. <b>cd sys[Tab]</b>입력해보자. 아무 반응도 안할 것이다.
	
	- 다시 [Tab]을 눌러보자. 그러면 아래에 3개의 이름 후보가 나온다. 즉 앞에 'sys'라는 글자가 들어간 디렉터리 또는 파일이 1개가 아니기 때문에 'sys'라는 글자만으로는 자동 완성되지 않았던 것이다.
	
	![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image22.png)
	
	- 이번에는 'cd sysco'까지 입력하고 [Tab]을 눌러보자. 'sysco' 글자가 들어간 것은 sysconfig 파일 1개뿐이므로 자동 완성 기능이 작동한 것이다. 다시 'net'를 입력하고 [Tab]을 누르면 'network-scripts'가 완성된다. Enter를 누르자.
	
	![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image23.png)
	
	- 이 정도면 자동 완성 기능 사용법을 익혔을 것이다. 자동 완성 기능을 사용하면 적은 키보드 입력만으로도 빠르게 글자를 입력할 수 있다는 장점이 있다. 그보다 더 큰 장점은 오타를 내지 않고 정확하게 입력할 수 있다는 점이다. 리눅스를 처음 사용할 때 많이 하는 실수 중 하나는, 파일 이름이나 디렉터리 이름을 잘못 입력하는 것이다. 앞 작업이 잘못되었는데 계속 후속 작업을 진행하면 당연히 제대로 되지 않을 것이다.

- step3
	- 앞으로 많이 할 실수를 미리 확인해보자.
	- ifcfg-enp0s3 파일의 내용을 확인하려고 한다. 다음 명령을 입력해 디렉터리를 이동하고 파일을 확인하자. 다음 명령은 모두 직접 입력한다.
	
	```
	cd     -> 사용자의 홈 디렉토리로 이동
	cd /etc/sysconfig/network-script/    -> 디렉토리 이동
	cat ifcfg-enp0s3
	```
	
	![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image24.png)
	
	
	- 위의 명령을 실행한 결과가 제대로 나오지 않는다. '/network-script' 디렉터리가 아니라 '/networkscripts' 디렉터리를 입력해야 하는데 오타가 있었기 때문이다. 처음 리눅스를 사용할 때 디렉터리나 파일 이름을 틀리는 아주 흔한 경우다.
	
	- 자동 완성 기능을 사용해보자. 실수 없이 입력될 것이다.

	```
	cd             -> 사용자 홈 디렉토리로 이동
	cd   /et[Tab]/sysco[Tab]/net[Tab]             -> 디렉토리 이동
	cat ifc[Tab]-e[Tab]           -> 파일 내용 확인
	```
	
	![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/3%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image25.png)
	
	- exit 명령을 입력해서 터미널을 닫는다.

- 이처럼 자동 완성 기능[Tab]을 사용하면 적게 입력하고 빠른 속도로 작업할 수 있을 뿐만 아니라, 오타 없이 결과를 낼 수 있다. 여러 번 반복해서 실습한 기능이므로, 앞으로 이 기능을 꼭 사용해서 실수를 최소화하는 습관을 들인다면 빠른 학습에 도움이 될 것이다.