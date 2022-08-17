# PXE 설치 서버의 개념과 구현

- PXE는 Preboot Execution Environment의 약자로, 아직 운영체제가 설치되지 않은 컴퓨터가 네트워크를 통해 PXE 서버에 접속해서 부팅되도록 해주는 인터페이스를 지칭하는 용어다. PXE 서버의 간단한 개념은 다음과 같다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image1.png)

- 실제로도 처리 과정은 간단하다.
	- ① PXE 설치 서버를 준비한다. PXE 설치 서버는 별도의 패키지가 있는 것이 아니라 IP 주소를 자동으로 할당하는 DHCP 서버, syslinux 부팅 파일을 전송할 TFTP 서버, CentOS DVD의 설치 파일을 전송할 FTP 서버 또는 웹 서버로 구성된다.
	- ② 아무것도 설치되지 않은 PC에 전원을 넣으면 자동으로 PXE 설치 서버를 찾는다. 나머지는 PXE 설치 서버에 설정한대로 설치가 자동으로 진행된다.

- 처리 과정을 살펴보면 PXE 설치 서버의 환경이 여러 개의 서버를 종합 것임을 알 수 있다. 따라서 이러한 서버들을 설정하는 것이 약간 복잡할 수 있지만, 이미 대부분 앞에서 배운 내용이므로 어렵지 않게 구축할 수 있을 것이다.

> PXE 설치를 위해서는 PXE 설치 서버와 PC가 모두 같은 네트워크 안에 있어야 한다.

### 실습1

<code>Server</code> PXE 설치 서버를 구현해보자.

#### step 0

- <code>Server</code> Server를 처음 설치 상태로 초기화하자.

- 원활한 실습을 위해 Server의 메모리 용량을 2GB (=2048MB) 이상으로 할당하자.
- 부팅하고 root 사용자로 접속한다.

#### step 1

<code>Server</code> PXE 설치 서버와 관련된 패키지를 설치하고 설정하자.

- <b>dnf -y install syslinux dhcp-server tftp-server vsftpd</b> 명령으로 관련 패키지를 설치하자. 
- 관련 포트를 열어야 하는데, 관련 포트가 여러 개이므로 <b>systemctl stop firewalld</b> 명령과 <b>systemctl disable firewalld</b> 명령으로 방화벽을 꺼두자.

- 먼저 DHCP 서버의 설정 파일인 /etc/dhcp/dhcpd.conf gedit이나 vi로 편집하자. 기존 실습에서 진행한 설정과 비슷하며, PXE 부팅을 허용하도록 추가하는 작업만 하면 된다. 이번에는 IP 주소를 10.0.2.120~199까지 할당하는 것으로 설정하자. 약 90대의 클라이언트에 IP 주소를 동시에 할당할 수 있도록 하기 위해서다.

```
subnet 10.0.2.0 netmask 255.255.255.0 {
   option routers 10.0.2.2;
   option subnet-mask 255.255.255.0;
   range dynamic-bootp 10.0.2.120 10.0.2.190;
   option domain-name-servers 10.0.2.2;
   allow booting;      -> 부팅을 허용함
   allow bootp;        -> 부팅 프로토콜을 허용함
   next-server 10.0.2.100   -> 부팅 파일이 있는 서버의 주소
   filename "pxelinux.0";    -> 부팅 파일의 이름
}
```

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image2.png)

- ftp 서버 기능을 하는 vsftpd 설정 파일인 /etc/vsftpd/vsftpd.conf 파일에서 익명(anonymous) 사용자의 접속을 허용해줘야 한다. vi나 gedit으로 /etc/vsftpd/vsftpd.conf 파일을 열고 12행쯤의 anonymous_enable=NO를 YES로 변경한다. 참고로 ftp서버는 CentOS 설치 패키지를 클라이언트에 전송하는 역할을 할 것이다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image3.png)

- tftp 서버는 클라이언트 PC에게 부팅된 파일을 전송하는 역할을 할 것이다. 역시 특별히 설정할 것은 없다.

#### step 2
<code>Server</code> CentOS ISO 파일을 ftp 서버의 홈 디렉터리인 /var/ftp 아래에 있는 /pub 디렉터리에 마운트하자.

- VirtualBox 설정에서 -> 저장소 -> CD 디스크 아이콘 선택 -> CentOS DVD ISO파일을 연결한다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image4.png)

- 잠시 기다리면 X 윈도에 자동으로 마운트될 것이다. <b>umount /dev/cdrom</b> 명령으로 마운트를 끊고 <b>mount /dev/cdrom /var/ftp/pub</b> 명령으로 새로 마운트하자 쓰기 방지와 읽기 전용으로 마운트된다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image5.png)

>DVD 복사<br>지금은 가상머신에서 실습 중이므로 DVD를 그냥 마운트해서 사용해도 되지만, 이번 장의 처음에 가정한 시나리오대로 운영하는 경우라면 DVD 장치에 동시에 100여 대의 클라이언트가 접근할 것이며, 너무 느려서 진행이 거의 되지 않을 것이다. 그러므로 다음 명령을 실행해 DVD 마운트는 다른 디렉터리에 하고 DVD의 전체 파일을 /var/ftp/pub 디렉터리에 복사해놓은 후 사용해야 한다.<br>mount /dev/cdrom /media<br>cp -r /media/\* /var/ftp/pub<br><br>가능하면 /var/ftp/pub 디렉터리는 성능이 좋은 별도의 SSD에 마운트해서 사용하는 것이 바람직하다.

#### step 3

<code>Server</code> 부팅에 필요한 파일을 준비해놓자.

- 다음 명령을 입력해 tftp 서버의 디렉터리인 /var/lib/tftpboot/ 에 DVD의 부팅 이미지 및 syslinux부팅 파일을 복사하자. 복사가 끝나면 정상적으로 복사되었는지 확인한다.

```
cd /var/ftp/pub/images/pxeboot/vmlinuz /var/lib/tftpboot/
cd /var/ftp/pub/images/pxeboot/initrd.img /var/lib/tftpboot/
cd /var/ftp/pub/isolinux/ldlinux.c32 /var/lib/tftpboot/
cp /usr/share/syslinux/pxelinux.0  /var/lib/tftpboot/
ls -l /var/lib/tftpboot/
```

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image6.png)

- 다음 명령을 입력해 /var/lib/tftpboot/ 디렉터리에 부팅 관련 디렉터리와 설정 파일을 생성하자.

```
mkdir /var/lib/tftpboot/pxelinux.cfg
cd /var/lib/tftpboot/pxelinux.cfg/
touch default
```

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image7.png)

- gedit으로 default 파일을 열고 다음 내용을 채우자.

```
DEFAULT CentOS8_Auto_Install    -> 기본 부팅 Label 지정 

Label   CentOS_Auto_Install   -> Label 시작
   kernel  vmlinuz      -> 커널 지정(/var/lib/tftpboot/ 디렉토리에 복사해둠)
   APPEND initrd=initrd.img repo=ftp://10.0.2.100/pub    -> CentOS 패키지 저장소 지정
```

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image8.png)

#### step 4

<code>Server</code> 관련된 서버를 시작하자.

- 다음 명령을 입력해 PXE 설치 서버와 관련된 dhcpd, vsftpd, tftp 서비스를 재시작하고 상시 가동(enable)하자.


```
systemctl restart dhcpd
systemctl restart vsftpd
systemctl restart tftp
systemctl enable dhcpd
systemctl enable vsftpd
systemctl enable tftp
```

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image9.png)

#### step 5

- 호스트 운영체제 VirtualBox가 제공하는 DHCP 서비스는 중지해야 한다.
- [파일] -> [환경설정] -> [네트워크] -> [활성화된 네트워크 선택] -> DHCP 지원 체크 해제

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image10.png)

#### step 6

<code>새 가상머신</code> 테스트할 가상머신을 생성하자.

- 적절하게 가상머신을 하나 만들자 OS는 Linux(RedHat 64bit),  기존과 다르게 CD항목에 Centos8 ISO는 추가하지 않는다.
- [환경설정] -> [시스템] -> [부팅순서] 에서 네트워크만 체크하고 다른 항목은 모두 해제한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image11.png)

- [환경설정] -> [네크워크] -> [고급] 에서 어탭터 종류로 Pcnet-FAST III를 선택해야 한다. Intel PRO/1000 시리즈는 PXE Boot을 지원하지 않는다. 

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image12.png)

- 가상머신을 부팅하고 잠시 기다리자. 스스로 tftp에 접속해서 파일을 다운로드할 것이다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image13.png)

- 잠시 기다리면 CentOS의 설치 화면이 나올 것이다.

- 앞서 소개한 시나리오대로라면 100대의 컴퓨터 전체에 설치를 위한 언어 선택, 디스크 파티션 설정 등의 작업을 일일이 해줘야 한다. 이러한 설정도 모두 한 번에 자동으로 진행되도록 해보자.

* * * 
# 킥스타트

- 킥스타트(Kickstart)는 레드햇이나 CentOS에서 PXE 설치 서버를 이용할 때, 부팅 후 필요한 작업까지미리 설정하여 원격 설치 시 편리하게 설치할 수 있도록 도와주는 기능이다. 그러므로 킥스타트는 PXE 설치 서버와 함께 구성해서 사용하는 것이 일반적이다. 직접 실습을 통해 확인하자.

### 실습3

#### step 0
<code>Server</code> \<실습 1\>에 이어서 한다.

#### step 1

<code>Server</code> 킥스타트 기능을 구현하자.

>  CentOS 7까지는 system-config-kickstart 패키지가 제공되어 GUI 환경으로 킥스타트를 설정할 수 있었으나, CentOS 8에서는 이 기능이 제거되었다. 좀 불편하지만 직접 텍스트 파일을 편집해야 한다.

- /root/anaconda-ks.cfg 파일은 CentOS를 설치할 때 설정한 정보가 그대로 저장되어 있다. 이 파일을 /var/ftp/centos.ks 파일로 복사하자.

```
cp /root/anaconda-ks.cfg /var/ftp/centos.ks
```

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image14.png)

- gedit이나 vi로 /var/ftp/centos.ks 를 열고 7행, 9행을 변경한 후 약 33행의 %package~%end 사이에 설치할 패키지를 지정해야 한다. 가장 큰 단위의 환경그룹은 '@^환경그룹명', 그룹은 '@그룹명', 가장 작은 단위인 패키지는 그냥 '패키지' 형식으로 추가할 수 있다. 다음 내용을 수정하고 저장하자.

> 사용 가능한 환경 그룹명 및 그룹명은  'Available Environment Groups'가 환경 그룹명이고, 'Installed Groups'와 'Available Groups'가 그룹명이다. 설치 가능한 패키지명은 dnt list 명령으로 수천 개를 확인할 수 있다.


```
22행쯤 : url --url=ftp=10.0.2.100/pub
25행쯤 : cdrom 주석(#) 처리
7~11행쯤(%package ~ %end 사이) : 기존 내요ㅕㅇ에 다음으로 변경
@^Server with GUI   -> GUI 지원 서버 환경 그룹
@GNOME Application  -> 그놈 응용 프로그램 그룹
mc                          -> 명령어 관리 패키지
```

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/images/image15.png)

- <b>chmod 644 /var/ftp/centos.ks</b> 명령으로 외부에서 읽을 수 있도록 허용하자.

- 이번에는 gedit으로 /var/lib/tftpboot/pxelinux.cfg/default 파일을 열어 마지막 행 뒤에 킥스타트설정 파일을 지정하는 ks=ftp://10.0.2.100/centos.ks'를 추가 입력한 후 저장하고 gedit을 종료하자.

#### step 2

<code>새 가상머신</code> PXE 설치 서버와 킥스타트를 테스트하자

- \<실습 1\>에서 사용한 가상머신의 하드디스크를 제거하고 새로운 하드디스크를 장착해서 사용하자. 이번에 주의할 점은 Server 가상머신이 설치된 환경의 킥스타트 파일 (anaconda-ks.cfg)을 사용했으므로, 하드디스크는 Server 가상머신과 동일한 80GB 용량의 SCSI 디스크로 장착해야 한다는 점이다.

- 부팅하자. 한동안 기다리면 아무것도 하지 않아도 설치까지 자동으로 진행될 뿐 아니라, root 암호 및 사용자(centos) 생성까지 자동으로 될 것이다.

#### step 3

- <code>호스트 운영체제</code> 실습을 모두 마쳤으면, 다시 DHCP를 활성화 한다.
