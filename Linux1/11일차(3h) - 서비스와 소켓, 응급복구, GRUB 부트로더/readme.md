# 서비스와 소켓

- 서비스(service)는 평상시에도 늘 가동하는 서버 프로세스며, 소켓(Socket)은 필요할 때만 작동하는 서버 프로세스다. 서비스와 소켓은(systemd)라는 서비스 매니저 프로그램으로 작동시키거나 관리한다.

> 이전에는 최상의 프로세스인 init 프로세스가 서비스를 직접 관리하는 방식이었으나, 요즘에는 systemd가 서비스 대부분을 관리한다. systemd와 관련된 세부 내용은 https://docs.fedoraproject.org/en-US/quick-docs/understanding-and-administering-systemd/ 주소를 참조하자

## 서비스

서비스의 특징을 살펴보자.

- 시스템과 독자적으로 구동 및 제공되는 프로세스를 말한다. 웹 서버(httpd), DB 서버(mysqld), FTP 서버(vsftpd) 등을 예로 들 수 있다.

- 실행 및 종료는 대개 <b>systemctl start/stop/restart 서비스이름</b> 명령으로 사용된다. 예를 들어 웹 서버는 <b>systemctl start httpd</b> 명령으로 구동한다.

- 서비스의 실행 스크립트 파일은 /usr/lib/systemd/system/ 디렉터리에 '서비스이름.service'라는 이름으로 확인할 수 있다. 예를 들어 Cron 서비스는 crond.service라는 이름의 파일로 존재한다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image1.png)

- 이 디렉터리에 있는 파일들은 대부분 <b>systemctl start/stop/restart 서비스이름</b> 명령으로 실행/중지/재시작할 수 있다.

- 부팅과 동시에 서비스의 자동 실행 여부를 지정할 수 있는데, 터미널에서 <b>systemctl list-unit-files</b> 명령을 실행하면 현재 사용(enabled) 과 사용 안 함(disabled)을 확인할 수 있다.

> 상태(STATE)가 static으로 설정된 것은 사용/사용 안함으로 설정할 수 없으며, 다른 서비스나 소켓에 의존해서 실행된다. 그 외에 generated, transient 등은 특별히 신경쓰지 않아도 된다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image2.png)

#### systemctl 명령

앞으로 systemctl 명령을 많이 사용하게 될 것이다. systemctl 명령에서 자주 사용하는 옵션을 정리하면 다음과 같다.

- 서비스 시작/중지/재시작   -> systemctl start/stop/restart 서비스이름 
- 서비스 상태 확인      -> systemctl status 서비스이름
- 서비스 사용/사용 안 함 설정 -> systemctl enable/disable 서비스이름

## 소켓

- 서비스는 항상 가동되지만 소켓은 외부에서 특정 서비스를 요청할 경우 systemd가 구동시킨다. 그리고 요청이 끝나면 소켓도 종료된다.

-  그래서 소켓으로 설정된 서비스를 요청할 때 처음 연결되는 시간은 앞에서 설명한 서비스에 비해 약간 더 걸릴 수 있다. 왜냐하면 systemd가 서비스를 새로 구동하는 데 시간이 소요되기 때문이다. 이와 같은 소켓의 대표적인 예로 텔넷 서버를 들 수 있다.

- 소켓과 관련된 스크립트 파일은 /usr/lib/systemd/system/ 디렉터리에 '소켓이름.socket'이라는 이름으로 존재한다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image3.png)


#### xinetd 데몬

- 예전 CentOS에서는 소켓과 비슷한 개념으로 xinetd 데몬이 주로 사용되었으며 CentOS 8도 xinetd 데몬을 지원한다. 하지만 많은 서비스가 xinetd 대신 소켓으로 사용된다. 강의에서는 xinetd와 관련된 서비스를 거의 사용하지 않으므로 더 이상 언급하지 않는다. 예를 들어 구현할 텔넷 서버도 예전에는 xinetd와 관련된 서비스였으나 현재는 소켓과 관련된 서비스로 변경되었다.

* * * 
# 응급 복구

- 시스템이 부팅되지 않는 이유는 무척 다양하다. 이때 해야 하는 작업이 '응급 복구'다. 이번에는 응급복구 중에서 리눅스를 사용하다가 root 사용자의 비밀번호를 잊어버려 로그인하지 못하는 경우 해결하는 방법에 대해 배워본다.

- 리눅스를 설치하고 오랜만에 사용할 때 root 사용자의 비밀번호가 기억나지 않아 로그인하지 못하는 경우가 종종 발생한다. 특히 리눅스 초보자라면 그런 경우가 많을 것이다. 학습 목적으로 리눅스를 설치했다면 설치 DVD나 USB로 포맷하고 다시 설치하면 되겠지만 중요한 파일이 들어 있다면 참 난감해지는 상황이 아닐 수 없다. 이런 경우 비밀번호를 다시 알아내는 방법은 없지만 새로운 비밀번호로 변경할 수는 있다.

## 실습1

root 사용자의 비밀번호를 잊어버렸을 때, 해결하는 방법을 알아보자.

#### step0

- Server를 처음 설치 상태로 초기화하자
-  root 사용자로 접속하려면 당연히 비밀번호를 입력해야 한다. 하지만 현재 비밀번호를 잊어버려서 root 사용자로 접속할 수 없는 상황이라고 가정해보자.

#### step1

부팅 시 처음에는 GRUB의 메뉴 화면이 나타난다.

- 기본 선택인 위 메뉴가 선택된 상태에서 E를 누른다(아래 쪽에 써 있듯이 Edit를 의미한다).

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image4.png)

- 키보드의 를 3번쯤 눌러 아래쪽 linux16 ($root)/boot/vmlinuz-4.18.0-80.el8.x86_64~~'행에 커서를 가져다 놓는다. End]를 눌러 행 끝으로 이동한 후 뒤쪽의 'thgb quiet'를 삭제한다. 그리고 제일 뒤에 'init=/bin/sh'를 입력한다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image5.png)

- Ctrl + X를 눌러 부팅한다.

#### step2 

별도의 로그인 절차 없이 부팅되며 'sh-4.4#'이라는 프롬프트가 나올 것이다.

- whoami 명령을 입력해 현재 로그인된 사용자가 root 인지 확인한다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image6.png)

- root 사용자의 비밀번호를 변경하기 위해 passwd 명령을 입력하고 새로운 비밀번호를 8자 이상으로 지정한다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image7.png)

- 그런데 비밀번호를 변경하는 데 오류가 발생한다. 이는 현재 '/(root)' 파티션이 읽기 전용(Read-Only)으로 마운트되었기 때문이다.

#### step3
 
마운트된 파티션을 읽기 쓰기로 변경하자.

- mount 명령을 입력해 제일 아래를 확인하면 '/' 파티션이 RO(Read-Only)로 마운트된 것을 확인할 수 있다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image8.png)

- <b>mount -o remount,rw /</b> 명령을 입력해 '/' 파티션을 읽기/쓰기 (rw) 모드로 다시 마운트(remount) 시킨다. 그리고 <b>mount</b> 명령을 입력하면 읽기/쓰기 모드로 변경된 것을 확인할 수 있다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image9.png)

- 다시 <b>passwd</b> 명령을 입력해 현재 사용자인 root 의 비밀번호를 변경한다. 이번에는 그냥 간단히 1234로 변경해보자. 경고는 나오지만 성공적으로 변경될 것이다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image10.png)

- Virtual Box의 Server 가상머신에서 마우스 오른쪽키를 누른 후 -> 재시동을 클릭하여 재 부팅한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image11.png)

- 여기서 의아하게 생각할 수 있을 것이다. CentOS 리눅스는 지금 실습한 방법만 안다면 누구든지 root 사용자의 권한을 얻어서 시스템에 접근할 수 있다는 말인가? 답부터 말하자면 '그렇다.' 그래서 시스템을 보호하려면 처음 부팅할 때 나오는 GRUB 자체를 편집한 수 없도록 설정한 필요가 있다. 또 컴퓨터 BIOS의 CMOS 비밀번호를 이용한 하드웨어 보안도 고려해볼 수 있다. 다음에는 GRUB에 비밀번호를 설정해서 아무나 root 사용자의 권한을 얻는 것을 막아보자.

* * * 
## GRUB 부트로더

- CentOS에서 기본적으로 제공하는 GRUB 부트로더를 살펴보자. GRUB 부트로더란 CentOS를 부팅할 때 처음 나오는 선택 화면을 말한다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image12.png)

- GRUB의 기본적인 특징은 다음과 같다.
	- 부트 정보를 사용자가 임의로 변경해 부팅할 수 있다. 즉 부트 정보가 올바르지 않더라도 수정하여 부팅할 수 있다. 
	- 다른 여러 가지 운영체제와 멀티부팅을 할 수 있다.
	- 대화형 설정을 제공하므로 커널 경로와 파일 이름만 알면 부팅이 가능하다.

- 그런데 CentOS에서는 이전의 GRUB보다 더 향상된 GRUB 2 버전을 사용한다. GRUB 2는 셸스크립트 문법을 사용하기 때문에 이전의 GRUB보다 설정을 변경하기가 훨씬 복잡해졌다. 하지만 다음과 같은 장점도 있다.
	- 셸 스크립트를 지원함으로써 조건식과 함수를 사용할 수 있다.
	- 동적 모듈을 로드할 수 있다. 동적 모듈은 /boot/grub2/i386-pc/ 디렉터리에 mod 파일로 존재한다. GRUB 2는 필요에 따라 이 파일들을 로드할 수 있다.
	- 그래픽 부트 메뉴를 지원하며 부트 스플래시(boot splash)성능이 개선되었다.
	- ISO 이미지를 이용해서 바로 부팅할 수 있다.
	- 설정 파일의 형식이 변경되었지만 더 향상된 내용을 포함할 수 있다.
	
- GRUB 2의 설정 파일은 /boot/grub2/grub.cfg 파일이며 /etc/grub2.cfg는 링크 파일이다.

- grub.cfg 파일은 일반 사용자에게 읽기 전용이며, root 사용자도 이 파일을 직접 편집해서는 안 된다. 설정된 내용을 변경하려면 /etc/default/grub 파일과 /etc/grub.d/ 디렉터리의 파일을 수정한 후 grub2-mkconfig 명령을 실행한다.

- 우선 /etc/default/grub 파일의 설정 내용을 이해하자.

|행번호|내용|
|----|--------|
|1|GRUB_TIMEOUT=5|
|2|GRUB_DISTRIBUTOR="$(sed 's, release \*$.g' /etc/system-release)"|
|3|GRUB_DEFAULT=saved|
|4|GRUB_DISABLE_SUBMENU=true|
|5|GRUB_TERMINAL_OUTPUT="console"|
|6|GRUB_CMDLINE_LINUX="crashkernel=auto resume=UUID=장치코드고유번호 rhgb quiet"|
|7|GRUB_DISABLE_RECOVERY="true"|
|8|GRUB_ENABLE_BLSCFG=true|

- 1행 -> 처음 화면이 나오고 자동으로 부팅되는 시간을 초 단위로 설정한다. -1로 하면 자동으로 넘어가지 않고 사용자가 직접 엔트리를 선택할 때까지 기다린다.

- 2행 -> 초기 부팅 화면의 각 엔트리 앞에 붙을 배포판 이름을 추출한다. 이 행의 경우 /etc/system-release 파일에서 'CentOS'라는 글자를 추출한다. 그래서 GRUB 부트로더 앞 부분에 CentOS가있는 것이다.

- 3행 -> saved는 이전에 선택한 엔트리가 기본으로 계속 선택되도록 한다는 뜻이다. 0번으로 지정하면 첫 번째 엔트리를 의미한다.

- 4행 -> 서브 메뉴 사용 여부를 설정한다. 기본값을 true로 설정해두면 서브 메뉴를 사용하지 않는다. 특별히 설정을 변경할 필요는 없다.

- 5행 -> GRUB이 나올 장치를 설정한다. 기본값을 console로 설정해두면 모니터로 설정된다. 그 외serial, gfxterm(그래픽 모드 출력) 등으로도 설정할 수 있다.

- 6행 -> 부팅 시 커널에 전달할 파라미터를 지정한다. 이전에 사용하던 GRUB 1의 파라미터도 일부 사용할 수 있다. 앞에 나온 \<실습1\>의  단일 사용자 모드(응급 복구 모드)로 접속하기 위해 이 행과 관련된 제일 뒤에 'init=/bin/sh'를 붙여서 부팅했었다.

- 7행 -> true로 설정하면 메뉴 엔트리에서 복구와 관련된 것을 비활성화한다. 특별히 변경할 필요는 없다.
- 8행 -> BLSCFG는 Bootloader Spec for configuring의 약자인데 특별히 변경할 필요는 없다. 

> GRUB 2와 관련된 내용은 상당히 방대하므로 GRUB의 문법을 설명하지 않을 것이다. GRUB에 대한상세 내용은 http://www.gnu.org/software/grub/manual/grub/grub.html 을 참조하자.

## 실습2 

GRUB 부트로더를 변경하고, 부트로더에 비밀번호를 설정하자

#### step0

Server를 처음 설치 상태로 초기화하자 

- root 사용자로 접속한다.
- 바탕 화면 왼쪽 위의 [현재 활동] →[터미널]을 선택해서 터미널을 연다.

#### step1

부팅 시 20초간 대기하고 GRUB 화면이 초기에 보이도록 설정한다.

-  gedit이나 vi 에디터로 /etc/default/grub 파일을 열고 첫 행의 부팅 시간을 20초로 변경한다.

```
GRUB_TIMEOUT=20
-- 이하 생략 --
```

- 파일 내용을 확인한 후 변경한 내용을 적용하기 위해 <b>grub2-mkconfig -o /boot/grub2/grub.cfg</b> 명령을 입력한다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image13.png)

- <b>reboot</b> 명령을 입력해 재부팅하면 GRUB 화면이 초기에 보이며 20초 동안 대기하게 될 것이다.

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image14.png)

- root 사용자로 접속한다.

#### step2

이번에는 GRUB에 비밀번호를 설정하여 앞의 \<실습 1\>에서 아무나 GRUB을 편집할 수 있었던 문제점을 해결해보자.

-  gedit이나 vi 에디터로 /etc/grub.d/00_header 파일을 열어 제일 아래에 다음 4 개 행을 추가하고 저장한 후 닫는다. 여기서 GRUB 사용자는 기존 리눅스 사용자와 관련이 없으며 새로 지정하면 된다.

```
cat << EOF
set superusers="thisislinux"  -> thisislinux는 새로운 GRUB 사용자의 이름이다.
password thisislinux 1234   -> 'GRUB사용자 새 비밀번호(1234)' 형식으로 설정한다,
EOF
```

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image15.png)

- 변경한 내용을 적용하기 위해 <b>grub2-mkconfig -o /boot/grub2/grub.cfg</b> 명령을 입력한다.

- <b>reboot</b> 명령으로 시스템을 재부팅한다. 이제부터 부팅, 편집, 명령 실행 등 GRUB을 사용하려면 앞에서 설정한 사용자와 비밀번호가 있어야 한다. 먼저 편집을 위해 E를 누르면 사용자와 비밀번호를 입력하는 창이 나온다. 앞에서 설정한 사용자와 비밀번호가 정확해야만 편집 모드로 들어갈 수 있다.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/11%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%84%9C%EB%B9%84%EC%8A%A4%EC%99%80%20%EC%86%8C%EC%BC%93%2C%20%EC%9D%91%EA%B8%89%EB%B3%B5%EA%B5%AC%2C%20GRUB%20%EB%B6%80%ED%8A%B8%EB%A1%9C%EB%8D%94/images/image16.png)

- 편집 모드에서는 별도로 설정을 변경하지 말고 Ctrl + X 를 눌러 부팅한다.