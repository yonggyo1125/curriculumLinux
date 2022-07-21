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

#### step0 

Server를 처음 설치 상태로 초기화하자

- 아직 부팅은 하지 말자.

#### step1
SATA 1(/dev/sdb)에 1GB 하드디스크 하나를 장착하자.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image5.png)

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image6.png)

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image7.png)

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image8.png)

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image9.png)

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image10.png)

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/15~17%EC%9D%BC%EC%B0%A8(9h)%20-%20%ED%95%98%EB%93%9C%20%EB%94%94%EC%8A%A4%ED%81%AC%20%EA%B4%80%EB%A6%AC/images/image11.png)

#### step2

- 이제 Server를 부팅하고 root 사용자로 접속한다

#### step2

이제는 그림의 순서대로 장착한 하드디스크에 파티션을 할당하자. 파티션은 1개의 파티션만 할당한다. 터미널을 열고 다음을 입력한다



* * * 
# 여러 개 하드디스크를 하나처럼 사용하기

* * * 
# LVM

* * * 
# CenOS를 RAID에 설치하기

* * * 
# 사용자별로 공간을 할당하기