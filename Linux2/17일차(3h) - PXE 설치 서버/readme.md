# PXE 설치 서버의 개념과 구현

- PXE는 Preboot Execution Environment의 약자로, 아직 운영체제가 설치되지 않은 컴퓨터가 네트워크를 통해 PXE 서버에 접속해서 부팅되도록 해주는 인터페이스를 지칭하는 용어다. PXE 서버의 간단한 개념은 다음과 같다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image1.png)

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

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image2.png)

- ftp 서버 기능을 하는 vsftpd 설정 파일인 /etc/vsftpd/vsftpd.conf 파일에서 익명(anonymous) 사용자의 접속을 허용해줘야 한다. vi나 gedit으로 /etc/vsftpd/vsftpd.conf 파일을 열고 12행쯤의 anonymous_enable=NO를 YES로 변경한다. 참고로 ftp서버는 CentOS 설치 패키지를 클라이언트에 전송하는 역할을 할 것이다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image3.png)

- tftp 서버는 클라이언트 PC에게 부팅된 파일을 전송하는 역할을 할 것이다. 역시 특별히 설정할 것은 없다.

#### step 2
<code>Server</code> CentOS ISO 파일을 ftp 서버의 홈 디렉터리인 /var/ftp 아래에 있는 /pub 디렉터리에 마운트하자.

- VirtualBox 설정에서 -> 저장소 -> CD 디스크 아이콘 선택 -> CentOS DVD ISO파일을 연결한다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image4.png)

- 잠시 기다리면 X 윈도에 자동으로 마운트될 것이다. <b>umount /dev/cdrom</b> 명령으로 마운트를 끊고 <b>mount /dev/cdrom /var/ftp/pub</b> 명령으로 새로 마운트하자 쓰기 방지와 읽기 전용으로 마운트된다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image5.png)

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

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image6.png)

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

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image8.png)

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

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/17%EC%9D%BC%EC%B0%A8(3h)%20-%20PXE%20%EC%84%A4%EC%B9%98%20%EC%84%9C%EB%B2%84/image9.png)

#### step 5

호스트 운영체제 VirtualBox가 제공하는 DHCP 서비스는 중지해야 한다.
