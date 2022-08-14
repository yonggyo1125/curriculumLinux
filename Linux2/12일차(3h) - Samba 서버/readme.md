#  리눅스에서 Windows의 폴더와 프린터 사용

- Windows에서 폴더와 프린터를 공유해놓으면, Windows에서는 특별한 절차 없이 공유된 폴더와 프린터를 사용할 수 있다. 이러한 방식으로 Windows에서 공유해둔 폴더와 프린터를 리눅스에서도 자유롭게 사용해보자.

- 이번에 구현할 네트워크 구성은 다음과 같다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image1.png)

- 이 구성도에서 한 가지 확인해야 할 것은 'Samba 서버'를 별도로 설치할 필요가 없으며 'Samba 클라이언트만 있으면 된다는 점이다. 즉 Windows가 Samba 서버 역할을 해서 자신의 공유 폴더와 프린터를 제공하며, 리눅스(Server)는 Samba 클라이언트 역할을 해서 Windows가 제공한 폴더와 프린터를 사용하는 것이다. Windows는 기존과 같이 다른 Windows에게 폴더와 프린터를 공유한다는 설정만 해놓으면 자동으로 Samba 서버 역할을 한다.


- 위 그림을 보며 실습할 차례를 요약하면 다음과 같다.

#### WinClient(Samba 서버 역할)

- WinClient에 자신의 자원을 사용할 사용자를 추가한다.
- WinClient의 자원을 공유시킨다.

#### Server(Samba 클라이언트 역할)

- Samba 클라이언트 패키지가 설치되어 있는지 확인한다.
- smbclient 명령으로 WinClient가 제공하는 자원을 확인한다.
- smbmount 명령으로 WinClient가 제공한 공유 폴더를 마운트한다.

> Samba 소스 파일<br>Samba의 소스 파일을 다운로드하거나 자세한 사용법을 알고 싶으면 http://www.samba.org/ 를 참고하자.

### 실습1
- Windows의 폴더를 공유하고, 리눅스에서 접근해 사용해보자.

#### step 0

- <code>Server</code> Server를 처음 설치 상태로 초기화하자.
- 부팅하고 root 사용자로 접속하자.

#### step 1

<code>WinClient 또는 호스트 운영체제</code> Windows의 폴더를 공유하자.

- Windows 파일 탐색기에서 C:\smbShare\라는 폴더를 만든다(폴더 이름은 아무렇게나 지어도 관계없다). 만든 폴더를 마우스 오른쪽 버튼으로 클릭한 다음 바로가기 메뉴에서 [속성] → [공유]를 선택하고 \<공유\> 버튼을 클릭하여 다음과 같이 Everyone 사용자를 선택한 후 \<추가\>를 클릭하자. 그리고 [사용 권한 수준] 설정은 [읽기/쓰기]를 선택해 읽기/쓰기가 가능하도록 하고 \<공유\>를 클릭한 후 \<완료\>를 클릭한다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image2.png)

- 최종적으로 '컴퓨터이름\smbShare' 또는 'IP주소\smbShare'라는 네트워크 경로로 공유되었다. \<닫기\>를 클릭해서 공유 설정을 마친다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image3.png)

- 공유한 폴더인 C:\smbShare에 적당한 파일 몇 개를 복사한다.

#### step 2

<code>WinClient 또는 호스트 운영체제</code> 리눅스에서 접근을 허용하려면 리눅스의 사용자를 추가하고 비밀번호를 지정해야 한다.

- 파워셸이나 명령 프롬프트를 관리자 모드로 실행한 후 다음 명령을 입력하자.

> 제어판의 [사용자 계정]에서 사용자를 추가할 수도 있으나, Windows 버전별로 사용법이 많이 달라서 혼란스러울 수 있으므로 간단히 명령으로 사용자를 추가하자.

```
net user root 1234 /add  -> root 사용자를 만들고 암호를 1234로 지정 
```

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image4.png)

- 필요하다면 제어판의 [사용자 계정]에서 추가된 root 사용자를 확인할 수 있다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image5.png)

-  파워셸이나 명령 프롬프트에서 <b>ipconfig</b> 명령으로 Windows의 IP 주소를 확인하자.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image6.png)

#### step 3

<code>Server</code> WinClient에서 공유한 폴더를 Server에서 사용해보자.

- <b>dnf -y install samba-client</b> 명령으로 Samba 클라이언트 패키지를 설치한다.
- <b>rpm -qa | grep samba</b> 명령으로 Samba 클라이언트 패키지인 samba-client와 samba-common이 설치되어 있는지 확인해보자.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image7.png)

- 먼저 다음 명령을 입력해 Windows에서 공유한 폴더 및 프린터가 보이는지 확인한다. 공유 폴더만 확인하는 것이므로 결과에 오류가 나와도 상관없다.

```
smbclient -L WinClient_IP주소
Enter root's password:     -> Windows에서 생성한 root 사용자의 암호(여기에서는 1234다)
```

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image8.png)

- 다음 명령을 입력해 WinClient에서 공유한 폴더 (smbShare로 공유했었다)에 마운트할 디렉터리(아무 이름이나 지어도 상관없다)를 만들고 마운트시킨다.

```
mkdir 마운트할디렉토리이름
mount -t cifs //WinClientIP주소/공유폴더이름  마운트할디렉토리이름
Password :     -> Windows에서 생성한 root의 암호(여기에서는 1234)
```

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image9.png)

- 이제 /sambaMount 디렉터리를 사용한다는 것은 WinClient의 C:\smbShare\라는 폴더를 사용한다는 것과 같은 의미가 된다. /sambaMount 디렉터리에 파일을 몇 개 복사하고 WinClient의 파일 탐색기에서 확인해도 잘 보일 것이다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image10.png)

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image11.png)

- 더 이상 마운트할 필요가 없다면 <b>umount/sambaMount</b>

* * * 
# Windows에서 리눅스 폴더와 프린터 사용

이번에는 리눅스에서 공유해놓은 디렉터리와 프린터를 Windows에서 사용해보자. Windows에서 리눅스로 접근하는 방식도 별반 어렵지 않다.

##  Windows에서 리눅스로 접근

- Windows에서 리눅스의 자원을 사용하는 것은 다음과 같이 구성할 수 있다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image12.png)

> Samba 서버를 설치하면 리눅스 컴퓨터가 Windows 컴퓨터처럼 사용된다는 의미다. 즉, 리눅스 컴퓨터가 Windows의네트워크 환경에서 Windows 컴퓨터와 동등하게 보인다.

- 이번 실습은 WinClient에서 별도로 설정할 것이 없으며, 주로 Server 쪽에서만 설정한다. 보안을위해 특별히 허가된 사용자만 접속되도록 설정하겠다.

### 실습2

Windows에서 리눅스의 자원을 사용해보자.

#### step 0

- <code>Server</code> Server를 처음 설치 상태로 초기화하자.
- 부팅하고 root 사용자로 접속하자.

#### step 1

- <code>Server</code> <b>dnf -y install samba</b> 명령으로 Samba 패키지를 설치하자.

#### step 2

Server 디렉터리를 공유하도록 설정하자.

- 먼저 Samba 의 사용이 허가된 그룹을 만들자. 여기에서는 sambaGroup으로 만들었고 디렉터리는 /share로 지정했다. 기존의 centos 사용자를 sambaGroup에 포함시킨다.

```
mkdir /share    -> 삼바로 공유할 디렉토리
groupadd sambaGroup   -> windows에서 접속을 허용할 그룹 생성
chgrp sambaGroup /share    -> 디렉토리의 소유 그룹 변경
chmod 770 /share       -> 디렉토리 허가권 변경 
usermod -G sambaGroup centos  -> centos 사용자를 sambaGroup에 소속시킴
smbpasswd -a centos     -> centos 사용자의 삼바 전용 비밀번호 지정(여기에서는 1234로 지정)
```

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image13.png)

- Samba의 설정 파일은 /etc/samba/smb.conf 다. vi나 gedit으로 열고 다음과 같이 수정하여 저장한다.

```
[global] 부분 변경
7행 수정: workgroup = WORKGROUP   -> windows의 기본 그룹명
7행 아래에 다음 추가: 
    unix charset = UTF-8    -> 문자 인코딩
	map to guest = Bad User  -> 인증 없이 접속 허용


제일 아래 추가
[Share]
  path = /share    -> 공유할 폴더
  writable = yes   -> 쓰기 허용
  guest ok = no   -> 게스트 거부
  create mode = 0777   -> 파일 전체 접근 허용
  directory mode = 0777  -> 폴더 전체 접근 허용
  valid users = @sambaGroup  -> sambaGroup 소속 사용자만 허용
```

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image14.png)

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image15.png)

> smb.conf 설정 파일의 workgroup 부분에는 Windows의 작업 그룹을 써줘야 한다. Windows에서 [제어판] → [시스템 및 보안] → [시스템]에서 확인할 수 있다.

- <b>testparm</b> 명령으로 변경한 내용에 오류가 없는지 확인한다.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image16.png)

- <b>systemctl restart/enable smb nmb</b> 명령으로 Samba 서버를 시작/상시 가동하자.

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image17.png)

- <b>firewall-config</b> 명령을 입력해 [방화벽 설정]을 실행한다. [설정]에서 [영구적]을 선택한 후 [서비스]탭에서 [samba]와 [samba-client]의 체크를 켜서 Samba 서버를 열어주자. 설정을 적용하기 위해 메뉴의 [옵션] - [Firewalld 다시 불러오기]를 선택한 후 [방화벽 설정]을 닫는다.

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image18.png)

#### step 3

<code>WinClient 또는 호스트 운영체제</code> Samba 서버 (=Server)에서 공유한 디렉터리 ('/share')에 접근하자.

- Windows 파일 탐색기를 실행하고 왼쪽에서 [내 PC]를 선택한 후 마우스 오른쪽 버튼을 눌러 [네트워크 드라이브 연결]을 선택한다. [네트워크 드라이브 연결]이 나오면 적당한 드라이브를 선택한 후 [폴더]에 직접 ‘\\10.0.5.100\share'를 입력하고 그 아래를 모두 체크한 다음 \<마침\>을 클릭하자.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image19.png)

-  [Windows 보안] 창에는 앞서 지정한 centos 사용자와 삼바 전용 비밀번호 1234를 입력하고 \<확인\>을 클릭하자.

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image20.png)

- Windows 파일 탐색기에서 확인하면 Z: 드라이브가 연결되어 있다. 파일 몇 개를 복사하자.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image21.png)


#### step 4

<code>Server</code> 파일이 잘 복사되었는지 확인하자. 

- /share 디렉터리를 확인해보자.

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image22.png)

- 현재 Samba 서버에 접속한 Windows는 <b>smbstatus</b> 명령으로 확인할 수 있다. 여기서는 10.0.2.5 컴퓨터에서 centos 사용자로 접속했다. 또 접속한 디렉터리는 /share 디렉터리를 사용했다.

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/12%EC%9D%BC%EC%B0%A8(3h)%20-%20Samba%20%EC%84%9C%EB%B2%84/images/image23.png)

- 이제 Windows에서도 리눅스의 저장 공간을 자신의 것처럼 사용할 수 있다. NFS와 차이점이라면 NFS는 리눅스(또는 유닉스) 사이에서 저장 공간을 공유하는 것이고, Samba는 리눅스(또는 유닉스)와 Windows 사이에서 저장 공간을 공유하는 것이다. 그러므로 리눅스/유닉스/Windows가 혼재된 시스템이라면 NFS와 Samba를 모두 구축하는 것이 바람직하다.

## Samba 서버 설정 파일

- 앞에서 사용해본 Samba 서버의 설정 파일은 /etc/samba/smb.conf 다. 이 파일의 문법 중 중요한 부분을 몇 가지 살펴보자.

우- 선 #과 : (세미콜론)은 주석 행을 의미한다. #은 주로 설명을 위한 주석이며 ; 은 바로 제거한 후에 사용하도록 붙인 일시적인 주석이다.

#### [global]: 모든 자원의 공유를 위한 설정

- workgroup = Windows의 작업 그룹 이름
- server string = Windows의 네트워크에 보이는 컴퓨터 설명 이름(생략가능)
- netbios name = Windows의 네트워크에 참가하는 컴퓨터 이름
- hosts allow = 삼바 서버에 접속을 허용할 컴퓨터의 IP 주소 또는 네트워크 주소 또는 컴퓨터 이름
- log file = 삼바서버에 접속하는 컴퓨터의 접속 기록 파일
- security =user(CentOS 8에 포함된 버전은 share를 허용하지 않음)

#### [공유 이름] : 공유하는 디렉터리 설정

- comment - 공유하는 디렉터리 설명. 생략 가능
- path = 물리적인 디렉터리
- read only = 디렉터리에 쓰기 권한이 있는지 여부, yes는 읽기 전용, no는 읽기/쓰기 허용
- browseable = 공유 리스트를 보여줄지 여부
- guest ok = 다른 사용자도 사용하게 할지 여부

> 이 외에 더 상세한 옵션은 <b>man smb.conf</b> 명령으로 확인해보자.

- 에디터로 직접 /etc/samba/smb.conf 파일을 수정한 후에는 문법상 오류가 없는지 체크하는 것이 좋다. 터미널에서 <b>testparm</b> 명령을 실행하면 smb.conf 파일의 오류를 검사한다.