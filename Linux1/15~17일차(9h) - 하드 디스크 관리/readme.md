# 하드디스크 한 개 추가하기

- 시스템의 하드디스크 공간이 부족할 때 가장 기본적으로 생각할 수 있는 방법은 하드디스크 1개를 추가하는 것이다. 하드디스크 1개를 추가해 사용하는 방법을 익혀보자.

- 기본적으로 우리가 운영하는 CentOS의 하드디스크는 다음과 같이 구성되어 있다. 여기에 하드디스크를 추가로 장착한 것이다. 실제 PC를 사용하는 경우는 여분의 물리 하드디스크를 장착하면 되고, 가상머신을 사용하는 경우는 실습을 통해 하드디스크를 장착해보자.

## IDE 장치와 SCSI 장치 구성

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

- 시스템 관리자라고 가정해보자. 회사 시스템의 저장공간이 부족하다면 아마도 구매 담당 부서에 하드디스크 구매를 요청할 것이고, 구매 담당자는 요구한 용량의 하드디스크를 구매해서 시스템 관리자에게 전달할 것이다. 그런데 40TB (1TB=1,024GB) 용량을 요청했는데,하드디스크는 10TB 2개와 20TB 1개가 들어왔다. 그러나 시스템 관리자는 40TB 하나를 추가하기를 원했던 것이다.

- 하드디스크 3개를 사용하면 불편한 점이 발생한다. 총 용량은 40TB지만 각 하드디스크의 용량을넘지 않도록 파일을 잘 분배해야 한다. 그렇지 않아도 해야 할 일이 많은 리눅스 시스템 관리인데 할일이 하나 더 생긴 것이다. 이럴 땐 차라리 누가 하드디스크 3개를 40TB 하드디스크 하나로 바꿔준다면 당장 그렇게 할 것이다.

- 이번에는 여러 개의 하드디스크를 하나의 하드디스크처럼 사용할 수 있는 RAID와 LVM에 대해 학습해보자.

## RAID의 정의와 개념

- 서버 컴퓨터의 저장 장치 대부분은 하드웨어 RAID 또는 소프트웨어 RAID 방식을 사용한다. 그렇다면 RAID가 무엇인지, 그리고 왜 필요한지 파악해보자.


- RAID(Redundant Array of Inexpensive/Independent Disks)는 여러 개의 하드디스크를 하나의 하드디스크처럼 사용하는 방식이다. 비용을 절감하면서도 신뢰성을 높이며 성능까지 향상시킬 수 있다. RAID의 종류는 크게 하드웨어 RAID와 소프트웨어 RAID로 나눌 수 있다.

### 하드웨어 RAID

- 하드웨어 RAID는 하드웨어 제조업체에서 여러 개의 하드디스크를 연결한 장비를 만들어 그 자체를공급하는 것이다. 
- 하드웨어 RAID는 좀 더 안정적이고 각 제조업체에서 기술 지원을 받을 수 있기에 많이 선호하는 방법이다. 
- 최근에는 저렴한 가격의 제품도 출시되고 있지만, 안정적이고 성능 좋은 제품은 상당히 고가다. 
- 대개 하드웨어 RAID는 고가의 경우 SA-SCSI 하드디스크를, 중저가는 SATA 하드디스크를 사용해 만들어진다. 하드웨어 RAID는 각 제조업체에 따라 조작 방법이 다를수 있다.

### 소프트웨어 RAID

- 고가 하드웨어 RAID의 대안으로, 하드디스크만 여러 개 있으면 운영체제에서 지원하는 방식으로 RAID를 구성하는 방법을 말한다. 

- 하드웨어 RAID와 비교하면 신뢰성이나 속도 등이 떨어질 수 있지만, 아주 저렴한 비용으로 좀 더 안전하게 데이터를 저장할 수 있다는 점에서 적극 고려해볼 수 있는 방식이다. 앞으로 소개하는 방식은 모두 소프트웨어 RAID 방식이지만, 하드웨어 RAID도 같은개념으로 하드웨어에 구현한 것일 뿐 별반 다르지 않다.

## RAID 레벨

- RAID는 기본적으로 구성 방식에 따라 Linear RAID, RAID 0, RAID 1, RAID 2, RAID 3,RAID 4, RAID 5의 일곱 가지로 분류할 수 있다. 
- 실무에서 주로 사용하는 방식은 Linear RAID, RAID 0, RAID 1, RAID 5와 RAID 5의 변형인 RAID 6, 그리고 RAID 1과 0의 혼합인 RAID1+0 등이다. 
- 여기서는 실제로 많이 사용하는 구성 방식 위주로 살펴본다. 앞에서 실습했던 단순 볼륨과 많이 쓰이는 RAID 방식인 Linear RAID, RAID 0, RAID 1, RAID 5, RAID 6을 비교하면 다음과 같다.

#### 각 RAID 방식 비교

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image20.png)

### 단순 볼륨

- 하드디스크 하나를 볼륨(Volumn - 묶음) 하나로 사용하는 방법이며 RAID 방식에는 포함되지 않는다. 

### Linear RAID와 RAID 0

- 두 방식 모두 최소 2개의 하드디스크가 필요하다. 2개 이상의 하드디스크를 1개의 볼륨으로 사용한다는 점은 비슷해 보인다. 하지만 가장 큰 차이점은 저장 방식이다.

- 다음의 예를 보면, Linear RAID 방식은 2개 이상의 하드디스크를 1개의 볼륨으로 사용하며 파일이 저장되는 방식은 앞 하드디스크에 데이터가 완전히 저장된 후 다음 하드디스크에 데이터를 저장한다. 즉, 앞 하드디스크에 데이터가 완전히 저장되지 않으면 다음 하드디스크는 전혀 사용되지 않는 것이다.

- 이와 달리 RAID 0 방식은 모든 하드디스크를 동시에 사용한다. 3개의 하드디스크를 사용할 경우를 단순화한 예를 들면, “안녕하세요?우재남입니다" (12바이트라고 가정하자)라는 내용은 다음과 같은 방식으로 저장된다.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image21.png)

- Linear RAID는 1번째 하드디스크가 모두 채워진 후에 2번째 하드디스크를 사용하기 시작한다. 이와 달리 RAID 0은 1번째, 2번째, 3번째 하드디스크에 동시에 저장된다. 위 이미지와 같이 '안'은 1번째에, ‘녕’은 2번째에, '하'는 3번째에 저장되는 식으로 '동시에 저장되는 것이다.

> 실제로는 bit 단위 또는 블록 단위로 저장되지만 쉽게 이해하기 위해 글자 1개씩 저장된다고 가정한다.

- 여기서 '동시에'라는 말은 중요한 의미를 갖는다. Linear RAID에서 "안녕하세요?우재남입니다”가 저장되는 시간이 한글자당 1초라고 가정한다면 Linear RAID의 경우 저장되는 데 총 12초의 시간이 소요된다. 
- 하지만 RAID 0의 경우에는 동시에 하드디스크 3개를 사용하므로 각 하드디스크당 4글자만 저장된다. 즉, 4초면 저장이 완료된다.
-  이렇게 여러 개의 하드디스크에 동시에 저장되는 방식을 '스트라이핑 Stripping' 방식이라고 부른다.

- 물론 저장되는 시간은 하드디스크말고도 컴퓨터 시스템에 존재하는 여러 부분의 성능과 관련이 있지만 저장되는 시간 효율이 Linear RAID와 비교했을 때 획기적으로 향상되는 것은 확실하다.

- 이처럼 RAID 0 방식은 저장되는 시간 또는 속도 면에서 RAID 방식 중 성능이 가장 뛰어나다고 할 수 있다. 또 하드디스크 개수가 가진 총 용량을 모두 사용하므로 공간 효율이 아주 좋다. 즉 1TB 3개를 사용하면 총 3TB 의 용량을 사용할 수 있으므로 100%의 공간 효율성을 가진다.

- 이번에는 단점을 살펴보자. RAID 0 의 경우 3개의 하드디스크 중 하나가 고장 나면 어떤 문제가 발생할까? 답은 모든 데이터를 잃어버린다는 것이다. 예를 들어 두 번째 하드디스크가 고장 났다고 생각하고 글자를 읽으면 "안X하세X?우X남입X다"가 될 것이다. 컴퓨터는 이를 가지고 원래의 데이터가 무엇인지 예측할 수 없다. 즉 전혀 쓸모 없는 데이터가 되는 것이다.

- 그러므로 RAID 0 방식을 사용하는 데이터는 '빠른 성능을 요구하되, 혹시 전부 잃어버려도 큰 문제가 되지 않는 자료'를 저장하는 데 적절한 방식이라고 생각할 수 있다.

> 100개의 하드디스크로 RAID O 방식을 구성한다고 가정했을 때, 단순히 계산하면 저장 속도는 100배 빨라질 수 있다. 그러나 하드디스크도 기계이므로 언제든 고장 날 수 있다. 즉 하드디스크 100개 중 하나라도 고장 난다면 저장된 데이터가 모두 없어지는 것과 마찬가지다. 결국 여러 개의 하드디스크로 RAID 0을 구성하면 저장 속도(=성능)는 빨라지지만 데이터의 위험성은 더 증가한다.

- Linear RAID의 장점은 각 하드디스크의 용량이 달라도 전체 용량을 문제 없이 사용할 수 있어 공간 효율성이 100%라는 것이다. RAID 0이라면 100TB와 1TB 하드디스크 2개로 구성했을 때 사용할 수 있는 총 용량은 2TB 밖에 되지 않는다. 저장 속도를 높이려고 언제나 데이터를 나눠서 각 하드디스크에 동시에 저장하도록 설계했기 때문이다. 즉 작은 1TB 하드디스크가 꽉 차면 큰 쪽의 나머지 99TB는 사용할 수 없으므로 1TB짜리 2개로 구성하는 것과 동일하다. 하지만 Linear RAID는 1번째 하드디스크부터 순차적으로 데이터를 저장하기 때문에 총 용량이 101TB가 된다. 

> Linear RAID를 구성할 때를 제외하고 나머지 RAID 0, 1, 5, 6, 10을 구성할 때는 일반적으로 동일한 용량의 하드디스크를 사용한다. 또 가능하면 모든 하드디스크를 동일한 회사의 동일 모델로 구성하는 것이 RAID를 좀 더 안정적으로 구성하는데 도움이 된다.

### RAID 1

- RAID 1 방식의 핵심은 '미러링(Mirroring)'이라고 할 수 있다. 즉 똑같은 데이터의 거울을 만들어놓는 것이다. 예를 들어 하드디스크 2개를 RAID 1 방식으로 구성한 후 "안녕하세요?우재남입니다"를 저장하면 다음과와 같다. 그런데 12바이트를 저장하는 데는 2배의 용량인 24 바이트가 소요됐음을 확인할 수 있다. 
- 즉, 데이터를 저장하는 데 2배의 용량을 사용한다. 이 말은 결국 총 하드디스크 용량의 절반밖에 사용하지 못한다는 말과 같다.

#### RAID 1의 저장 방식

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image22.png)

- RAID 1의 장점은 2개의 하드디스크 중 하나가 고장 나도 데이터가 손상되지 않는다는 것이다. 이것을 '결함 허용 Fault-tolerance을 제공한다'라고 표현한다. 
- 반대로 단점은 실제 계획보다 2배 큰 저장 공간이 필요하다는 것이다(즉, 비용이 두 배로 든다). RAID 1의 경우 총 2TB 중 1TB에 저장된 내용만 사용하므로 공간 효율이 50%밖에 되지 않는다. 이를 '공간 효율이 떨어진다'라고도 표현한다.

- RAID 1 방식을 사용하는 데 적당한 경우는 '하드디스크가 고장 나도 없어져서는 안 될 중요한 데이터'가 있을 때라고 생각하면 된다. 즉 비용이 많이 들더라도 중요도가 높은 데이터들을 저장할 때 사용한다.

- 이번에는 저장 속도를 생각해보자. 똑같은 데이터를 2번 저장하므로 2배의 시간이 걸린다고 생각할 수 있지만, 똑같은 데이터가 다른 하드디스크에 동시에 저장되는 것이므로 저장 속도는 빠르지도 느리지도 않다. 이 예에서 12바이트를 저장하는 데 12초가 걸린다면, 각각 저장되는 것이므로 총 12초의 시간이 걸린다고 할 수 있다.

### RAID 5

#### RAID 0과 RAID 1 비교

||RAID 0|RAID 1|
|----|----|----|
|성능(속도)|뛰어남|변화 없음|
|데이터 안정성(결함 허용)|보장 못함(결함 허용 X)|보장함(결함 허용 O)|
|공간 효율성|좋음|나쁨|

- 각각의 장점이 명확하다. 그래서 RAID 1처럼 데이터의 안전성이 어느 정도 보장되면서 RAID 0처럼 공간 효율성도 좋은 방식을 요구하게 되었다. 이를 어느 정도 포용하는 방식이 RAID 5다.
- RAID 5는 최소한 3개 이상의 하드디스크가 있어야 구성할 수 있으며 대부분 5개 이상의 하드디스크로 구성한다. 하드디스크에 오류가 발생하면 패리티(Parity)를 이용해서 데이터를 복구할 수 있다. 예를 들어보자. 이번에는 '000 111 010 011'이라는 12bit 데이터를 4개의 하드디스크로 구성된 RAID 5에 저장해본다.

#### RAID 5의 저장 방식1

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image23.png)

- 네모로 표시된 데이터는 패리티 데이터다. 각 행에 하나씩 패리티 데이터를 사용하며 첫 번째 행은 sdd, 두 번째 행은 sdc, 3번째 행은 sdb와 같은 순서로 패리티 사용 공간을 비워놓는다. 
- 처음 3bit인 000을 저장할 때는 sda에 0, sdb에 0, sdc에 0을 저장하고 sdd에는 패리티를 저장할 공간으로 비워둔다. 
- 두 번째 3bit인 111 을 저장할 때는 sda에 1, sdb에 1,  sdc는 패리티 데이터로 비워 두고 sdd에 1을 저장한다. 이렇게 데이터를 저장한 상태가 위 이미지이다. 이제는 다음을 살펴보자. 이 예의 경우 짝수 페리티를 사용했는데, 짝수 패리티란 각 행이 짝수가 되게 만들려고 숫자를 채워 넣는 것이다.

#### RAID 5의 저장 방식2

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image24.png)

- 짝수 패리티를 사용하기로 했으므로 첫 행의 '0+0+0+Parity'는 짝수가 되어야 한다. 그러므로 첫 행의 패리티는 0이 입력된다. 두 번째 행도 '1+1+Parity+1=짝수이므로 패리티는 1이 된다. 세 번째 010과 네 번째 011도 마찬가지다. 
- 이렇게 저장이 완료된 RAID 5는 어느 정도의 결함을 허용한다. 네 개의 하드디스크 중 1개가 고장 나도 원래의 데이터를 추출할 수 있는 것이다. 이번에는 두 번째 하드디스크인 sdb가 고장 났다고 가정하고 sdb 의 데이터 저장 상태를 유추해 보자.

#### 하드디스크 하나가 고장 났을 때 RAID 5가 복구하는 방식

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image25.png)

- 첫 행을 보면 현재 sda는 0, sdb는 알 수 없음, sdc는 0, sdd는 0이 들어 있다. '0+알수없음+0+0=짝수'여야 하므로 알 수 없는 sdb의 값은 0이 된다는 것을 예측할 수 있다. 나머지도 마찬가지로 유추해보면 sdb에 들어 있던 원래 값이 0110이라는 것을 알 수 있으므로 원래의 데이터를 손실 없이 사용할 수 있다.

- RAID 5의 장점은 어느 정도의 결함을 허용하며 저장 공간 효율도 좋다는 것이다. 각 하드디스크의 용량이 1TB 라고 가정하면, 총 사용할 수 있는 공간은 3TB로 전체 용량의 75%다. 만약 RAID 5를 하드디스크 10개로 구성했다면, 전체 10TB 중 1개의 패리티로 사용하는 1TB 용량을 제외하고 나머지 9TB를 사용할 수 있으므로 전체 용량의 90%를 사용할 수 있다 (하드디스크의 개수를 N개라고 하면, N-1만큼의 공간을 사용할 수 있다). 그러므로 여러 개의 하드디스크로 RAID 5를 구성할수록 저장 공간의 효율을 높일 수 있다.

### RAID 6

- RAID 5 방식을 사용할 때는 하드디스크 1개가 고장 나도 데이터에 이상이 없다는 것을 확인했다. 그렇다면 10개의 하드디스크로 RAID 5를 구성할 때 2개의 하드디스크가 동시에 고장 난다면 어떻게 될까? 불행히도 모든 데이터를 전혀 복구할 수 없게 된다. 이런 경우 여러 개의 하드디스크로 RAID 5를 구성할 때 아무래도 신뢰성을 좀 더 높이고 싶을 것이다.

- RAID 6 방식은 RAID 5 방식이 개선된 것으로, RAID 5는 1개의 패리티를 사용하지만 RAID 6은 2개의 패리티를 사용한다. 공간 효율은 RAID 5보다 약간 낮지만, 2개의 하드디스크가 동시에 고장나도 데이터에는 이상이 없도록 한다.

- 10개의 하드디스크로 RAID 6을 구성할 때 1개당 1TB라고 가정한다면 '하드디스크 개수-2'인 8TB의 용량을 사용할 수 있다. RAID 5의 경우 최소 3개의 하드디스크로 구성해야 했지만, RAID은 최소 4개의 하드디스크로 구성해야 한다는 점도 기억하자.

- 결론적으로 RAID 6은 공간 효율이 RAID 5보다 약간 낮은 반면, 데이터의 신뢰도는 더욱 높아지는 효과를 갖는다. 또 RAID 5는 패리티를 1개만 생성하면 되지만, RAID 6은 패리티를 2개 생성해야 하므로 내부적인 쓰기 Write 알고리즘이 복잡해져 RAID 5와 비교했을 때 성능(속도)이 약간 떨어진다.

### 그 외 RAID를 조합하는 방법

- 앞에서 익힌 기본적인 RAID 방식을 조합해서 구성할 수도 있다. 그중 많이 사용하는 예로 RAID1+0 방식이 있다. 
- RAID 1(Mirroring)로 구성한 데이터를 다시 RAID 0(Stripping)으로 구성하는 방법이다. 
- 신뢰성(안전성)과 성능(속도)을 동시에 확보할 수 있다.

#### RAID 1+0의 저장 방식

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image26.png)

- RAID 1+0 방식은 전체 12글자(12바이트)를 저장하는 데 각 하드디스크당 6글자만 저장하면 되므로 총 6초밖에 걸리지 않았다. 
- 또 왼쪽 RAID 1과 오른쪽 RAID 1에서 각각 하드디스크가 1개씩 고장 나도 데이터는 안전하므로 신뢰성 (안정성)까지 얻을 수 있다. 이 외에도 아주 중요한 데이터일 경우 RAID 1+6 방식을 사용할 수도 있다.

##  Linear RAID, RAID 0, RAID 1, RAID 5 구현

이번 실습에서는 다음과 같은 하드웨어 환경을 구축한다. 9개의 SCSI 하드디스크를 장착하고 Linear RAID (/dev/sdb, /dev/sdc), RAID 0(/dev/sdd, /dev/sde), RAID 1 (/dev/sdf, /dev/sdg), RAID 5 (/dev/sdh, /dev/sdi, /dev/sdj) 를 구현할 것이다.

#### RAID 실습을 위한 하드웨어 구성도

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image27.png)

## 실습2

- RAID를 실습하기 위해 9개의 하드디스크를 장착한 가상머신 환경을 만들자.

### step0

- Server를 처음 설치 상태로 초기화하자 
- 아직 부팅은 하지 말자.

### step1

- 다음과 같이 하드디스크 9개를 추가하자.

<table>
	<thead>
		<tr>
			<th>하드디스크 크기</th>
			<th>비고</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>2GB</td>
			<td rowspan='2'>Linear RAID</td>
		</tr>
		<tr>
			<td>1GB</td>
		</tr>
		<tr>
			<td>1GB</td>
			<td rowspan='2'>RAID 0</td>
		</tr>
		<tr>
			<td>1GB</td>
		</tr>
		<tr>
			<td>1GB</td>
			<td rowspan='2'>RAID 1</td>
		</tr>
		<tr>
			<td>1GB</td>
		</tr>
		<tr>
			<td>1GB</td>
			<td rowspan='3'>RAID5</td>
		</tr>
		<tr>
			<td>1GB</td>
		</tr>
		<tr>
			<td>1GB</td>
		</tr>
	</tbody>
</table>

- [설정 ] -> [저장소]를 클릭한다.
- [컨트롤러: IDE]를 클릭하고 오른쪽의 [속성] - [종류]를 virtio-scsi로 변경한다.
- [컨트롤러: IDE]의 [하드디스크 추가 아이콘] 클릭하고 만들기를 클릭하고 위 표를 참고해서 총 9개의 하드디스크를 추가한다.

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image28.png)

### step2

하드디스크를 확인하자

-  부팅하고 root 사용자로 접속한 후 터미널을 하나 연다. 
- 터미널에서 <b>Is -I /dev/sd\*</b> 명령을 입력해 조금 전 장착한 SCSI 장치가 /dev 디렉터리에 있는지 확인해본다

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image29.png)

- 원래 CentOS가 설치된 /dev/sda를 제외하고 /dev/sdb ~ /dev/sdj 까지 9개의 장치를 확인할 수 있다.


### step3
지금 장착한 /dev/sdb ~ /dev/sdj의 하드디스크 9개는 앞으로 RAID용으로 계속 사용할 것이다. 그러므로 fdisk 명령어로 9개의 하드디스크 모두를 RAID용 파티션으로 만들면 앞으로 편리하게 실습할 수 있
 
 - <b>fdisk /dev/sdb</b> 명령을 입력해 /dev/sdb 장치에 /dev/sdb1 파티션을 생성한다. 앞의 \<실습 1\>에서는 파일 시스템 유형을 별도로 지정하지 않았다. 그럴 경우 CentOS는 자동으로 83(Linux)라는 파일 시스템을 지정해준다. 이번 실습은 RAID 실습이므로 별도로 fd (Linux raid autodetect)라는 파일 시스템을 지정해야 한다.

```
# fdisk /dev/sdb
# Command : n   -> 새로운 파티션 분할
# Select : p   -> Primary 파티션 선택
# Partition number : 1   -> 파티션 번호 1번 선택
# First sector : [Enter]  -> 시작 섹터 번호
# Last sector : [Enter]  -> 마지막 섹터 번호
# Command : t       -> 파일 시스템 유형 선택
# Hex Code : fd      
	-> 'Linux raid auto detect' 유형 번호(L을 입력하면 전체 유형이 출력됨)
Command : p   -> 설정 내용 확인
Command : w   -> 설정 저장
```

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image30.png)

- 계속 <b>fdisk /dev/sdc</b>부터 <b>fdisk /dev/sdj</b> 명령까지 입력해 나머지 하드디스크 8개의 파티션을 생성한다.

- 9개의 하드디스크 파티션이 모두 만들어졌으면 <b>Is /dev/sd\*</b> 명령을 입력해 확인해보자.

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image31.png)

- 이제 추가한 9개의 하드디스크를 이용해서 RAID를 구축해보겠다.

### step4

지금까지 설정한 내용을 스냅샷으로 저장하자.

- <b>halt -p</b> 명령으로 VirtualBox를 종료한다.
- '9개 하드디스크 파티션 완료' 이름으로 현재 상태를 스냅숏한다.

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image32.png)

### Linear RAID 구축

- 준비가 완료되었다면 본격적으로 RAID 장치를 만들어보자. 우선 다음의 순서를 참고해 Linear RAID를 만들어보겠다.

#### Linear RAID 구축 순서

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image33.png)

### 실습3

Linear RAID를 구성해 보자.  /dev/sdb, /dev/sdc 로 구성한다.

#### step0

- \<실습 2\>에 이어서 진행해야 한다.
- 부팅하고 root로 접속한다.

#### step1

상기 이미지에서 나온 선처리 작업을 먼저 한다.

- fdisk는 \<실습 1\>에서 이미 했으므로 <b>fdisk -I /dev/sdb; fdisk -l /dev/sdc</b> 명령을 입력해 확인만 하자.

> fdisk 명령어의 옵션은 파티션 상태를 화면에 출력해준다. 그리고 명령어 사이를 세미콜론(;)으로 구분했는데, 명령을 연속으로 실행할 때 사용한다.

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image34.png)

#### step2

mdadm 명령어를 사용해서 실제 RAID를 구성하자.

- /dev/sdb1 과 /dev/sdc1 Linear RAID 장치인 /dev/md9 로 생성하고, 잘 생성되었는지 확인해본다. 

```
mdadm --create .dev/md9 --level=linear ---raid=devices=2 /dev/sdb1 /dev/sdc1
	-> RAID 생성
mdadm --detail --scan	-> RAID 확인
```

> /dev/md9 장치는 Linear RAID 장치로 사용하려고 임의로 지정한 이름이다. Linear RAID는 md9로 RAID 0은 md0으로 RAID 1은 md1로 RAID 5는 md5로 지정하겠다. 그러면 md?의 이름만으로도 어떤 RAID 장치인지 쉽게 구분할 수 있을 것이다. 단, Linear 특별히 번호가 없어서 비어 있는 9번을 사용했다.

![image35](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image35.png)

- mdadm 명령
	- mdadm 명령은 CentOS에서 RAID 장치를 생성/관리하는 명령어다. 이 명령의 옵션이 갖는 의미는 다음과같다.
		- <b> --create /dev/md9</b> : md9 장치에 RAID 생성
		- <b> --level=linear</b> : Linear RAID 지정. 0은 RAID 0, 1은 RAID 1 등으로 지정
		- <b> --raid-devices=2 /dev/sdb1 /dev/sdc1</b> : 2개의 하드디스크를 사용하며, 이어서 나오는 것이 장치 이름

	- 그 외에도 자주 사용되는 명령은 다음과 같다.
		- <b>mdadm --stop /dev/md9</b> : RAID 장치인 /dev/md9 중지
		- <b>mdadm --run /dev/md9</b> : 중지된 RAID 장치 가동
		- <b>mdadm --detail /dev/md9</b> : /dev/md9 장치의 상세 내역 출력
	- 더 상세한 내용은 <b>man mdadm</b> 명령으로 살펴보자
	
- <b>mkfs.ext4 /dev/md9</b> 또는 <b>mkfs -t ext4 /dev/md9/</b> 명령을 입력해 /dev/md9 파티션 장치의 파일 시스템을 생성한다. 즉, 포맷하는 과정이다.
	
![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image36.png)

- <b>mkdir /raidLinear</b> 명령을 입력해 마운트할 디렉터리(/raidLinear)를 생성하고 <b>mount /dev/md9 /raidLinear</b> 명령을 입력해 마운트시킨다. 
- <b>df</b> 명령을 입력해서 확인해보면 /raidLinear 디렉터리에 약 2.8GB 가량 여유 공간이 있음을 확인할 수 있다. 
- /dev/sdb 는 2GB, /dev/sdc 는 1GB 용량이므로 LinearRAID는 2개의 하드디스크 용량을 모두 사용하기 때문에 3GB 정도가 나왔다.

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image37.png)

- 이번에는 컴퓨터를 켤 때 언제든지 /dev/md9 장치가 /raidLinear 디렉터리에 마운트되어 있도록 설정하자. /etc/fstab 파일을 vi 에디터나 gedit으로 열어서 아랫부분에 다음을 추가하고 저장하자.

```
/dev/md9    /raidLinear    ext4    defaults     0 0
```

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image38.png)

### step3

- <b>mdadm --detail /dev/md9</b> 명령을 입력해 구축한 Linear RAID를 자세히 확인해보자.

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image39.png)

- /dev/md9 의 상세 내용이 나온다. RAID Level은 linear, Array Size(용량)은 3GB, Raid Devices(장치 개수)는 2개다.
- 현재 작동 중인 장치(하드디스크)는 2개며, 맨 아래에는 장치의 상세한 내용과 함께 /dev/sdb1 과 /dev/sdc1 을 사용하는 내용이 출력된다.

### RAID 0 구축

- 이번에는 앞에서 구성한 Linear RAID와 거의 비슷한 방법으로 RAID 0을 구성해본다.  차이점은 RAID 장치를 /dev/md0 으로 사용하는 것과 mdadm 명령을 사용할 때 '--level=0'으로 설정하며, 마운트할 디렉터리는 /raid0 정도라는 것뿐이다.

### 실습4

- RAID 0을 구성해보자.  /dev/sdd 와 /dev/sde 를 사용한다.

#### step0 

- 앞의 \<실습 3\>에 이어서 진행해야 한다.

#### step1

- 하드디스크 파티션 등의 선처리 작업은 이미 되어 있으므로 생략한다.

#### step2

mdadm 명령을 이용해 실제 RAID를 구성하자

- <b>mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdd1 /dev/sde1</b> 명령을 입력해 /dev/sdd1 과 /dev/sde1 을 RAID 0 장치인 /dev/md0 으로 생성하고 <b>mdadm --detail --scan</b> 명령을 입력해 잘 생성되었는지 확인한다.

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image40.png)

- <b>mkfs.ext4 /dev/md0</b> 또는 <b>mkfs -t ext4 /dev/md0</b> 명령을 입력해 /dev/md0 파티션 장치를 포맷한다.

- <b>mkdir /raid0</b> 명령을 입력해 마운트할 디렉터리 (/raid0) 를 생성하고, <b>mount /dev/md0 /raid0</b> 명령을 입력해 마운트시킨다. 그리고 <b>df</b> 명령으로 확인한다.

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image41.png)

- /dev/md0 장치는 RAID 0이므로 하드디스크 용량을 모두 사용한다. 따라서 /dev/sdd 의 1GB와 /dev/sde 의 1GB를 합한 약 2GB의 용량이 나왔다 

- 이번에는 컴퓨터를 켤 때 언제든지 /dev/md0 장치가 /raid0 에 마운트되어 있도록 설정하자. /etc/fstab 파일을 vi 에디터나 gedit으로 열어서 맨 아랫부분에 다음을 추가하면 된다.

```
/dev/md0    /raid0    ext4    defaults     0  0
```

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image42.png)

#### step3

- <b>mdadm --detail/dev/md0</b> 명령을 입력해 구축한 RAID 0을 자세히 확인해보자.


### RAID 1 구축

앞의 RAID 0과 거의 동일하다.

### 실습5

- RAID 1을 구성해보자.  /dev/sdf 와  /dev/sdg를 사용한다.

#### step0

- 앞의 \<실습 4\>에 이어서 진행해야 한다.

#### step1

- 하드디스크 파티션 등의 선처리 작업은 이미 되어 있으므로 생략한다.

#### step2

<b>mdadm</b> 명령을 이용해서 실제 RAID를 구성하자.

- 다음 명령을 참고해 /dev/sdf1 과 /dev/sdg1 을 RAID 1 장치인 /dev/md1 로 생성하고, 잘 생성되었는지 확인해본다.

```
mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdf1 /dev/sdg1
	-> 'Continue creating array?' 메시지가 나오면 y를 입력해서 계속 진행한다.
	
mdadm --detail --scan
```
> RAID 1 생성 시 나오는 경고 메시지는 부팅 장치로 사용할 수 없다는 경고다. 지금 만드는 RAID 1은 부팅 장치로 사용할 일이 없으므로 관계 없다.

- <b>mkfs.ext4 /dev/md1</b> 또는 <b>mkfs -t ext4 /dev/md1</b> 명령을 입력해 /dev/md1 파티션 장치를 포맷한다.

- <b>mkdir /raid1</b> 명령를 입력해 마운트할 디렉터리 (/raid1) 를 생성하고, <b>mount /dev/md1 /raid1</b> 명령을 입력해 마운트시킨다. 그리고 <b>df</b> 명령으로 확인한다.

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image43.png)


- RAID 0인 /raid0 디렉터리의 용량이 약 2GB 정도인데, RAID 1인 /raid 디렉터리는 1GB 정도 밖에 되지 않는다는 것을 확인할 수 있다. 동일한 데이터를 2회 저장하므로 실제 가용 용량은 2GB의 절반인 1GB 정도로 나온다.


-  이번에는 컴퓨터를 켤 때 언제든지 /dev/md] 장치가 /raid 디렉터리에 마운트되어 있도록 설정하자. /etc/fstab 파일을vi 에디터나 gelit으로 열어서 맨 아랫부분에 다음을 추가하면 된다.

```
/dev/md1    /raid1    ext4    defaults    0  0
```

#### step3

- <b>mdadm --detail /dev/md1</b> 명령을 입력해 구축한 RAID 1을 자세히 확인한다.


### RAID 5 구축

- 다음 그림을 참고해 RAID 5를 만든다. 방법은 앞에서 진행한 것과 거의 비슷하며, 하드디스크 개수만 최소 3개 이상으로 구성하면 된다.


#### RAID 5 구축 순서
 
![image44](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image44.png)

### 실습6

- RAID 5를 구성해보자. /dev/sdh, /dev/sdi, /dev/sdj 를 사용한다.

#### step 0

- 앞의 \<실습 5\>에 이어서 진행해야 한다.

#### step 1

- 하드디스크 파티션 등의 선처리 작업은 이미 되어 있으므로 생략한다.

#### step 2

<b>mdadm</b> 명령을 이용해서 실제 RAID 5를 구성하자.

- 다음 명령을 참고해 /dev/sdh1, /dev/sdi1, /dev/sdj1 을 RAID 5 장치인 /dev/md5 로 생성한다.

```
mdadm --create /dev/md5 --level=5 -raid-devices=3 /dev/sdh1 /dev/sdi1 /dev/sdj1
		-> 만약 경로 창이 나오면 그냥 두고 약 1-2분 정도 기다리자. 자동으로 없어진다.
		
mdadm --detail --scan
```
- <b>mkfs.ext4 /dev/md5</b> 명령을 입력해 /dev/md5 파티션을 포맷한다.
- <b>mkdir /raid5</b> 명령을 입력해 마운트할 디렉터리 (/raid5) 를 생성하고, <b>mount /dev/md5/raid5</b> 명령을 입력해 마운트시킨다. 그리고 <b>df</b> 명령으로 확인한다.

![image45](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image45.png)

- RAID 5는 <b>하드디스크 개수-1</b>만큼의 용량을 사용할 수 있다. 지금은 3개를 설치했으므로 2개의 용량인 2GB만 사용할 수 있다. 10개를 설치할 경우 9GB의 용량을 사용할 수 있다.

- 이번에는 컴퓨터를 켤 때 언제든지 /dev/md5 장치가 /raid5 디렉터리에 마운트되어 있도록 설정하자. /etc/fstab 파일을 vi 에디터나 gedit으로 열어서 맨 아랫부분에 다음을 추가하면 된다.

```
/dev/md5   /raid5   ext4    defaults   0 0
```

![image46](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image46.png)

- <b>mdadm --detail /dev/md5</b> 명령을 입력해 구축한 RAID 5를 자세히 확인해보자.

#### step 3

- <b>reboot</b> 명령으로 재부팅한 후 root 사용자로 로그인한다.
- <b>df</b> 명령으로 RAID 장치를 확인한다.

![image47](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image47.png)

#### step 4

- <b>halt -p</b> 명령으로 종료한다.
- 지금까지 설정한 내용을 'RAID 5까지 구성 완료' 이름으로 스냅숏으로 저장하자.

![image48](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image48.png)

## Linear RAID, RAID 0, RAID 1, RAID 5에서의 문제 발생과 조치 방법

- 이제 각 RAID 장치들이 우리가 기대하는 것처럼 잘 작동하는지 테스트해볼 차례다.
- Linear RAID나 RAID 0은 하드디스크 중 하나라도 고장나면 해당 하드디스크에 저장된 데이터를모두 복구할 수 없다고 이미 말했다. 
- 또 RAID 1과 RAID 5는 하드디스크 중 하나가 고장 나도 데이터가 안전하다는 점도 말했다.

### Linear RAID, RAID 0, RAID 1, RAID 5의 문제 발생 테스트

- RAID의 개념에서 배웠듯이 RAID 1, 5는 '결함 허용' 기능이 있다. 즉 하드디스크에 문제가 발생해도 저장된 데이터는 안전하다는 의미다. 
- 테스트를 위해 다음과 같이 각 RAID 구성과 연결된 하드디스크를 1개씩 고장 내겠다.


#### 각 RAID 구성과 연결된 하드디스크를 고장 내기 위한 하드웨어 구성도

![image49](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image49.png)

- 위 구성도를 보면 기존에 /dev/sdb ~ /dev/sdj 까지 9개였던 장치가 /dev/sdb ~ /dev/sdf 까지 5개만 보인다. 즉 기존의 /dev/sdc (SCSI 0:2)가 없어지면 /dev/sdc 장치가 없어지는 것이 아니라, 위의 구성도의 /dev/sdc (SCSI 0:3) 처럼 하나씩 밀리는 것이다.

### 실습7

Linear RAID, RAID 0, 1, 5의 하드디스크가 고장난 상황을 살펴보고, 정상적으로 부팅이 가능하도록 하자.

#### step 0

- 앞의 \<실습 6\>에 이어서 진행해야 한다.
- Server를 부팅하고 root로 접속한다.

#### step 1

정상적으로 작동하는 RAID에 적당한 파일을 복사해놓자.

- <b>df</b> 명령을 입력해서 확인했을 때 다음과 같이 정상적으로 raid에 마운트되어 있어야 한다.

![image50](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image50.png)

- /raidLinear, /raid0, /raid1, /raid5 디렉터리에 아무 파일이나 testFile이라는 이름으로 복사해 넣는다.

![image51](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image51.png)

- 각 디렉터리에 동일한 파일이 있는 것을 확인할 수 있다.
- 현재는 RAID가 모두 정상적으로 작동하는 상태다. <b>halt -p</b>명령을 입력해 종료한다.

#### step 2

다음과 같이 4개의 하드디스크를 고장 내자.

- [설정] - [저장소] - [컨트롤러 IDE]에서 추가한 하드 중 2번째, 4번째 6번째, 8번째 하드디스크를 제거한다.

![image53](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image53.png)
	
![image54](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image54.png)

#### step 3

- 다시 부팅하자.
- 그런데, 잠시 기다리면 정상적으로 부팅되지 않고 응급 모드 Emengency mode로 접속될 것이다. RAID로 구성된 하드디스크가 고장 나면 일단 응급 모드로 접속된다.
- 일단 접속하기 위해 root 사용자의 비밀번호인 password를 입력하고 [Enter]를 누르자.

- 먼저 <b>Is -l /dev/sd\*</b> 명령을 입력해 장치 이름을 확인해보자. 앞서 설명한 것처럼 /dev/sdb ~ /dev/sdj 까지 9개 였던 것이 /dev/sdb ~ /dev/sdf 까지 5개만 남았다.

![image55](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image55.png)

- df 명령을 입력해서 확인하면 기존의 /raidLinear, /raid0 디렉터리는 보이지 않고 결함 허용을 하는/raid1, /raid5 만 보인다.

![image56](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image56.png)

- <b>ls -l /raid1 /raid5</b> 명령을 입력해 RAID 1 및 RAID 5에 저장했던 파일을 확인하자. 잘 있을 것이다.

![image57](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image57.png)

- <b>mdadm --detail /dev/md1</b> 명령을 입력해 RAID 1 장치가 어떻게 작동하는지 상세히 확인해보자.

![image58](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image58.png)

- 총 2개의 하드디스크 중 1개가 작동하는 것을 확인할 수 있다. RAID 1에서 작동되는 장치는  /dev/sdd 가 작동된다. 비록 2개 중 하나만 작동하지만 결함 허용 기능으로 인해 데이터가 안전하게 보관된 것이 확인되었다.

- 같은 방식으로 <b>mdadm --detail /dev/md5</b> 명령을 입력해 RAID 5 장치도 확인해보자.

![image59](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image59.png)

#### step 4

이번에는 결함 허용을 제공하지 않는 RAID 장치를 다시 가동시켜보자.

- <b>mdadm --run /dev/md9</b> 명령을 입력해 Linear RAID (/dev/md9) 장치를, <b>mdadm --run /dev/md0</b> 명령을 입력해 RAID 0(/dev/md0)을 다시 가동시켜보자.

![image60](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image60.png)

#### step 5

- 우선 시스템이 정상적으로 가동되도록 하기 위해 Linear RAID와 RAID 0 장치를 중지시키고, /etc/fstab 에서도 제거하자.

- <b>mdadm --stop /dev/md9</b> 명령과 <b>mdadm --stop /dev/md0</b> 명령을 입력해 결함 허용이 없는 Linear RAID, RAID 0을 중지하자

![image61](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image61.png)

-  vi 에디터로 /etc/fstab 을 열어서 /dev/md9 와  /dev/md0 두 행 앞에 주석(#)을 붙인 후 저장하고 종료하자.

![image62](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image62.png)

- <b>reboot</b> 명령을 입력해 재부팅하자.

#### step 6

정상적으로 X 윈도로 부팅된다. root 사용자로 로그인하자.

- <b>df</b> 명령을 입력해서 확인하면 /raid1 과 raid5 디렉터리는 작동하고 있고, <b>Is</b> 명령으로 확인하면 기존의 데이터도 안전하다. 하지만 각 하드디스크가 하나씩 고장 난 상태라서 완전한 상태는 아니다. 또, Linear RAID와 RAID 0은 현재 가동조차 하지 않는다. 다음 실습에서 완전히 정상 상태가 되도록 복구해보겠다.
- <b>halt -p</b> 명령을 입력해 우선 시스템을 종료시킨다.


### Linear RAID, RAID 0, RAID 1, RAID 5의 원상복구

- 지금은 RAID 1과 RAID 5의 데이터를 정상적으로 사용할 수 있지만, 만약 RAID 1 또는 RAID 5에서 정상 작동 중인 다른 하드디스크까지 고장 난다면 영구히 복구할 수 없게 된다. 그러므로 될 수있으면 빨리 다음과 같이 고장 난 하드디스크를 제거하고 새로운 하드디스크로 교체해줘야한다

- 또 Linear RAID와 RAID 0의 구성은 원상 복구할 수 있지만, 당연히 그 안의 데이터는 살릴 수없다.

![image63](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image63.png)

### 실습8

- Linear RAID, RAID 0, RAID 1, RAID 5 장치의 고장 난 하드디스크를 새로운 하드디스크로 교체하자.

#### step 0

- 앞의 \<실습 7\>에 이어서 실습한다.

#### step 1

고장난 장치를 새로운 하드디스크로 교체하자. 가상머신이 꺼진 상태여야 한다.

- [설정] -> [저장소] -> [컨트롤러: IDE] -> [하드디스크 추가 아이콘]을 클릭하고 다음과 같이 1GB씩 같은 하드디스크를 4개 더 추가한다.

![image64](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image64.png)

- 부팅하면 정상적으로 X 윈도 화면으로 부팅될 것이다. root 사용자로 로그인하자.

#### step 2

새로운 하드디스크를 추가했다고 자동으로 RAID 장치가 복구되는 것은 아니다. 직접 수동으로 복구해야한다.

- 먼저 RAID 1장치의 구성을 다시 살펴보자.

```
mdadm --detail /dev/md1
```

![image65](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image65.png)

- 역시 자동으로 복구되지는 않았지만, 새 하드디스크를 교체하기 전과 약간의 차이를 확인할 수 있다 장치가 /dev/sdd 에서 /dev/sdf로 변했다. 

- 내부 파일인 /raid1/testFile /raid5/testFile은 아직도 이상 없이 존재한다


#### step 3

새로 장착한 하드디스크를 이용해서 Linear RAID, RAID 0, RAID 1, RAID 5를 복구하자.

- 우선 새로운 하드디스크 /dev/sdc 의 파일 시스템을 만들자.

```
# fdisk /dev/sdc 
Command : n    -> 새로운 파티션 분할
Select : p     -> Primary 파티션 선택
Partition number : 1   -> 파티션 번호 1번 선택
First Sector : [Enter]   -> 시작 섹터 번호 입력
Last Sector : [Enter]   -> 마지막 섹터 번호 입력
Command : t      -> 파일 시스템 유형 선택
Hex Code : fd     -> 'Linux raid autodetect' 유형 번호 입력
Command : p     -> 설정된 내용 확인
Command : w     -> 설정 저장 
```

- 같은 방법으로 하드디스크 /dev/sde , /dev/sdg , /dev/sdi 의 파일 시스템을 만들자.
- 모든 파티션이 작성되었는지 확인한다.

![image66](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image66.png)

- <b>mdadm --stop /dev/md9</b> 명령을 입력해 Linear RAID 장치(/dev/md9)를 중지하고 <b>maadm --create /dev/md9 --level=linear --raid-devices=2 /dev/sdb1 /dev/sdc1</b> 명령을 입력해 다시 구성하자. 확인 메시지가 나오면 y를 입력한다.

![image67](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image67.png)

- 같은 방식으로 <b>mdadm --stop /dev/md0</b> 명령을 입력해 RAID 0 장치(md0)를 중지하고 <b>mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdd1 /dev/sde1</b> 명령을 입력해 다시 구성하자.

![image68](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image68.png)

- <b>mdadm --detail /dev/md9</b> 명령과 <b>mdadm --detail /dev/md0</b> 명령을 입력해 두 RAID 장치가 잘 작동되는지 확인하면 구성했을 때와 동일하게 잘 작동할 것이다.

#### step 4 

이번에는 결함 허용이 있는 RAID 1, 5를 구성하자.

- RAID 1을 재구성하자. 그런데 RAID 1은 하드디스크가 1개 빠졌을 뿐 잘 작동한다. 그러므로 새로운 하드디스크만 추가하는 명령인 <b>mdadm /dev/md1 --add /dev/sdg1</b> 명령을 입력해야 한다.

- <b>mdadm /dev/md5 --add /dev/sdi1</b> 명령을 입력해서 같은 방식으로 RAID 5를 재구성하자.

![image69](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image69.png)

-<b>mdadm --detail /dev/md1</b> 명령과 <b>mdadm --detail /dev/md5</b> 명령을 입력해서 두 RAID 장치가 잘 작동된는지 확인하자.

![image70](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image70.png)

> 만약 RAID 5 장치의 4번 장치가 'spare rebuilding /dev/sdi1'로 표시된다면 현재 RAID 5를 재구성하는 상태이기 때문이다. 잠시 기다렸다가 다시 확인하면 된다.

- gedit이나 vi 에디터로 /etc/fstab 을 열어 앞에서 주석 (#) 표시했던 /dev/md9 와 /dev/md0 의 주석을 제거하자.

- reboot 명령을 입력해 재부팅한다.

#### step 5

- 이제는 정상적으로 X 윈도 화면으로 부팅될 것이다. root 사용자로 접속하자.

> 만약 부팅 중 멈춘다면 [CTRL] + [D] 를 눌러서 계속 진행한다.

- <b>Is</b> 명령으로 /raid0 디렉터리를 확인하면 당연히 testFile이 보이지 않아야 한다.

> 만약 raid0에 파일이 보인다면 이 파일은 정상 파일이 아닌 50%만 정상인 파일이다 (파일 크기가 기존과 동일해도 실제 내용의 50%는 비었다고 보면 된다). 그러므로 RAID 0을 복구한 후에는 mkfs 명령으로 깨끗이 포맷하는 것이 좋다.

![image71](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image71.png)

- 이번에는 /raidLinear 디렉터리를 확인하자. 기존의 testFile이 보일 것이다. 즉 복구되었다.

![image72](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image72.png)

-  /raid1 과 /raid5 디렉터리의 데이터는 정상적으로 안전하게 있을 것이다. 결함 허용을 제공하므로 또다시 하드디스크가 고장 나도 데이터는 안전하다.

#### step 6

- 앞의 실습에서 RAID 1과 RAID 5는 새로운 하드디스크를 추가하기 전과 후 모두 데이터가 존재하기 때문에, 사용자 입장에서는 겉으로 보기에 변화가 없는 듯 보인다. 하지만 내부적으로는 다음과 같은 변화가 발생했다

![image73](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image73.png)

## 고급 RAID 레벨

- 이제 기본적인 RAID 레벨인 Linear RAID, RAID 0, RAID 1, RAID 5는 이해했을 것이다. 
- 이번에는 RAID 5보다 신뢰도를 높인 RAID 6과 신뢰도와 속도 두 마리 토끼를 잡기 위한 RAID 1+0, 그리고 성능은 떨어지고 비용도 많이 들지만 신뢰도를 훨씬 높인 RAID 1+6을 차례로 구성해보자.

### RAID 6과 RAID 1+0 개념

- RAID 5는 패리티를 1개 사용하기 때문에 3개의 하드디스크 이상이면 구성할 수 있지만, RAID 6은 패리티를 2개 사용하기 때문에 최소 4개의 하드디스크가 필요하다. 하지만 실무에서는 7~8개 이상의 하드디스크로 구성해야 어느 정도 효과를 볼 수 있다. 
- 예를 들어 하드디스크 4개로 구성할 때는 공간 효율이 '하드디스크 개수 -2'이므로 4-2=2TB만 사용할 수 있다. 또 RAID 1+0은 RAID 1 (안전성)+RAID 0 (속도)'의 개념이라고 설명했다. 그래서 공간 효율은 50%가 된다. 

- 이번에 구성할 RAID 6과 RAID 1+0의 구성도는 다음과 같다.

- RAID 6은 기존 RAID 5의 구성과 구현 방법이 거의 동일하다. 단, 하드디스크가 최소 4개 이상 필요한 것뿐이다. RAID 1+0의 구현 방법은 약간 다르다. 다음과 같이 각 2개씩 먼저 RAID 1로 구성한 후, 2개의 RAID 1 장치를 다시 RAID 0으로 묶는 방식을 사용한다.

![image74](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image74.png)

### 실습9

- RAID 6과 RAID 1+0을 구성해보자.

#### step 0

- Server를 처음 설치 상태로 초기화하자.
- 아직 부팅은 하지 말자.

#### step 1

실습에 필요한 하드디스크 8개를 준비하자.

- \<실습 1\> 또는 \<실습 2\>를 참조해서 1GB SCSI 하드디스크 8개를 장착하자. 즉 /dev/sdb ~ /dev/sdi 까지 추가한다. 

![image75](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image75.png)

- 부팅하고 root 사용자로 접속한다.
- 8개의 하드디스크(sdb ~ sdi) 각각에 <b>fdisk /dev/하드디스크이름</b> 명령을 입력해 RAID 파티션을 생성하자. 

![image76](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image76.png)

#### step 2

/dev/sdb1 ~ /dev/sde1 을 RAID 6 장치인 /dev/md6 으로 생성하자.

- <b>mdadm --create /dev/md6 --level=6 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1</b> 명령을 입력해 RAID 6을 만든다. 그리고 <b>mdadm --detail /dev/md6</b> 명령을 입력해서 만들어진 RAID 6 구성을 확인한다.

![image77](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image77.png)

- <b>mkfs.ext4 /dev/md6</b> 명령을 입력해서 /dev/md6 파티션을 포맷한다.

- <b>mkdir /raid6</b> 명령을 입력해서 마운트 디렉터리 (/raid6) 를 생성하고, <b>mount /dev/md6 /raid6</b> 명령을 입력해서 마운트시킨다. 그리고 <b>df</b> 명령으로 확인한다.

![image78](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image78.png)

- 결과를 보면 /raid6 디렉터리에 약 2GB 정도의 공간이 있는 것을 확인할 수 있다. 
- RAID 개념에서 설명했듯이 RAID 6은 <b>하드디스크개수-2</b> 만큼의 용량을 사용할 수 있다.

> 지금은 하드디스크 4개를 이용해서 RAID 6을 설치했으므로 2개의 용량인 2GB를 사용할 수 있는 것이다. 하드디스크 개수가 적어서 공간 효율성이 너무 떨어진다. 그러므로 RAID 6은 7~8개 이상의 하드디스크를 사용해야 공간 효율성의 효과를 볼 수 있다.

#### step 3
- 이번에는  /dev/sdf1 ~ /dev/sdi1을 RAID 1+0 장치인 /dev/md10 으로 생성하자.

- 먼저 <b>mdadm --create /dev/md2 --level=1 --raid-devices=2 /dev/sdf1 /dev/sdg1</b> 명령을 입력해 /dev/def 와 /dev/sdg 를 /dev/md2 에 RAID 1로 구성하자. /dev/sdh 와 /dev/sdi 도 <b>mdadm --create /dev/md3 --level=1 --raid-devices=2 /dev/sdh1 /dev/sdi1</b> 명령을 입력해 /dev/md3 에 역시 RAID1로 구성하자. 이때 확인 메시지가 나오면 y를 입력해서 계속 진행한다.

> 혹시 혼란스러울까봐 다시 언급하지만 '/dev/md번호'에서 번호는 임의로 지정한 것이다. 다른 RAID 장치와 중복되지 않는다면 아무 번호나 지정해도 상관없다.

![image79](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image79.png)

![image80](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image80.png)

- 이번에는 <b>mdadm --create /dev/md10 --level=0 --raid-devices=2 /dev/md2 /dev/md3</b>명령을 입력해 두 개의 RAID 1장치를 RAID 0(/dev/md10)으로 묶는다. 이 상태가 RAID1+0이 구성된 결과다.

- 이제 <b>mkfs.ext4 /dev/md10</b> 명령을 입력해 /dev/md10 파티션을 포맷한다.
- <b>mkdir /raid10</b> 명령을 입력해서 마운트할 디렉터리(/raid10)를 생성하고, <b>mount /dev/md10 /raid10</b> 명령을 입력해 마운트시킨다. 그리고 <b>df</b> 명령으로 확인한다.

![image81](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image81.png)


- 결과를 보면 /raid10 디렉터리에 약 2GB 정도의 공간이 있는 것을 확인할 수 있다. RAID 1+0은 RAID 1과 마찬가지로 공간 효율이 <b>하드디스크개수 / 2(50%)</b>가 된다는 것을 확인할 수 있다. 이제 RAID 방식 중에서 성능 (속도)이 가장 빠른 RAID 0의 효과를 내면서, 안정성은 RAID 1만큼 확보된 RAID 1+0 장치를 사용할 수 있다.

#### step 4

- <b>cp /boot/vmlinuz-4\* /raid6/testFile</b> 명령과 <b>cp /boot/vmlinuz-4\* /raid10/testFile</b> 명령을 입력해 RAID 6과 RAID 1+0 장치에 적당한 파일을 복사하자.


#### step 5

- 이번에는 컴퓨터를 켤 때 언제든지 /dev/md6 장치는 /raid6 디렉터리에, /dev/md10 장치는 /raid10 디렉터리에 마운트되어 있도록 설정하자. /etc/fstab 파일을 vi 에디터나 gedit으로 열고, 맨 아랫부분에 다음 2줄을 추가하면 된다.

```
/dev/md6    /raid6    ext4    defaults    0 0
/def/md10   /raid10    ext4    defaults    0 0
```

#### step 6

- <b>reboot</b> 명령으로 정상적으로 부팅되는지 확인하자. 또 /raid6 과 /raid10 의 파일도 잘 있는지 확인하자.

#### step 7

- <b>halt -p</b> 명령을 입력해 시스템을 종료한다.


### RAID 6과 RAID 1+0의 문제 발생 테스트

- RAID 6과 RAID 1+0의 장점인 신뢰성을 시험해보기 위해 각각 2개의 하드디스크를 고장 내보자. RAID 5에서는 2개의 하드디스크를 고장 낼 경우 모든 데이터를 사용할 수 없지만, RAID 6과 RAID 1+0에서는 데이터에 아무런 이상이 없다. 
- 2, 4, 6, 7 번째 하드디스크 4개를 다음과 같이 고장 내보자.

![image82](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image82.png)

### 실습10

- RAID 6과 RAID 1+0의 결함 허용을 확인하자. 각 하드디스크를 2개씩 고장 낸 후 파일이 정상적으로 있는지 확인해보자.

#### step 0

- 앞의 \<실습 9\>에 이어서 한다.


#### step 1

- Server가 종료된 상태에서 다음과 같이 2, 4, 6, 7 번째 하드디스크 4개의 하드디스크를 고장 내자.

![image83](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image83.png)

#### sten 2

부팅하고 root 사용자로 접속한다. 부팅이 약간 오래 걸릴 수 있다.

#### step 3

현재는 하드디스크 중 몇 개가 고장 난 상황이다.

- 데이터를 확인해보자. 현재 각 RAID의 하드디스크가 2개씩 모두 고장 난 상태지만 데이터는 안전하다.

![image84](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image84.png)

- <b>mdadm --detail /dev/md6</b> 명령을 입력해 RAID 6(/dev/md6) 장치의 구성을 확인하자

![image85](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image85.png)

- 결과를 보면 현재 /dev/md6 장치의 상태가 잘 나타난다. 현재 /dev/sdb1, /dev/sdc1 두 장치만 작동 중인 상태임을 확인할 수 있다.
- RAID 1 장치인 /dev/md2, /dev/md3 도 역시 1개씩만 작동하고 있을 것이며, RAID 1+0은 잘 작동하고 있을 것이다.

#### step 4

- <b>halt -p</b> 명령을 입력해 시스템을 종료한다.

- 일반적으로 실무에서 많이 사용하는 RAID 방식은드웨어 RAID의 경우 RAID 1, 5 등이고, 소프트웨어 RAID의 경우 사용 용도에 따라 RAID 1, 5, 6을 골고루 사용한다. 특히 RAID 1+0은 안정적이고 빠른 방식이므로 소프트웨어 RAID를 구성할적극 고려할 만하다.

#### 퀴즈1
- \<실습 10\>을 마치고 새로운 하드디스크 4개를 장착해서 RAID 6과 RAID 1+0을 완전한 상태로 원상 복구해보자. 상세한 명령은 \<실습 8\>을 참조한다.

- 힌트 1 : sdc, sde, sdg, sdh로 사용할 4개의 하드디스크에 파티션을 설정한다.
- 힌트 2 : md6에는 sdc1과 sde1을, md2에는 sdg1을, md3에는 sdh1 을 추가한 후 재부팅한다.


#### 퀴즈2

- Server (B)를 초기화하고 다음고ㅛㅏ 같은 RAID 1+6을 구현해보자. RAID 1+6은 공간 효율이 25%이므로 비용도 비싸고 성능도 느리지만 안전성 면에서는 탁월하다.

- 힌트 : RAID를 구성하는 명령은 다음과 같이 사용하자.

```
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdd1 /dev/sde1
mdadm --create /dev/md2 --level=1 --raid-devices=2 /dev/sdf1 /dev/sdg1
mdadm --create /dev/md3 --level=1 --raid-devices=2 /dev/sdh1 /dev/sdi1
mdadm --create /dev/md16 --level=6 --raid-devices=4 /dev/md0 /dev/md1 /dev/md2 /dev/md3

mkfs.ext4 /dev/md16
mkdir /raid16
mount /dev/md16 /raid16
```

![image86](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image86.png)

* * * 
# LVM

- LVM은 Logical Volume Manager의 약자로 '논리 하드디스크 관리자'란 의미다. 
- LVM은 앞에서배운 Linear RAID와 기본 기능은 비슷해 보이지만 더 많은 기능이 있다. 그래서 CentOS는 기본적으로 설치 시 LVM으로 하드디스크를 분할해서 설치한다.

- LVM의 주요 용도는 여러 개의 하드디스크를 합쳐서 1개의 파티션으로 구성 후, 다시 필요에 따라나누는 것이다. 
- 또는 1개의 하드디스크를 LVM으로 구성하고 다시 파티션을 구분할 수도 있다. 일례로 2TB의 하드디스크 2개를 합친 후 다시 1TB와 3TB로 나눠서 사용 가능하다. 
- RAID와 달리 LVM 에서는 새로운 용어가 몇 개 나온다.

- <b>물리 볼륨(Physical Volumn)</b> : /dev/sda1, /dev/sdb1 등의 파티션을 말한다. 
- <b>볼륨 그룹(Volumn Group)</b> : 물리 볼륨을 합쳐서 1개의 물리 그룹으로 만든 것이다.
- <b>논리 볼륨(Logical Volumn)</b> : 볼륨 그룹을 1개 이상으로 나눈 것으로 논리적 그룹이라고 한다.

이번에 구성할 하드디스크의 구성도는 다음과 같다.

![image87](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image87.png)

- 물리 볼륨인 2TB와 3TB, 2개의 하드디스크를 합쳐 5TB의 볼륨 그룹으로 묶었다. 그리고 5TB를 1TB, 3TB, 1TB로 분할해서 각 /Ivml, /lvm2, /lvm3 디렉터리에 마운트한 상태를 보여준다.

- 결국 LVM은 여러 개의 하드디스크 (물리 볼륨)를 묶어서 1개의 볼륨 그룹으로 만든 후, 다시 필요한 용량의 파티션 (논리 그룹)으로 나눠서 사용하는 것이라고 보면 된다.

### LVM 구현

이번 실습의 순서는 다음과 같다. RAID 구성과는 명령어가 좀 다르다.

![image88](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image88.png)

### 실습11
- LVM을 구성하자. 

#### step 0

- Server를 처음 설치 상태로 초기화하자
- 아직 부팅은 하지 말자.


#### step1

- 다음과 같이 2GB와 3GB 용량의 SCSI 하드디스크 2개를 추가한다. 
- 부팅하고 root 사용자로 접속하자.

![image89](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image89.png)

#### step 2

LVM을 구현하기 위해 선처리 작업 부분을 먼저 수행한다.

- 장착한 SCSI 하드디스크에 파티션을 할당하자. 이번 실습은 LVM 실습이므로 파일 시스템 유형을8e(Linux LVM) 로 지정해야 한다.

> 파일 시스템 유형을 지정하지 않으면 기본인 83 (Linux)가 되며, RAID는 fd (Linux raid autodetect)로 지정했었다.

```
# fdisk /dev/sdb   -> 하드디스크 선택
Command : n   -> 새로운 파티션 분할
Select : p     -> Primary 파티션 선택
Partition number (1-4) : 1   -> 파티션 번호 1번 선택
First sector : [Enter]   -> 시작 섹터 번호 입력(기본 설정)
Last sector : [Enter]   -> 마지막 섹터 번호 입력(기본 설정)
Command : t   -> 파일 시스템 유형 선택
Hex Code : 8e    
		-> 선택한 파일 시스템 유형 번호 입력('L'을 입력하면 유형 번호가 출력됨)
Command : p   -> 설정된 내용 확인
Command : w   -> 설정 저장
```

- 같은 방식으로 /dev/sdc 의 파티션을 나눈다. 

- <b>pvcreate /dev/sdb1</b> 명령과 <b>pvcreate /dev/sdc1</b> 명령을 입력해 물리적인 볼륨을 생성한다.

![image90](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image90.png)

- 2개의 물리 볼륨을 하나로 묶어주자. 즉 볼륨 그룹을 생성하는 단계며 <b>vgcreate myVG /dev/sdb /dev/sdc1</b> 명령을 입력하면 된다. 볼륨 그룹 이름을 myVG로 정했다.

![image91](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image91.png)

- <b>vgdisplay</b> 명령을 입력해 볼륨 그룹이 제대로 생성되었는지 확인해보자.

![image92](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image92.png)

- 생성한 myVG 볼륨 그룹은 현재 물리 볼륨 (Cur PV)이 2개로 구성되어 있으며, 2GB+3GB=5GB인 것을확인할 수 있다. 이로써 선처리 작업이 모두 끝났다.
- 이제부터는 /dev/myVG 를 하나의 하드디스크처럼 생각하고 작업하면 된다.

#### step 3

- 일반적인 하드디스크의 파티션을 생성한 때는 fdisk 명령을 사용했지만 붙음 그룹의 파티션을 생성할 때는 <b>Ivcreate</b> 명령을 사용한다. 일반적인 하드디스크(/dev/sdb)를 /dev/sdb1 과 /dev/sdb2 로 파티션을 나눠 생성하는 것과 마찬가지로 볼을 그룹(/dev/myVG)을 /dev/myVG/myLG1, /dev/myVG/myLG2, /dev/myVG/myLG3 이라는 논리 그룹으로 파티션을 나눠 생성하는 것이다.

- 논리 그룹을 IGB, 3GB, 1GB로 나누기 위해 다음 명령을 입력하고 /dev/myVG 디렉터리를 확인해보자.

```
lvcreate --size 1G --name myLG1 myVG   -> myVG아래 myLG1을 1GB 크기로 생성
lvcreate --size 3G --name myLG2 myVG
lvcreate --extents 100%FREE --name myLG3 myVG -> 나머지 용량 할당 
ls -l /dev/myVG
```

![image93](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image93.png)

> /dev/myVG/myLG1 은 사실 /dev/dm-0이라는 파일에 링크되어 있다. 하지만 이 장치 파일의 이름은 lvcreate 명령의 버전마다 달라질 수 있으므로 /dev/myVG/myLG1 이라고 생각하는 것이 좋다.

#### step 4

- /dev/myVG/myLG1, /dev/myVG/myLG2, /dev/myVG/myLG3 에 파일 시스템을 생성하자.

```
mkfs.ext4 /dev/myVG/myLG1
mkfs.ext4 /dev/myVG/myLG2
mkfs.ext4 /dev/myVG/myLG3
```

#### step 5

- /vml /vm2 /Ivm3 세 디렉터리를 생성하자. 그리고 myLG1~3 장치를 /lvm1~3 디렉터리에 각각 마운트하자 마운트한 후에는 아무 파일이나 하나 복사해놓고 df 명령을 입력해 여유 공간을 확인해본다.

![image94](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image94.png)

#### step 6

- 컴퓨터를 켤 때 항상 myLG1~3 장치가 /lvm1~3에 마운트되도록 설정하자. /etc/fstab 파일을 vi 에디터나 gedit으로 열어서 맨 아랫부분에 다음을 추가하고 재부팅하면 된다.

```
/dev/myVG/myLG1    /lvm1   ext4    defaults    0 0
/dev/myVG/myLG2    /lvm2   ext4    defaults    0 0
/dev/myVG/myLG3    /lvm3   ext4    defaults    0 0
```

#### 퀴즈
- Server(B)에 5GB, 4GB 하드디스크를 장착하고, LVM으로 3GB 3개로 분할해보자.
- 힌트 : 먼저 Ivm2 패키지를 설치해야 한다.

* * * 
# CentOS를 RAID에 설치하기

- 우리는 Server, Server(B)를 /dev/sda)에 설치했다. 그런데 이 하드디스크가 고장 나면 아예 부팅이 되지 않으므로 추가한 RAID나 LVM을 전혀 사용할 수 없다. 
- 그래서 이번에는 아예 결함 허용을 제공하는 RAID 1에 CentOS를 설치하고자 한다. 다음과 같이 /dev/sda), /dev/sdb 를 RAID 1로 구성하면서 CentOS를 설치하면 어떤 하드디스크가 고장 나든 잘 부팅될 것이다. 

![image95](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image95.png)

### 실습12

- RAID 1로 안전하게 작동되는 CentOS를 새로 설치하자.

#### step 0
- 다음 내용을 참고하여 실습에 사용할 가상머신을 생성한다. 

```
가상머신 이름 : RAID 1 
메모리 할당 : 2GB(=2048MB)
하드디스크 : SCSI 80GB X 2
```

- 완성된 가상머신은 다음과 같다.

![image96](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image96.png)

#### step 1

기존의 설치 방식과 동일하게 CentOS 8 ISO 파일을 넣고 설치를 진행하자.

- 초기 환영 화면에서 왼쪽의 [한국어]를 선택하고 \<계속 진행\>을 클릭한다. 
- [언어 설정]에서 [한국어]로 지정한다. 
- [설치 목적지]를 클릭한다.

![image97](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image97.png)

- [설치 목적지]에서 하드디스크 2개를 한 번씩 클릭해서 선택한 후 <b>사용자 정의</b>을 선택하고 \<완료\>를 클릭한다.

![image98](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image98.png)

- [수동으로 파티션 설정]에서 <b>표준 파티션</b>으로 변경한 후 아래쪽 \<+\>를 클릭하고 [신규 적재 지점 추가]에서 적재 지점(Mount Point)은 [swap]을 선택하며, 희망 용량(Desired Capacity)은 4G를 입력한 후 \<적재 지점 추가\>를 클릭한다.

![image99](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image99.png)

- [수동으로 파티션 설정]에서 [swap]을 선택하고 장치 유형(Device Type)을 [RAID]로 선택한 후 RAID 레벨은 [RAID1]을 선택해 왼쪽 아래의 \<최신화 설정\>을 클릭한다.

![image100](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image100.png)

- 다시 왼쪽에 있는 \<+\>를 클릭해서 동일한 방식으로 / 파티션을 RAID 1로 구성한다.

![image101](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image101.png)

![image102](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image102.png)

- 왼쪽 \<완료\>를 클릭하고 [변경 요약]의 오른쪽 아래에 있는 \<변경 사항 적용\>을 클릭한다.
- 설정이 완료되었으면 \<설치 시작\>을 클릭한다.

#### step 2

- 설치가 진행된다.
- 설치가 완료되었으면 재부팅>을 클릭해서 컴퓨터를 재부팅한다.

#### step 3

컴퓨터가 다시 켜지면 일부 설정을 추가로 해줘야 한다.

- 부팅 화면이 나온다. 몇 초를 기다리거나 첫 번째 행이 선택된 상태에서 그냥 Enter를 누르면 부팅된다.
- [초기 설정]에서 [Lincese Information]을 클릭한 후 아래쪽 '약관에 동의합니다'를 체크하고 \<완료\>를 클릭하자. 그리고 오른쪽 \<설정 완료\>를 클릭해서 진행한다.

- 다시 부팅되면 잠시 후 X 윈도 로그인 화면이 나온다. [목록에 없습니까?]를 클릭해서 root 사용자로 로그인 하자, 암호는 root 사용자의 암호인 'password'를 입력하고 \<로그인\>을 클릭한다.

- 그놈GNOME 의 초기 설정 화면이 나오고 먼저 [환영합니다] 화면이 등장한다. 이미 한국어가 선택되어 있을 것이다. \<다음\>을 클릭한다.

- 입력]이 나온다. '한국어'를 선택하고 \<다음\>을 클릭한다.
- [개인 정보]가 나오면 그대로 두고 \<다음\>을 클릭한다.
- [온라인 계정]도 그대로 두고 \<건너뛰기\>를 클릭한다.
- 마지막 창에서 \<CentOS Linux 시작\>을 클릭한다.
- [시작하기(GNOME Help)] 창이 나온다. 오른쪽 위의 \<X\>를 클릭해서 닫는다.

#### step 4

RAID 1로 작동되는 것을 확인하자.
 
- 왼쪽 위 [현재 활동] → [프로그램 표시] → [유틸리티] → [터미널]을 선택해서 터미널을 연다.
- <b>mdadm --detail --scan</b> 명령을 입력해 전체 작동되는 RAID를 확인하자.

![image108](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image108.png)

- <b>mdadm --detail /dev/md/swap</b> 명령과 <b>mdadm --detail /dev/md/root</b> 명령을 입력해 각 RAID 장치를 자세히 확인해 보자. 두 RAID 장치 모두 잘 작동하고 있을 것이다.

![image109](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image109.png)

- <b>halt -p</b> 명령을 입력해 시스템을 종료하자.


#### step 5

RAID 1의 결함 허용이 잘 작동하는지 확인하자.

- RAID1의 하드디스크 2개 중 아무거나 제거하고 부팅해보자.

![image110](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image110.png)

- 부팅이 좀 오래걸리지만 기다리면 부팅될 것이다. root로 접속하자. 
- <b>mdadm --detail /dev/md/root</b> 명령을 입력해 RAID 장치를 다시 확인해보자.

![image111](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image111.png)

> RAID 1은 결함 허용 기능이 있으므로 하드디스크 하나가 고장 나도 운영체제 자체는 잘 작동한다.

### 퀴즈

RAID1 가상머신에 새로운 하드디스크를 장착하고 RAID1 가상머신이 다시 결함 허용을 하도록 원상 복구하자.

- 힌트 1 : 하드디스크를 추가한다.
- 힌트 2 : fdisk -1 /dev/sda 명령을 입력해 /dev/sda 의 파티션을 확인하고, 동일하게 /dev/sdb 장치의 파티션을 설정한다.
- 힌트 3 :  mdadm 명령을 사용해 /dev/md/swap 과 /dev/md/root에 파티션을 추가해서 원상복구하자. 이때 하드디스크 추가 후 하드디스크 2개를 동일하게 만드는 데는 오랜 시간이 걸린다.

* * * 
# 사용자별로 공간을 할당하기

- 리눅스는 여러 명의 사용자가 동시에 접속해서 사용할 수 있다. 만약 A라는 사용자가 시스템을 사용할 때 루트(/) 파일 시스템에 고의든 실수든 큰 파일들을 계속 복사했다고 가정해보자. 하드디스크가 꽉 차면 시스템 전체가 가동되지 않는 치명적인 문제를 일으킬 수 있다. 
- 이런 상황을 미연에 방지하려면 각 사용자별로 사용할 수 있는 용량을 제한해야 한다. 즉 사용자가 적정 용량 이상을 사용하지 못하게 함으로써 할당된 양만큼의 공간만 사용하게 하면 아무런 문제가 발생하지 않을 것이다.

## 쿼터의 개념과 실습

- 쿼터(Quota)를 간단히 정의하면 다음과 같다.

```
파일 시스템마다 사용자나 그룹이 생성할 수 있는 파일의 용량과 개수를 제한하는 것
```

- 일반 사용자가 사용하는 파일 시스템을 루트(/)로 지정하는 것보다는 별도의 파일 시스템을 지정해서 지정한 부분만 사용하도록 하는 것이 여러 면에서 좋다. 우선 실수로 루트(/) 파일 시스템을 사용하는 일이 없으므로 시스템과 관련된 문제를 발생시킬 소지가 적어진다.

- 루트(/) 파일 시스템을 많은 사용자가 동시에 사용하면, 서버를 운영하면서 하드디스크를 읽고 쓰는 작업과 일반 사용자가 하드디스크를 읽고 쓰는 작업이 동시에 발생한다. 이러면 전반적으로 시스템의 성능이 저하될 수 있다.

#### 쿼터 진행 순서

![image103](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image103.png)


### 실습13

쿼터 실습을 진행하자. 먼저 사용자를 만들고 해당 사용자에게 공간을 할당해보자.

#### step 0

- Server를 처음 설치 상태로 초기화하자.
-  아직 부팅은 하지 말자.
- Server에 10GB 크기의 새로운 SCSI 하드디스크 하나 장착한다.
- 부팅하고 root 사용자로 접속한 후 터미널을 하나 연다.
-  /dev/sdb 의 파티션 생성과 포맷을 진행한 후 /userHome 디렉터리에 마운트하자.

```
# fdisk /dev/sdb
Command : n
Select : p
Partition number (1-4) : 1
First sector : [Enter]
Last sector : [Enter]
Command : p
Command : w
mkfs.ext4 /dev/sdb1
mkdir /userHome
mount /dev/sdb1 /userHome
```

- 재부팅해도 인식되도록 vi나 gedit을 이용해서 /etc/fstab 맨 아래에 다음을 추가하자.

```
/dev/sdb1    /userHome    ext4     defaults   0 0
```

#### step 1

- 다음 명령을 입력해 쿼터 실습을 할 사용자 john과 bann을 만들고, 비밀번호도 사용자 이름과 동일하게 하자.

```
useradd -d /userHome/john john
useradd -d /userHome/bann bann
passwd john
(john 입력, 입력되는 문자는 보이지 않는다.)
(john을 다시 입력, 입력되는 문자는 보이지 않는다.)

passwd bann
(bann 입력, 입력되는 문자는 보이지 않는다.)
(bann을 다시 입력, 입력되는 문자는 보이지 않는다.)
```

![image104](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image104.png)

> useradd 명령어 중 -d 옵션은 사용자의 홈 디렉터리를 임의로 지정하기 위한 옵션이다. 사용자의 비밀번호는 8자 이상이며 사전에 있는 글자 등은 사용할 수 없지만, root 사용자는 아무 비밀번호나 지정할 수 있다. 그래서 경고만 나오고 계속 진행된다.

#### step 2

/etc/fstab 파일을 편집한다.


 vi-  에디터나 gedit으로 /etc/fstab 파일을 열어서 /dev/sdb1 을 마운트하는 부분의 defaults 글자에 붙여 다음과 같이 ',usrjquota=aquota.user.jqfmt=vfsv0(맨 뒤는 숫자 0)'이라고 추가한다. 글자가 틀리지 않도록 주의하자. 저장하고 닫는다.

```
/dev/sdb1   /userHome  ext4   defaults,usrjquota=aquota.user,jqfmt=vfsv0     0  0
```

- 재부팅하는 효과를 내기 위해 <b>mount --options remount /userHome</b> 명령을 입력하고 다시 마운트한다. <b>mount</b> 명령을 입력해서 확인해보면 /dev/sdb1 디렉터리가 '쿼터용'으로 마운트된 것을 확인할 수있다

![image105](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image105.png)

![image106](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image106.png)

#### step 3

- 쿼터를 사용하려면 쿼터 DB를 생성해야 한다. 다음 명령을 차례로 입력하자(좀 생소한 명령들이지만 쿼터생성 시 한 번만 사용하므로 외울 필요는 없다. 또한 일부 명령은 생략 가능하지만 확실히 하기 위해 반복해서 입력한 것도 있다).

```
cd /userHome     -> 쿼터용 파일 시스템이 마운트된 디렉토리로 이동
quotaoff -avug    -> 일단 쿼터를 끈다.
quotacheck -augmn   -> 파일 시스템의 쿼터 관련 체크를 진행한다.
rm -rf aquota.*      -> 생성된 쿼터 관련 파일을 일단 삭제한다.
quotacheck -augmn    -> 다시 파일 시스템의 쿼터 관련 체크를 진행한다. 
touch aquota.user aquota.group  -> 쿼터 관련 파일을 생성한다.
chmod 600 aquota.*    -> 보안을 위해 소유자(root) 외에는 접근하지 못하게 한다.
quotacheck -augmn   -> 마지막으로 파일 스스템의 쿼터 관련 체크를 진행한다. 
quotaon -avug    -> 설정된 쿼터를 시작한다.
```

![image112](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image112.png)

> quotacheck 명령어의 기능은 하드디스크를 스캔해서 여러 부분을 체크하는 것이고, quotaon/quotaoff 명령어의 기능은 설정된 쿼터를 켜거나 끄는 것이다. 사용할 수 있는 옵션을 요약하면 다음과 같다. 더 상세한 내용은 <b>man quotacheck</b> 명령을 입력해 확인하자.

- -a(All) : 모든 파일 스스템을 체크한다.
- -u(User) : 사용자 쿼터 관련 체크를 진행한다.
- -g(Group) : 그룹 쿼터 관련 체크를 진행한다. 
- -m(no-remount) : 재마운트를 생략한다.
- -n(use-first) : 첫 번째 검색된 것을 사용한다.
- -p(print-state) : 처리 결과를 출력한다.
- -v(Verbose) : 파일 시스템의 상태를 보여준다.

#### step 4

쿼터 DB 생성을 완료했으므로, 이제 각 사용자별로 공간을 할당해야 한다.

-  john 사용자와 bann 사용자가 사용할 수 있는 공간을 각각 20MB씩 할당하자. <b>edquota -u john</b> 명령을 입력하면 각 사용자별 또는 그룹별 할당량을 편집할 수 있다. 사용법은 vi 에디터와 동일하다 (터미널 창이 작으면 줄이 아래로 내려가서 이상하게 보인다. 터미널 창을 가로로 크게 늘려준다).

![image113](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image113.png)

- 우선 각 열의 의미를 살펴보자.

	- [Filesystem]: 사용자별 쿼터를 할당하는 파일 시스템을 의미한다. 우리는 앞에서 /etc/fstab 파일에/dev/sdb1을 쿼터로 설정해놓았다.

	- [blocks], [soft], [hard]: 현재 사용자가 사용하는 블록 (KB 단위)과 소프트 사용 한도, 하드 사용한도를 의미한다. blocks에 28이 설정되어 있으므로 현재 john이라는 사용자가 28KB를 사용한다는 의미다. [soft]와 [hard] 아래의 0은 사용 한도가 0이라는 의미가 아닌, 한도를 제한하지 않았다는 의미다. 즉 john 사용자는 용량 제한 없이 /dev/sdb1 파일 시스템 (/userHome 에 마운트되어 있음)을 사용할 수 있다.

	- [inodes], [soft], [hard]: [blocks]는 용량을 의미하지만. [inodes] inode의 개수를 의미한다(파일의 개수라고 생각하면 이해가 쉬울 것이다). john 사용자는 현재 7개의 파일을 사용하며 한도는 제한하지 않았다는 뜻이다.

- [inodes] 부분은 그냥 두고, [blocks] 부분에 사용량 제한을 걸어보자. John 사용자의 사용량을 [soft]는 20MB(20,480KB), [hard]는 30MB(30,720KB)로 제한하고 저장하자. 칸을 정확히 맞출 필요는 없으며 차례만 틀리지 않으면 된다 (vi 에디터를 사용하듯 [a]를 눌러 편집을 시작하고, 편집이 끝나면 [Esc]누른 후 :wq'를 입력한다).

![image114](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image114.png)

> 사용자별이 아닌 그룹별로 쿼터를 설정하려면 <b>edquota -g</b> 그룹이름 명령을 실행한다.

- 이제는 john 사용자가 사용할 수 있는 용량이 설정한 대로 제한되었는지 확인해보자. john 사용자로 접속한 후 파일을 몇 개 복사한다. /boot/vmlinuz-4.18.0-80.el8.x86_64 파일의 크기가 약 7.5MB이므로 이 파일을 사용한다.

```
su - john
$ pwd
$ cp /boot/vmlinuz-4* test1   -> 약 7.5MB 사용
$ cp test1 test2  -> 약 15.0MB 사용
$ cp test1 test3  
	-> 약 22.5MB 사용 : 소프트 한도(20MB) 초과. (경고 출력)
$ ls -l    
	-> test3 파일이 소프트 한도를 넘었지만 파일은 정상적으로 복사됨
	
$ cp test1 test4 
	-> 약 30MB 사용: 하드 한도(30MB)를 초과해서 더 사용할 수 없음
	
$ ls -l 
	-> test4 파일은 하드 한도까지 사용할 수 있는 남은 용량 만큼 파일이 생성됨.
	    그러므로 test4는 정상적인 파일이 아님
```

![image115](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image115.png)

- quota 명령을 입력하면 자신에게 할당된 하드디스크 공간을 확인할 수 있다.

![image116](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image116.png)

- [blocks]는 현재 사용자 (john)가 사용하는 하드디스크 공간이다. [limit](=hard)가 30.720KB이므로 이미 제한된 사용량을 모두 사용했다. 그런데 john 사용자에게 허용된 실제 사용량은 [quota](=soft)인 20,480KB다. 이를 넘는 공간인 10,240KB (30,720-20,480KB)는 [grace](유예 기간 동안인 6일 (또는 7일) 동안만 사용할 수 있다. 그러므로 john 사용자는 6일 안에 자신의 [quota] 사용량인 20,480KB를 넘는 공간을 정리해야 한다.

#### step 5
- <b>repquota /userHome</b> 명령을 입력해 사용자별 현재 사용량을 확인해보자. 먼저 <b>exit</b> 명령을 입력해 root 사용자의 권한으로 실행해야 한다.

![image117](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image117.png)

> 소프트 한도를 초과한 사용량의 유예 기간(grace period)은 기본 설정이 7일이다. 이 유예 기간은 <b>edquota -t</b> 명령을 사용해서 변경할 수 있다.

#### step 6

- 이번에는 bann 사용자에게도 john 사용자와 똑같이 사용량을 할당해보자. 
- john 사용자에게 적용된 사항을 bann 사용자에게도 동일하게 적용시키면 좀 더 간단하게 작업할 수 있다. <b>edquota -p 기준사용자 대상사용자</b> 명령을 입력하면 된다. 작업이 끝나면 <b>repquota /userHome</b> 명령을 입력해 사용자별 현재 사용량을 확인해보자.

![image118](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image118.png)

> 더 이상 쿼터를 사용하지 않으려면 <b>quotaoff /userHome</b> 명령을 실행한다.