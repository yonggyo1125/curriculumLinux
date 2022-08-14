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

