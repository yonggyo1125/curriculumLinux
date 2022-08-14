# vsftpd 설치와 운영
- vsftpd(very Secure FTP)는 CentOS에서 기본적으로 제공되며, 리눅스와 유닉스 환경에서 보안성과 성능이 우수한 FTP 서버로 인정받고 있다. 또한 vsftpd 설치, 운영이 쉬우므로 리눅스 환경에서 FTP 서버를 운영하는 데 많이 이용된다.

- 관련 내용을 참고하거나 소스 파일을 다운로드하는 일은 http://vsftpd.beasts.org/ 에서 할 수 있으며, 여기에서는 CentOS에서 제공하는 vsftpd를 dnf 명령으로 설치한다.

### 실습1 

- vsftpd를 설치하고 운영해보자.

#### step 0

<code>Server</code> Server를 처음 설치 상태로 초기화하자.
- 부팅하고 root 사용자로 접속하자.

#### step 1

<code>Server</code> <b>dnf -y install vsftpd</b> 명령을 입력해 vsftpd 패키지를 설치하자.

#### step 2

<code>Server</code> 서비스를 가동하자.
- vsftpd에 'anonymous (익명)'로 접속되는 디렉터리는 /var/ftp/ 다. 다음 명령을 입력해 이 디렉터리 아래에 있는 /pub 디렉터리에 샘플 파일을 몇 개 복사하고 서비스를 가동하자 vsftpd 패키지의 서비스 이름도 vsftpd다.

```
cd /var/ftp
ls
cd pub
cd /boot/vmlinuz-4* file1     -> 샘플 파일 복사
ls                                    -> 복사한 샘플 파일 확인 
systemctl restart vsftdp       -> vsftpd 서비스 재가동
systemctl enable vsftpd       -> 리눅스 부팅 시 vsftpd 서비스를 자동으로 가동
```

> anonymous 사용자는 ftp 전용 사용자로 모든 리눅스에 내장된 사용자다. 특별히 암호 없이도 ftp 서버에 접속할 수 있다. 외부에서 접속할 때는 사용자 이름이 anonymous지만, 리눅스 내부에서는 ftp라는 이름으로 사용된다. 이 ftp 사용자의 디렉터리는 var/ftp며, 그래서 anonymous 사용자로 접속했을 때 접속되는 디렉터리는 /var/ftp 가 된다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image1.png)

- 외부에서 FTP 서버에 원활하게 접근할 수 있도록 <b>systemctl stop firewalld</b> 명령으로 잠시 방화벽을 꺼두자.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image2.png)

- vsftpd의 설정 파일은 /etc/vsftpd/vsftpd.conf 파일이다. vi나 gedit으로 이 파일을 열자 12행쯤에 anonymous_enable=NO로 되어 있는 부분을 YES로 변경한 후 저장한다.

> 이전 버전의 vsftpd 서버는 기본적으로 anonymous 의 접속이 허용되어 있었으나, 최근의 리눅스에서는 허용이 안 되어있다. 이는 보안 측면에서 더 도움이 된다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image3.png)

- 설정을 변경했으므로 <b>systemctl restart vsftpd</b> 명령으로 서비스를 재시작한다.

#### step 3

<code>호스트 운영체제 또는 WinClient</code> FTP 서버에 접속해서 파일을 다운로드/업로드 해본다.

- 프리웨어 FTP 클라이언트인 FileZilla를 사용해보자. http://filezilla-project.org 에 접속해 최신 Windows용 FileZilla Client를 다운로드하자.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image4.png)

> 많이 사용되는 Windows용 FTP 클라이언트 프로그램에는 알드라이브 CuteFTP, LeapFTP 등이 있다. 대부분 프리웨어가 아닌 셰어웨어이므로 회사/학교 등에서 사용할 때는 주의해야 한다.

- 설치를 진행하자. 모두 기본 설정 값으로 설치하면 된다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image5.png)

-  FileZilla 를 실행한 후 [호스트]에는 Server의 IP 주소(10.0.2.100)를 입력하고, [사용자에는 anonymous (익명 사용자) [비밀번호]에는 아무거나 입력한 후 \<빠른 연결\> 버튼을 클릭한다. [비밀번호를 기억할까요?] 창이 나오면 그냥 \<확인\>을 클릭한다. [Insecure FTP connection] 창이 나와도 \<확인\>을 클릭한다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image6.png)

- 접속된 상태는 다음과 같다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image7.png)

- 왼쪽에서 다운로드합 적당한 음마를 선택한 후, 오른쪽 리모트 사이트에서 '/pub' 디렉터리를 클릭한다. 오른쪽 아래에서 필요한 파일을 선택한 후 드래그해서 위쪽에 가지다두면 다운로드가 실행된다 또는 필요한 파일을 마우스 오른쪽 버튼으로 클리한 후 바로가기 메뉴에서 [다운로드]를 선택해도 된다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image8.png)

- 이번에는 왼쪽 로컬 컴퓨터에 있는 아무 파일이나 마우스 오른쪽 버튼으로 클락한 후 업로드를 선택하자. [550 Permission dented] 메시지가 나타나면서 업로드에 실패할 것이다. 이는 FTP 서버에서 기본적으로 다운로드만 허용될 뿐 업로드는 허용되지 않기 때문이다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image9.png)


#### step 4

<code>Server</code> 앞에서 수정했던 vsftpd의 설정 파일인 /etc/vsftpd/vsftpd.conf 파일을 수정하자.
- VI 에디터로 /etc/vsftpd/vsftpd.conf 파일을 일이 다음 내용과 같이 수정한다.

```
19행쯤 확인: write_enable=YES     -> 확인.  기본적인 업로드 허용
29행쯤: anon_upload_enable=YES   -> 주석(#) 제거(anonymous 사용자의 업로드 허용)
33행쯤: anon_mkdir_write_enable=YES    -> 주석(#) 제거(anonymous 사용자의 디렉토리 생성 허용)
```

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image10.png)

#### vsftpd.conf

vsftpd.conf 파일에서 자주 사용하는 옵션은 다음과 같다.

- anonymous_enable: anonymous(익명) 사용자의 접속을 허가할지 설정
- local_enable: 로컬 사용자의 접속 허가 여부 설정
- write_enable: 로컬 사용자가 저장, 삭제, 디렉코리 생성 등의 명령을 실행하게 할 것인지 설정(anonymous 사용자는 해당 없음)
- anon_upload_enable: anonymous 사용자의 파일 업로드 허가 여부 설정
- anon_mkdir_write_enable_anonymous: 사용자의 디렉토리 생성 허가 여부 설정
- dirlist_enable: 접속한 디렉토리의 파일 리스트를 보여줄지 설정
- download_enable: 다운로드의 허가 여부 설정
- listen_port: FTP 서비스의 포트 번호 설정(기본 21번)
- deny_file: 업로드를 금지할 파일 지정(예: deny_file={\*.mpg,\*.mpeg,\*.avi})
- hide_file: 보여주지 않을 파일 지정(예: hide_file={\*.gif,\*.jpg,\*.png})
- max_clients: FTP 서버의 동시 최대 접속자 수 지정
- max_per_ip: PC 1개가 동시에 접속할 수 있는 접속자 수 지정 

<br><br>

- 업로드할 /var/ftp/pub/ 디렉터리의 소유권도 anonymous 사용자의 접속 이름인 ftp로 바꿔야 한다. <b>chown ftp.ftp /var/ftp/pub/</b> 명령을 입력해 바꾼다. 변경 후에는 <b>systemctl restart vsftpd</b> 명령으로vsftpd 서비스를 다시 시작한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image11.png)

> chown ftp.ftp /var/ftp/pub/ 명령으로 소유권(Ownership)을 변경하는 대신 chmod 777 /var/ftp/pub/ 명령으로허가권(Permission)을 변경해도 업로드할 수 있다.

#### step 5

<code>호스트 운영체제 또는 WinClient</code> 이번에는 보안을 제외하고 연결해보자

- FileZilla를 닫은 후 다시 실행해서 왼쪽 상단의 [사이트 관리자] 아이콘을 클릭하고 \<새 사이트\>를 추가하자.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image12.png)

- \<연결\>을 클릭해서 연결한 후 Windows의 파일을 /pub 디렉터리에 마우스로 끌어다놓고 업로드해보자 잘될 것이다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image13.png)

#### step 6

- <code>호스트 운영체제 또는 WinClient</code> 이번에는 Server에 로컬 사용자로 접속해보자. 기존에 있던 centos 사용자로 FTP 접속을 시도해보자.
- FileZilla에서 centos 사용자로 접속해본다 (비밀번호도 centos 로 설정했다).

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/10%EC%9D%BC%EC%B0%A8(3h)%20-%20FTP%20%EC%84%9C%EB%B2%84/images/image14.png)

- 접속이 잘 된다. 접속이 잘 되는 이유는 vsftpd.conf에 <b>'local_enable=YES'</b>라는 행이 있기 때문이다.만약 이 행이 주석 처리되어 있다면 접속이 안 됐을 것이다.