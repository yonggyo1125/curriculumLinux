# 파일 압축과 묶기

## 파일 압축

- 리눅스에서 많이 볼 수 있는 압축 파일의 확장명은 xz, bz2, gz, zip, Z 등이다. 예전에는 주로 확장명 gz를 사용했으나, 최근에는 압축률이 더 좋은 xz나 bz2를 더 많이 사용하는 추세다. 이 파일들을 관리하는 명령어는 다음과 같다.

#### xz

- 확장명 xz로 압축하거나 풀어줌. 비교적 최신 압축 명령이며 압축이 뛰어남
- 사용 예

```
# xz 파일이름   -> '파일 이름'을 압축 파일인 '파일이름.xz'로 만들며 <b>기존 파일은 삭제됨</b>
# xz -d 파일 이름.xz(d는 Decompress의 의미)
		-> '파일이름.xz' 압축 파일을 일반 파일인 '파일이름'으로 만듬
# xz -l 파일이름.xz(l은 List의 의미)
		-> '파일이름.xz' 압축 파일에 포함된 파일 목록과 압축률 등을 출력
		
# xz -k 파일이름(k는 Keep의 의미)
		-> 압축 후에 기존 파일을 삭제하지 않고 그대로 둠
```

#### bzip2 

- 확장명 bz2로 압축하거나 풀어줌
- 사용 예

```
# bzip2 파일이름   -> '파일이름'을 압축 파일인 '파일이름.bz2'로 만듬
# bzip2 -d 파일이름.bz2     -> '파일이름.bz2' 압축 파일을 일반 파일인 '파일이름'으로 만듬
```


#### bunzip2

- 확장명 bz2의 압축을 풀어줌
- 'bzip2 -d'와 동일한 명령


#### gzip

- 확장명 gz로 압축하거나 풀어줌
- 사용 예

```
# gzip 파일이름   -> '파일이름'을 압축 파일인 '파일명.gz'로 만듬
# gzip -d 파일이름.gz  -> '파일이름.gz' 압축 파일을 일반 파일인 '파일이름'으로 만듬
```

#### gunzip

- 확장명 gz의 압축을 풀어줌
- 'gzip -d'와 동일한 명령

#### zip

- Windows용과 호환되는 확장명 zip으로 압축하거나 풀어줌
- 사용 예

```
# zip 설정할파일이름.zip 압축할파일이름
		-> 압축할 파일 이름을 '새로생성할파일이름.zip'으로 만듦
```

#### unzip

- Windows 용과 호환되는 zip으로 묶은 압축 파일을 풀어줌
- 사용 예

```
# unzip 압축파일이름.zip    -> '압축파일이름.zip'의 압축을 풀어줌
```

## 파일 묶기

- 알집(Alzip)이나 반디집(bandizip) 같은 Windows용 압축 프로그램을 생각해보면 aaa, bbb라는 2개 파일을 압축했을 때 ccc.zip이라는 1개의 압축 파일이 생긴다. 즉 aaa와 bbb라는 두 파일이 ccc라는 1개의 파일로 묶인 후 압축된 것이다. 이는 Windows 압축 프로그램이 '파일 압축'과 '파일 묶기'를 한꺼번에 하기 때문이다.

- 이와 조금 다르게 <b>리눅스(유닉스)에서는 '파일 압축'과 '파일 묶기'를 원칙적으로 별개의 프로그램으로 실행하도록 되어 있다.</b> 물론 사용자 편의를 위해 한 번에 할 수 있는 옵션도 제공한다. 파일 묶기 명령어는 tar이며 묶인 파일의 확장명도 tar다.

#### tar 
- 확장명 tar로 묶음 파일을 만들거나 묶음을 풀어줌

- 동작
	- c(소문자)  -> 새로운 묶음을 만듦
	- x       -> 묶인 파일을 풀어줌
	- t       -> 묶음을 풀기 전에 묶인 경로를 보여줌
	- C(대문자)  -> 묶음을 풀 때 지정된 디렉토리에 압출을 풀어줌.<br>지정하지 않으면 묶을 때와 동일한 디렉토리에 묶음이 풀림

- 옵션
	- f(필수)    -> 묶음 파일 이름 지정. 원래 tar은 테이프(tape) 장치 백업이 기본임(생략하면 테이프로 보내짐)
	- v     -> visual의 의미로 파일이 묶이거나 풀리는 과정을 보여줌(생략가능)
	- J(대문자)   -> tar + xz
	- z(소문자)  -> tar + gzip
	- j(소문자)   -> tar + bzip2
	
-  사용 예

```
# tar cvf my.tar /etc/sysconfig/  -> 묶기 
# tar cvfJ my.tar.xz /etc/sysconfig/  -> 묶기 + xz 압축
# tar cvfz my.tar.gz /etc/sysconfig/  -> 묶기 + gzip 압축
# tar cvfj my.tar.bz2 /etc/sysconfig  -> 묶기 + bzip2 압축
# tar tvf my.tar   -> 파일 확인
# tar xvf my.tar   -> tar 풀기
# tar cxvf newdir my.tar     -> newdir에 tar 풀기
# tar xfJ my.tar.xz      -> xz 압축 해제 + tar 풀기
# tar xfz my.tar.gz     -> gzip 압축 해제 + tar 풀기
# tar xfj my.tar.bz2    -> bzip2 압축 해제 + tar 풀기
```

- 자주 사용할 명령은 <b>tar xvfJ 파일이름.tar.xz</b> 명령과 <b>tar xvfj 파일이름.tar.bz2</b> 명령 정도다. 최소한 두 가지 명령은 기억해놓자.

* * * 
# 파일 위치 검색

- 리눅스에서 특정 파일의 위치를 검색하는 명령어는 다음과 같다. 가장 많이 사용되는 명령어는 find다. 다음 


#### find 경로 옵션 조건 action

- 옵션  -> -name, -user(소유자), -newer(전, 후), -perm(허가권), -size(크기)
- action -> -print(기본값), -exec(외부 명령 실행)

- 기본 사용 예

```
# find /etc -name "*.conf"  -> '/etc' 디렉토리 하위에 확장자명이 "*.conf"인 파일 검색
# find /home -user centos  -> '/home' 디렉토리 하위에 소유자가 centos인 파일 검색
# find ~ -perm 644    -> 현재 사용자의 홈디렉토리 하위에 허가권이 644인 파일 검색
# find /usr/bin -size +10k -size -100k
		-> /usr/bin 디렉토리 하위의 파일 크기가 10KB~100KB인 파일 검색
```

- 고급 사용 예

```
# find ~ -size 0k -exec ls -l { } \;
		-> 현재 사용자의 홈 디렉터리 하위에 파일 크기가 0인 파일의 목록을 상세히 출력
		
# find /home -name "*.swp" -exec rm { } \;
		-> /home 디렉토리의 하위에 확장명이 *.swp인 파일 삭제
```

> find /home -name "\*.swap" -exec rm { } \; 명령의 의미는 다음과 같다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image1.png)

#### which 실행파일 이름

- PATH에 설정된 디렉토리만 검색
- 절대 경로를 포함한 위치 검색

#### whereis 실행파일 이름

- 실행 파일 및 소스, man 페이지 파일까지 검색

#### locate 파일이름

- 파일 목록 데이터베이스에서 검색하기 때문에 매우 빠르고 유용하지만 updatedb 명령을 1회 실행해야 사용할 수 있음. updatedb 명령 실행 이후에 설치된 실행 파일은 찾을 수 없으므로, 다시 updatedb 명령을 실행해야 찾을 수 있음

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image2.png)

* * *
# 시스템 설정

- CentOS의 X 윈도 환경에서 제공하는 시스템의 설정 명령을 사용하면 여러 가지 시스템 설정으로 좀 더 편리하게 사용할 수 있다.

## 표준 시간대 변경

- [설정]의 [자세히 보기] → [날짜 및 시각] 부분에서 표준 시간대를 변경할 수 있다.


![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image3.png)

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image4.png)

## 네트워크 설정

- <b>nmtui</b> 명령어. 네트워크 개념을 학습하고 자세히 다룬다.


## 방화벽 설정

- <b>firewall-config</b> 명령어. 외부에 서비스하기 위해 포트를 열 때 사용한다.  강의 후반부에 네트워크 서버를 구축할 때 자주 사용할 명령어다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image5.png)


## 서비스(데몬) 설정

- <b>ntsysv</b> 명령어, 서비스(데몬)의 시작, 중지, 재시작 및 사용 여부를 설정할 때 사용한다. 서비스(데몬)의 개념은 잠시 후에 다룬다.

> 먼저 dnf -y install ntsysv 명령으로 설치해야 한다.


* * * 
# CRON과 AT

## CRON 

- 시스템을 가장 적게 사용하는 새벽 5시에 백업해야 할 경우, 하루 이틀쯤은 퇴근하지 않고 기다릴 수 있겠지만 매일 그래야 한다면 아마도 회사를 그만두고 싶어질 것이다. 이런 경우 주기적으로 반복되는 일을 자동으로 실행할 수 있도록 시스템 작업을 예약해놓는 것을 <b>cron</b>이라 부른다. <b>cron</b>과 관련된 데몬(서비스)은 <b>crond</b>이고, 관련 파일은 <b>/etc/crontab</b>이다.

- <b>/etc/crontab</b>의 형식은 다음과 같다. 

```
분 시 일 월 요일 사용자 실행명령
```

- 분에는 0~59, 시에는 0~23, 일에는 1~31, 월에는 1~12, 요일에는 0~6이 올 수 있다. 요일은 0부터 일요일로 시작한다. 사용자는 명령을 실행할 사용자가, 실행 명령에는 그 시간에 실행할 명령이 올 수 있다. 간단한 예를 보면 다음과 같다.


```
00 05 1 * * root cp -r /home/backup
```

- 네 번째인 월 부분에 입력한 는 매월을 의미한다. 네 번째부터 거꾸로 읽으면 매월 1일 새벽 5시00분에 실행한다. 요일 부분도 모든 요일을 의미하는 \*로 표시했다. 즉, 요일은 상관하지 않는다. 사용자는 root의 권한이며 명령은 <b>cp -r /home /backup</b> 명령을 실행한다. /home 디렉터리가 통째로 /backup 디렉터리에 복사된다.

- 하나 더 기억할 사항은 cron의 경우 주기적으로 실행할 내용을 디렉터리에 넣어놓고 작동한다는 점이다. 해당 디렉터리의 구조는 다음과 같다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image6.png)

- /etc/crontab 파일이 시간별, 일별, 주별, 월별로 호출하는 디렉터리를 보여준다. 그래서 일반적으로 crontab 파일에 다음과 같은 내용을 입력해둘 수 있다.

```
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
03 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

- 첫 줄은 매시간 1분에 /etc/cron_hourly 디렉터리 안의 명령들을 자동으로 실행한다. 나머지 행의 의미도 앞에서 설명했던 것과 마찬가지다. 
- <b>run-parts 디렉토리</b> 명령어는 디렉토리 안의 명령어를 모두 실행한다.

## AT

- cron은 주기적으로 반복되는 작업을 예약하는 것이지만, <b>at 명령어는 일회성 작업을 예약하는 것이다.</b> 즉 예약해두면 한 번만 실행되고 소멸된다.

- 명령어 사용법은 다음과 같다.

#### 예약 
- at 시간

```
at 3:00am tomorrow     -> 내일 새벽 3시
at 11:00pm January 30  -> 1월 30일 오후 11시
at now +1 hours       -> 1시간 후 
- at 프롬프트에 예약 명령어 입력 후 [Enter] 누름
```
- 완료되면 Ctrl + D 누름

#### 확인 
- at -l


#### 취소 

- atrm 작업번호


## 실습1

매월 15일 새벽 3시 1분에 /home 디렉터리와 그 하위 디렉터리를 /backup 디렉터리에 백업하자.

#### step 0

- 시간 설정을 위해 먼저 <b>wget http://download.hanbit.co.kr/centos/8/openrdate-1.2-14.fc30.x86_64.rpm</b> 명령으로 패키지를 다운로드 받은 후 <b>dnf -y install openrdate\*.rpm 명령으로 시간 설정과 관련된 패키지를 미리 설치해놓자.

> rdate 명령은 타임서버의 시간을 설정할 수 있는 간단하고 편리한 명령이지만 CentOS 8에서는 제공되지 않는다. 그 대신 Fedora Linux 30에서 제공하는 openrdate 패키지를 설치해서 사용해도 잘 작동한다.


#### step 1

- <b>systemctl status crond</b> 명령으로 cron과 관련 서비스인 crond가 동작하는지 확인한다. 기본적으로 가동되어 있을 것이다. Q를 누르면 종료된다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image7.png)

> systemctl 명령은 서비스 시작, 중지, 상태 확인 등을 하는 명령이다. 잠시 후 상세히 설명한다.

#### step 2

- <b>gedit /etc/crontab</b> 명령을 입력해 예약 파일을 열고 맨 아래에 '01 3 15 \* \* root run-parts /etc/cron.monthly'를 추가한 후 저장하고 닫는다(#부분은 주석이므로 무시한다). 이미 설명했지만 이 내용은 매월 15일 새벽 3시 1분에 /etc/cron.monthly 디렉터리 안의 모든 파일을 실행하라는 의미다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image8.png)

#### step 3

- /etc/cron.monthly/ 디렉터리에 메시지를 출력하는 스크립트 파일(myBackup.sh)을 만들고, 속성을 실행할 수 있게 바꾼다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image9.png)

#### step 4

- <b>gedit myBackup.sh</b> 명령을 입력하고 파일 안에 다음을 참고해 내용을 입력한 후 저장하고 닫는다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image10.png)

> myBackup.sh 내용은 현재 날짜를 추출해서 /backup 디렉터리에 backup-현재날짜.tar.xz라는 파일로 /home 디렉터리 전체의 백업 파일을 생성하라는 의미다. 셸 스크립트 문법이라 좀 생소하겠지만, 간단하면서도 실무에서 유용하게 사용할 수 있으므로 익혀두자. 셸 스크립트는 [ 쉘 스크립트 프로그래밍](https://github.com/yonggyo1125/curriculumLinux/tree/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D) 에서 자세히 살펴본다.

#### step 5

- 백업용 디렉터리를 생성하고 crond 데몬을 재시작한다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image11.png)

-이제 매월 15일마다 /home 디렉터리를 백업할 것이다. 

#### step 6

- 한 달을 기다려서 결과를 보기에는 너무 지루할 것 같으므로 날짜를 강제로 바꾸고 테스트해보자. 01월 15일 03시 00분 2027년(011503002027)'으로 날짜를 강제로 바꾸고 crond 서비스를 재시작한다. 1분 정도 기다린 후에 설정된 내용이 잘 실행되었는지 확인해보자. 또 2월로 시간을 바꾸고 다시 실행해본다. 계속 백업된 데이터가 쌓이는 것을 확인할 수 있다.

```
date 011503002027
systemctl restart crond   -> 실행 후 1~2분 기다린다.
ls -l /backup
date 021503002027
systemctk restart crond  -> 실행 후 1~2분 기다린다.
ls -l backup
```

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image12.png)

#### step 7

- 이번에는 at 명령어로 내일 새벽 4시에 시스템을 최신 패키지로 업데이트하고, 완료되면 시스템을 재부팅하도록 예약해보자. 그리고 예약된 내용을 삭제하는 연습도 해보자.

```
at 4:00 am tomorrow
dnf -y update
reboot
Ctrl + D 누름   -> 작업 예약을 완료한다.
at -l               -> 제일 앞에 출력되는 번호가 작업번호다.
atrm 작업번호  -> 작업을 삭제한다.
at -l
```

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/8%EC%9D%BC%EC%B0%A8(3h)%20-%20%ED%8C%8C%EC%9D%BC%20%EC%95%95%EC%B6%95%EA%B3%BC%20%EB%AC%B6%EA%B8%B0%2C%20%ED%8C%8C%EC%9D%BC%20%EC%9C%84%EC%B9%98%20%EA%B2%80%EC%83%89%2C%20%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%84%A4%EC%A0%95%2C%20CRON%EA%B3%BC%20AT/images/image13.png)

