# 하드디스크 한 개 추가하기

- 시스템의 하드디스크 공간이 부족할 때 가장 기본적으로 생각할 수 있는 방법은 하드디스크 1개를 추가하는 것이다. 하드디스크 1개를 추가해 사용하는 방법을 익혀보자.

- 기본적으로 우리가 운영하는 CentOS의 하드디스크는 다음과 같이 구성되어 있다. 여기에 하드디스크를 추가로 장착한 것이다. 실제 PC를 사용하는 경우는 여분의 물리 하드디스크를 장착하면 되고, 가상머신을 사용하는 경우는 실습을 통해 하드디스크를 장착해보자.

## DE 장치와 SCSI 장치 구성

- 기본적으로 우리가 운영하는 Server는 다음과 같이 구성된다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image1.png)

- 일단 상기 이미지의 기본 구성을 이해해보자. 메인보드의 IDE 0, IDE 1 슬롯(메인보드에 케이블을 꽂을 수 있는 홈이라고 생각하면 된다)에는 각각 2개의 IDE 장치를 장착할 수 있다. 그래서 IDE 장치는 총 4개를 장착할 수 있다. 이 4개의 장치를 표기할 때는 주로 IDE 0:0, 0:1, 1:0, 1:1로 표기한다.


- 상기 이미지를 보면 IDE 1:0에 CD/DVD 장치가 장착되어 있다. VirtualBox에서는 기본적으로 IDE 1:0에 CD/DVD 장치를 장착한다. 그러므로 IDE 장치 (주로 하드디스크)를 추가하려면 나머지 비어있는 3개의 장치에 장착해야 한다(하지만 우리는 IDE SATA 하드디스크가 아닌 SCSI 하드디스크를 사용할 것이다).



#### IDE/SATA/SCSI/NVMe 장치

- 일반적으로 PC에서 사용되는 하드디스크나 CD/DVD 장치가 IDE 장치(또는 EIDE 장치)나 SATA 장치라고 생각하면 된다. 서버용으로는 주로 SCSI 하드디스크를 사용하며, SSD 형태의 플래시 메모리를 사용할 수 있는 NVMe 장치도 제공된다(상기 이미지에서는 SATA와 NVMe 장치를 생략했다).

- 물론 IDE, SCSI, SATA, NVMe 모두 VirtualBox에서는 어차피 가상으로 생성하기 때문에 진짜 컴퓨터의 하드 디스크 종류와는 무관하다. 참고로 요즘에는 PC용 하드디스크나 CD/DVD 장치로 IDE 대신 SATA (Serial ATA)를 서버용으로 SCSI 대신 SA-SCSI(Serial Attached SCSI, 줄여서 SAS)를 주로 사용한다. SCSI가 최대 16개 장치를 연결할 수 있었다면, SA-SCSI는 최대 65,535개까지 연결할 수 있다.


![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image2.png)

## 하드디스크 추가하기

현재 SATA 0에 Server를 설치한 하드디스크가 1개 장착되어 있을 뿐이다. 지금부터 여기에 다음과 같이 추가 하드디스크를 새로 장착할 것이다.


![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image3.png)


- 용량이 큰 하드디스크를 장착하면 포맷하는 시간이 오래 걸리므로 작은 하드디스크(1GB)를 하나 장착한다(실제로는 가상이라서 큰 용량도 포맷이 오래 걸리지 않는다). 추가한 하드디스크의 이름은 /dev/sdb 가 된다. 추가 하드디스크 장치의 물리 이름인 /dev/sdb 를 사용하려면 최소 1개 이상의 파티션으로 나눠야 한다. 특별히 파티션을 여러 개 나눌 필요는 없으므로 1개의 파티션으로만 나눌 것이다. 그래서 논리 파티션의 이름은 상기 이미지에도 나와 있듯이 /dev/sdb1 이 된다. 
- 리눅스에서는 이 파티션을 그냥 사용할 수 없으며 반드시 특정한 디렉터리 (=폴더)에 마운트Mount시켜야 사용할 수 있다. 그래서 우리는 /mydata 라는 디렉터리를 만들고 그 디렉터리에 마운트할 것이다.

> 리눅스에서는 하드디스크 파티션뿐 아니라 CD/DVD나 USB 메모리 등도 특정 디렉터리에 마운트해야만 사용할 수 있다. 지난 실습에서 CD/DVD를 넣으면 자동으로 /run/media/root/ 디렉터리 아래에 마운트되었던 것을 확인했다. 또, 필요할 때는 별도의 디렉터리에 수동으로 마운트할 수도 있었다.

- 리눅스에서 하드디스크를 추가하는 것은 Windows처럼 간단하지 않다. 다음에 나타난 순서대로 차근차근 실습을 진행해보자.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image4.png)

## 실습1

하드디스크 1개를 장착해서 사용해보자.

### step0 

Server를 처음 설치 상태로 초기화하자

- 아직 부팅은 하지 말자.

### step1
SATA 1(/dev/sdb)에 1GB 하드디스크 하나를 장착하자.

- [설정] -> [저장소] -> [컨트롤러:SATA] -> [추가 버튼] -> [하드 디스크] 선택

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image5.png)

- [만들기] 선택

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image6.png)

- VDI(VirtualBox 디스크 이미지) 선택 하고 [다음] 클릭

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image7.png)

- [동적할당] 선택 후 [다음] 클릭

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image8.png)

- 하드디스크의 용량이 크면 파티션 구성 및 포맷을 진행할때 오랜 시간이 소요되므로 1GB 로 설정하고 [만들기]를 선택한다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image9.png)


- Not Attached(장착되지 않음) 항목에 새로 생성된 vdi 파일을 선택한 후 [선택]을 클릭한다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image10.png)

- 다음과 같이 추가된 하드디스크 이미지가 확인이 되면 [확인]을 클릭한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image11.png)

### step2

- 이제 Server를 부팅하고 root 사용자로 접속한다

### step3

- 이제는 그림의 순서대로 장착한 하드디스크에 파티션을 할당하자. 파티션은 1개의 파티션만 할당한다. 터미널을 열고 다음을 입력한다

> 파티션<br><br>하드디스크를 처음 장착하면 그냥 기계일 뿐이다. 그래서 하드디스크를 사용하려면 먼저 파티션(Partition)을 설정해야 한다. 만약 하드디스크를 통째로 하나의 파티션으로 사용하려면 1개의 파티션으로 전체를 설정하면 되고, 2개로 나눠서 사용하려면 2개의 파티션을 설정하면 된다.<br>파티션은 Primary 파티션과 Extended 파티션 두 가지가 있는데, 1개의 하드디스크는 4개의 Primary 파티션까지 설정할 수 있다. 만약 파티션을 5개 이상 설정하고 싶다면 3개의 Primary 파티션과 1개의 Extended 파티션으로 설정한 후 Extended 파티션을 2개 이상의 Logical 파티션으로 설정해야 한다.

```
# fdisk /dev/sdb  -> 하드디스크 선택
Command : n    -> 새로운 파티션 불할
Select : p    -> Primary 파티션 분할
Partition number : 1
	-> 파티션 번호 1번 선택 (Primary 파티션은 최대 4개 까지 생성 가능)
First sector: [Enter]
	-> 시작 섹터 번호 입력(1개의 파티션만 계획 중이므로 첫 섹터로 설정)
Last sector: [Enter]
	-> 마지막 섹터 번호 입력(1개의 파티션만 계획 중이므로 마지막 섹터로 설정)
	
Command : p   -> 설정된 내용 확인
Command : w   -> 설정 저장
```

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image12.png)

> CentOS 리눅스에서 섹터 하나는 512바이트로 설정되어 있다. 그러므로 512×2097152=1,024MB(=1GB)가 된다. 이는 VIrtualBox 가상 하드디스크에 적용되는 크기일 뿐, 실제 하드디스크라면 상황이 다를 수도 있다. 그리고 시작 섹터가 2048번인 이유는 제일 앞의 0~2047(=1MB) 부분이 시스템 성능 향상을 위해 사용하지 않는 부분이기 때문이다. 또 Blocks의 단위는 1KB (=1024 바이트)로 설정되어 있다.

### step 4

- 할당된 파티션 장치의 이름은 /dev/sdb1 이다. 파일 시스템을 ext4 형식으로 생성하자 (이 과정이 포맷이라고 생각하면 된다). 
- <b>mkfs -t 파일시스템 파티션장치</b> 명령을 입력하거나 간단히 <b>mkfs.파일시스템 파티션장치</b> 명령을 입력한다.

> CentOS는 ext2, ext3, ext4, xfs 파일 시스템을 사용할 수 있다. ext4 및 xfs는 ext2 ext3 파일 시스템보다 여러 면에서 향상된 파일 시스템이므로 swap을 제외하고는 ext4 xfs 파일 시스템을 사용하는 것이 바람직하다. 이 책에서 추가하는 디스크의 파일 시스템은 주로 ext4 파일 시스템을 사용한다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image13.png)

### step 5

- /dev/sdb1 파일 시스템을 사용하기 위해 디렉터리에 마운트하자.

- 먼저 <b>mkdir /mydata</b> 명령을 입력해 마운트할 /mydata 디렉터리를 만들고, <b>cp anaconda-ks.cfg /mydata/test1</b> 명령을 입력해 anaconda-ks.cfg 파일을 test1 이라는 이름의 파일로 바꿔 /mydata 디렉터리에 복사해보자(anaconda-ks.cfg 파일 대신 아무 파일이나 복사해도 상관 없다). <b>Is -I /mydata/</b> 명령을 입력하면 test1 파일을 확인할 수 있다.

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image14.png)

- /mydata 디렉터리에 있는 test1이라는 파일은 기존의 /dev/sda2 에 저장된 상태다.

- 이번에는 <b>mount /dev/sdb1 /mydata</b> 명령을 입력해 포맷이 완료된 /dev/sdb1 장치를 /mydata 디렉터리에 마운트하자 그리고 <b>Is -I /mydata/</b> 명령을 입력해 /mydata 디렉터리 안을 확인한다. 다음에는 <b>cp anaconda-ks.cfg /mydata/test2</b> 명령을 입력해 anaconda-ks.cfg 파일을 test2라는 이름의 파일로 바꿔 /mydata 디렉터리에 복사하자. 다시 <b>Is -I /mydata/</b>명령을 입력하면 test2 파일이 복사된 것을 확인할 수 있다.

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image15.png)

> lost+found 디렉터리는 fsck 등의 명령어로 파일 시스템을 점검할 때 생성되는 파일이 저장되는 곳이다. 그냥 없는 것처럼 무시해도 된다.

- 이제 /mydata 디렉터리는 /dev/sda2가 아닌 /dev/sdb1에 있다. 즉 /mydata 디렉터리에 어떤 파일을복사한다는 것은 /dev/sdb1 장치에 파일을 저장한다는 의미다. 앞에서 복사한 test2 파일은 다음과 같이 /dev/sdb1 장치에 저장되어 있다.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image16.png)

- /dev/sda2 에 있던 test1 파일은 없어진 것이 아니라 /mydata 디렉터리가 /dev/sdb1 에 마운트되어 있기때문에 잠시 /dev/sda2 에 숨어 있다고 생각하면 된다.

- <b>umount /dev/sdb1</b>명령을 입력해 /dev/sdb1 을 마운트 해제(umount)하자. 그리고 <b>ls -l /mydata</b> 명령을 입력해 test1 파일이 그대로 있는지 확인해보자.

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image17.png)

- test1 파일이 원상 복구되었다. 또한 test2 파일은 없어진 것이 아리나 /dev/sdb1 장치에 그대로 보관되어 있다. 언제든지 /dev/sdb1 을 아무 디렉토리에나 마운트하면 다시 test2 파일을 사용할 수 있다.

### step6

이번에는 컴퓨터를 켤 때 /dev/sdb1 장치가 항상 /mydata 에 마운트 되어 있도록 설정하자

- /etc/fstab 파일을 vi 에디터나 gedit로 열어서 제일 아랫부분에 다음을 추가하자

```
/dev/sdb1	/mydata	ext4	defaults	0	0
```

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image18.png)

> /etc/fstab 파일은 리눅스가 부팅될 때마다 자동으로 읽는 중요한 파일이다. 이 파일에는 마운트 정보가 수록되어 있으며,글자가 틀릴 경우 아예 부팅되지 않을 수 있으므로 수정 시 주의를 요한다.<br>6개의 필드는 장치 이름, 마운트 디렉터리, 파일 시스템, 속성, dump 사용 여부, 파일 시스템 체크 여부를 의미한다. 파일시스템과 속성을 defaults로 설정하면 읽기/쓰기/실행 등 대부분 작업이 가능하다. dump 사용 여부를 1로 설정하면 리눅스 dump 명령을 이용한 백업이 가능하다. 파일 시스템 체크 여부를 1 또는 2로 설정하면 부팅 시 이 파티션을 체크하는데.1인 파일 시스템을 먼저 체크하고 2는 1을 체크한 후에 체크한다. 3은 없다. 일반적으로 / 파일 시스템을 1로 설정하고 이외에는 2로 설정하거나 별로 중요하지 않다면 0으로 설정한다. 0으로 설정하면 파일 시스템 체크를 생략하므로 부팅 속도가향상된다.

- 수정한 /etc/fstab 파일을 저장한 후 <b>reboot</b> 명령을 입력해 재부팅시키고 root 사용자로 접속한다.
- 터미널을 열고 <b>Is -I /mydata</b> 명령을 입력해 /mydata 디렉터리를 확인하면 test2 파일을 확인할 수있다. 즉 다음 마지막 부분처럼 /dev/sdb1 장치가 자동으로 마운트되는 것이다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image19.png)

* * * 
# 여러 개 하드디스크를 하나처럼 사용하기

* * * 
# LVM

* * * 
# CenOS를 RAID에 설치하기

* * * 
# 사용자별로 공간을 할당하기