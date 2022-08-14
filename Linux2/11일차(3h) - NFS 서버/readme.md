# NFS 서버 구현

- Windows는 네트워크로 연결된 컴퓨터끼리 간단하게 폴더(디렉터리)를 공유할 수 있지만, 리눅스는 대부분 명령으로 작업을 해결해야 하기 때문에 윈도우보다는 좀 더 복잡한 과정을 거쳐야 한다. NFS의 개념은 별로 어려울 것이 없으므로 다음과 같이 직접 구현해보자.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image1.png)

- 위 그림을 보면서 구현하는 순서를 살펴보자

- (1) NFS 서버에 nfs-utils 패키지가 설치되었는지 확인한다.
- (2) NFS 서버의 /etc/exports 에 공유할 디렉터리와 접근을 허가할 컴퓨터 및 접근 권한을 지정한다. 
- (3) NFS 서비스를 실행한다.
- (4) NFS 클라이언트에 nfs-utils 패키지가 설치되었는지 확인한다.
- (5) NFS 클라이언트에서 showmount 명령을 실행해 NFS 서버에 공유된 디렉터리가 있는지 확인한다.
- (6) NFS 클라이언트에서 mount 명령을 실행해 NFS 서버에 공유된 디렉터리를 마운트한다.

- 위 그림에서 에서 주목할 점은, NFS 클라이언트는 마운트된 ~/myShare 이름의 디렉터리에 접근하면 자동으로 NFS 서버의 /share 디렉터리에 접근하는 효과를 낸다는 것이다(여기서 ~는 현재 사용자의 홈 디렉터리이므로 현재 사용자가 centos 사용자라면 /home/centos/myShare 디렉터리가 된다).

> NFS의 소스 파일 및 최신 정보를 알고 싶다면 http://nfs.sourceforge.net 을 참고하자.

### 실습1

- Server를 NFS 서버로 구축하고 Client를 NFS 클라이언트로 설정하자.

#### step 0

- <code>Server</code> Server를 처음 설치 상태로 초기화하자.
- 부팅하고 root 사용자로 접속하자.

#### step 1

- <code>Server</code> NFS 서버를 설정하자.
- <b>rpm -qa nfs-utils</b> 명령으로 NFS 서버와 관련된 'nfs-utils' 패키지가 설치됐는지 확인해본다. 만약 설치되지 않았다면 <b>dnf -y install nfs-utils</b> 명령으로 설치한다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image2.png)

- vi나 gedit으로 /etc/exports 파일을 열고 다음 내용을 넣어서 공유할 디렉터리를 추가한 후 저장하자.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image3.png)

>  위 내용의 의미는 '/share 디렉터리에 해당 IP 주소 컴퓨터가 접근할 수 있도록 하고 접근 권한은 Read와 Write 모두를 할 수 있게 하라.'다.<br>IP 주소는 모두 써도 되지만, 지금은 10.0.2.000에 해당하는 모든 컴퓨터가 접속되도록 했다. 마지막에 있는 sync는 기본 설정 값이며, NFS가 쓰기 작업을 완료할 때마다 디스크를 동기화한다. 그래서 쓰기 속도가 async보다 약간 더 느려진다. 이 옵션을 생략해도 무방하지만, nfs 서비스를 가동할 때 경고 메시지가 나오므로 쓰는 것이 깔끔하다.

#### /etc/exports 파일

```
/etc/exports 파일은 다양하게 사용될 수 있다. 형식은 다음과 같다.

       공유디렉터리      접근할 호스트IP주소또는이름(접근권한옵션)

예를 들어보면 더 쉽다.

(예1) /share 디렉터리를 10.0.2.128 컴퓨터에 읽기 전용으로 공유하라.

       /share   10.0.2.128(ro) 

(예2) /share 디렉터리를 this.com 도메인 아래의 모든 호스트에서 읽기가 가능하도록 공유하라.

       /share *.this.com(rw)

그 외에 더 세부적인 사항은 man exports 명령으로 확인하자.
```

-  /share 디렉터리를 생성하고 chmod 명령으로 /share 디렉터리의 접근 권한을 707로 한다. 당한 파일을 /share 디렉터리에 미리 몇 개 복사하자.

```
mkdir /share 
chmod 707 /share
cp /boot/vm*   /share
ls  /share
```

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image4.png)

- <b>systemctl restart nfs-server</b> 및 <b>systemctl enable nfs-server</b> 명령으로 nfs-server 서비스를 시작 및 상시 가동되도록 하자.
- <b>exportfs -v</b> 명령으로 서비스가 가동하는지 확인한다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image5.png)

> 옵션 중 별도로 지정하지 않았던 root squash라는 것이 보인다. 이는 NFS 클라이언트가 root라는 이름으로 NFS 서버에 접속하더라도 NFS 서버의 root 사용자 권한은 얻을 수 없도록 방지하는 기본 설정 옵션이다. 만약 별도로 no_root_squash 옵션을 사용하고자 한다면 사설 네트워크 환경에서만 사용하는 것이 바람직하다. 보안상 문제가 있을 수 있다.

- <b>systemctl stop firewalld</b> 명령으로 방화벽을 잠깐 끄자.

> NFS 서버는 보안에 좀 취약한 편이라서 일일이 보안 관련 설정을 하는 것이 좋다. 하지만 지금 실습은 회사 내부의 인트라넷이라는 가정이므로 보안 관련 설정은 무시하고 넘어간다.

#### step 2

<code>Client</code> NFS 서버에 접속해서 공유한 디렉터리를 사용해보자.

- <b>rpm -qa nfs-utils</b> 명령으로 관련 패키지가 설치되었는지 확인하자. 설치되어 있을 것이다.
- 우선 <b>showmount -e NFS서버IP주소</b> 명령으로 NFS 서버에 공유된 디렉터리를 확인해보자.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image6.png)

- 다음 명령을 참고해 NFS 서버의 /share 디렉터리에 마운트할 디렉터리 /home/centos/myShare 를만들고 마운트하자.

```
cd   -> centos 사용자의 홈 디렉터리(/home/centos)로 이동
mkdir myShare
su -c 'mount -t nfs NFS서버IP주소:서버공유디렉토리 클라이언트마운트디렉토리'
```

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image7.png)

- 이제 ~/myShare 디렉터리를 사용한다는 의미는 NFS 서버의 /share 디렉터리를 사용한다는 것과 같다. /share 디렉터리를 읽기 및 쓰기로 공유했므로 적당한 파일을 복사해보자.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image8.png)

#### step 3

<code>Client</code> NFS 클라이언트가 부팅될 때마다 NFS 서버의 디렉터리에 자동으로 마운트되도록 하자.

- 우선 <b>su</b> 명령을 입력해 root 사용자로 접속한다.
- gedit으로 /etc/fstab 파일을 열고 맨 아래 줄에 다음 내용을 추가한다

```
NFS서버IP:서버공유디렉토리   클라이언트마운트디렉토리  nfs   defaults   0  0
```

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image9.png)

- Client를 재부팅한 후 <b>Is -I /home/centos/myShare</b> 명령으로 자동 마운트되었는지 확인한다. 그리고 <b>touch /home/centos/myShare/newFile</b> 명령으로 읽기/쓰기 작업이 되는지 확인하자.

#### step 4

- <code>WinClient</code> 리눅스에서 공유한 NFS 서버 디렉터리를 윈도우에서 접근해보자.

- [제어판]의 [프로그램] → [Windows 기능 켜기/끄기]에서 [NFS 서비스] → [NFS 클라이언트]의 체크를 켜고 \<확인\>을 클릭해 설치하자. 만약 다시 시작하라는 메시지가 나오면 WinClient를 다시 시작한다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/11%EC%9D%BC%EC%B0%A8(3h)%20-%20NFS%20%EC%84%9C%EB%B2%84/images/image10.png)


- 명령 프롬프트에서 <b>mount NFS서버IP주소:서버공유디렉터리 \*</b> 명령으로 NFS 서버에 접속하자 (파워셸인 경우 cmd 명령을 입력하면 명령 프롬프트로 전환된다).

```
mount 10.0.2.100:/share *
```



- 자동으로 Z: 드라이브가 생성되면서 접속된다. 파일 탐색기를 열고 확인해보자. 파일 읽기/쓰기가 가능할 것이다.






