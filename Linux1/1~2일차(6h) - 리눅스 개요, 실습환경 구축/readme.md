# 리눅스 개요

- '유닉스'라는 운영체제는 리눅스가 탄생하기 이전부터 널리 사용되었으며, 현재까지도 많이 사용되는 운영체제 중 하나다. 유닉스는 상용 소프트웨어로 발전되었고, 현재는 무척 비싼 비용을 지불해야 사용할 수 있다.

> 유닉스도 여러 회사에서 각자의 특성에 맞게 제작/판매되고 있다. 업체별로 IBM의 AIX, HP의 HP-UX, 오라클(Oracle)의 Solaris, DEC의 Tru64 Unix, Xinuos의 OpenServer 등이 많이 사용된다.

- 이러한 유닉스를 대체할 수 있는 것이 리눅스다. 리눅스를 간단히 표현한다면 '무료 유닉스' 정도로 생각할 수 있다. 즉 대부분의 유닉스는 비싼 비용을 지불해야 사용할 수 있지만, 리눅스는 유닉스와 거의 동일한 기능과 역할을 하는 운영체제면서도 무료로 사용할 수 있으며, 어떤 면에서는 유닉스보다 뛰어난 기능을 발휘한다.

## 리눅스의 탄생

- 1991년 8월 리누스 토르발스 Linus B. Torvalds는 어셈블리어로 리눅스 커널 Kernel 0.01 버전을 처음 작성했다. 그 당시 리누스 토르발스의 목표는 당시 유닉스 시스템의 작은 버전이었던 미닉스 Minix보다 좋은 운영체제를 만드는 것이었다. 이후 1992년에 0.02 버전을 작성하면서 인터넷에 소스 코드를 공개했는데, 이것이 리눅스의 탄생이 되었다

- 흔히 현재의 리눅스를 리누스 토르발스가 혼자서 개발했다고 오해하는 사람이 많다. 실제로 리누스토르발스는 커널Kernel이라고 부르는 리눅스의 핵심 부분만 작성해서 배포했다.

- 커널은 리눅스의 핵심 부분이다. 자동차에 비유하면 '엔진' 정도로 볼 수 있겠다.

- 일반적으로 사람들이 이야기하는 리눅스는 리누스 토르발스가 만든 커널에 컴파일러, 셸, 기타 응용프로그램들이 조합된 배포판을 가리킨다. 그리고 이러한 배포판은 여러 가지 응용 프로그램을 조합해 많은 리눅스 단체 또는 회사가 자신의 이름을 붙여서 판매/배포한다(그중 대표적인 배포판의 하나가 'CentOS 리눅스다).

#### 일반적인 리눅스 배포판의 구성

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image3.png)

- 리눅스는 GNU 프로젝트에 의해 완성되었으므로 정확히는 GNU/Linux라고 부르는 것이 맞다.

## GNU 프로젝트
- 리누스 토르발스가 리눅스 커널을 개발하기 전인 1984년, 리처드 스톨먼Richard Stallman에 의해 GNU프로젝트가 시작되었다. GNU 프로젝트의 목표는 '모두가 공유할 수 있는 소프트웨어'를 만드는 것이었고, 리처드 스톨먼은 1985년에 자유 소프트웨어 재단 Free Software Foundation, ESF을 설립했다. FSF는GNU 프로젝트에서 제작한 소프트웨어를 지원함으로써 컴퓨터 프로그램 복제, 변경, 소스 코드 사용에 걸린 제한을 철폐하는 것이 목표였다. 즉 누구든지 소프트웨어를 자유롭게 사용하도록 한다는 것이었다.

- FSF에서 제공하는 대부분의 소프트웨어는 GPL General Public License이라는 라이센스를 따르도록 되어 있다. 라이선스는 자유 소프트웨어 Free Software의 수정과 공유에 있어서 기본적으로 자유를 보장한다.

- 모든 소스 코드가 완전히 공개되어 있는 자유 소프트웨어는 프리웨어 Freeware 무료 소프트웨어라는 개념을 뛰어 넘어 다음과 같은 '진정한 자유 Freedom'에 대한 개념을 내포하고 있다.
	- 소프트웨어 사용에 대한 자유
	- 소프트웨어 수정에 대한 자유
	- 소프트웨어 재배포에 대한 자유
	- 수정된 소프트웨어의 이익을 전체가 얻을 수 있도록 배포할 수 있는 자유
	
#### 자유 소프트웨어가 발전하는 이유

- 자유 소프트웨어는 심지어 무료로 얻은 소프트웨어를 유상으로 판매할 수 있는 자유도 보장한다. 일반적으로무료로 얻은 것을 그대로 유상으로 판매하지는 않을 것이며 소프트웨어의 기능을 추가/향상시킨 후 판매할 것이라고 생각하기 때문이다. 그 대신 자신이 판매하는 소프트웨어도 자유 소프트웨어로 소스 코드를 공개해야한다. 그러면 또 누군가 소프트웨어를 더욱 개선시켜 더 좋아지게 할 것이다. GNU 프로젝트는 이렇게 함으로써 소프트웨어가 계속해서 반복적으로 발전하게 된다고 생각한다.

- 이외의 자세한 사항은 'GNU 선언문'을 읽어보자. GNU 홈페이지(http://www.gnu.org/)에서원문과 한글 번역문 등 자세한 내용을 확인할 수 있다.

### 커널

- 커널Kernel에는 다음 그림에 나와 있듯이 현재 제어하는 하드웨어 장치의 지원 여부 정보, 하드웨어 성능, 하드웨어를 제어하는 코드들이 들어 있다. 
- 리누스 토르발스는 이 ‘커널'이라고 부르는 리눅스의 핵심을 개발했고 지금도 계속 업그레이드 중이다. 
- 리눅스 커널 아카이브 (https://www.kernel.org/)에서 항상 최신 버전의 리눅스 커널을 다운로드할 수 있다.

- 배포되는 리눅스 커널의 버전은 안정 버전(Stable Version)과 개발 버전(Developmental Version)으로 나뉘어 있다. 안정 버전은 이미 검증된 개발 완료 코드로 구성되어 있으며, 개발 버전은 현재 개발 중인 버전이므로 상대적으로 불안정하다. 개발 버전의 경우 안정 버전이 나오기 전에 미리 추가된 기능을 접하고 싶을 때 사용할 수 있다.

- 커널은 5.3.2 버전을 예로 들면, 파일 이름에 붙은 5.3.2라는 숫자를 살펴보면, 5는 주 버전(Major Version), 3은 부 버전(Minor Version), 2는 패치 버전(Patch Version)을 의미한다.

#### 리눅스 커널 버전의 의미

- 리눅스 커널 2.x 버전에서는 부 버전이 홀수일 경우 개발용 (테스트용) 버전을 의미하고, 짝수일 경우 안정 버전을 의미했다. 일례로 2.5는 개발자용 2.6은 안정화 버전이었다. 하지만 3.x 버전부터 부 버전의 숫자는 단지 업그레이드를 표시하는 데만 사용되고 있다.
- 리눅스의 가장 큰 특징 중 하나는 배포판에 포함된 기본 커널을 사용자가 직접 최신 커널로 업그레이드할 수 있다는 점이다. 이러한 과정을 '커널 업그레이드' 또는 '커널 컴파일'이라고 한다.

* * * 
# CentOS 리눅스 소개

## 레드햇 리눅스와 CentOS 리눅스

- 일반 사용자의 경우 리눅스 커널만으로는 리눅스를 사용할 수 없다. 이런 이유로 여러 회사나 단체에서 리눅스 커널에 다양한 응용 프로그램을 추가해 쉽게 설치할 수 있도록 만든 것이 바로 리눅스 '배포판'이다. 배포판의 종류는 수백 가지가 넘으며, 우리나라에서 주로 사용하는 유명한 배포판도10여 가지나 된다.

- 비교적 잘 알려진 리눅스 배포판에는 Red Hat Enterprise Linux, Gentoo, Ubuntu Linux, Debian, Fedora, Knoppix, linux Mint, Mandriva, openSUSE, Pardus 등이 있다. 그중에서 전 세계적으로 가장 유명한 배포판 중 하나가 레드햇(Red Hat)사에서 제작한 '레드햇 리눅스(RedHat Linux)'다. 예전에 레드햇 리눅스는 유료 버전과 무료 버전을 모두 배포했으나, 현재 레드햇 리눅스의 의미는 상용으로 판매되는 레드햇 엔터프라이즈 리눅스(Red Hat Enterprise Linux)(줄여서 RHEL)만을 의미한다. 레드햇사에서는 '레드햇 리눅스 9.0' (2003년 3월)을 마지막으로 더는 무료로 리눅스를 배포하지 않고 있다.

- 비록 레드햇 엔터프라이즈 리눅스가 상용으로 판매되더라도 GPL 라이선스를 따라야 하므로 소스를공개해야 한다. 이렇게 공개된 레드햇 엔터프라이즈 리눅스의 소스 코드를 그대로 가져와서 로고만 변경한 후, 다시 컴파일(또는 빌드)하여 만든 것이 CentOS(The Community ENTerprise Operating System) 리눅스다. 결국 레드햇 엔터프라이즈 리눅스와 CentOS 리눅스는 완벽하게 동일하다고 보면 된다.

- 기업에서는 별도의 비용이 있다면 레드햇 엔터프라이즈 리눅스를 구매해서 사용하면 되고, 비용을 절감하고 싶다면 동일한 리눅스인 CentOS를 사용하면 된다. 물론 일반인이 CentOS를 사용해도아무 문제가 없으며 잘 작동한다.

- 또 다른 차이점이라면 유료로 구매한 레드햇 엔터프라이즈 리눅스는 설치, 문제 해결 등에 대한 기술지원이 된다는 장점이 있지만, 무료인 CentOS는 자체적으로 문제를 해결해야 한다.

#### RHEL, CentOS, Fedora의 관계
- Red Hat사는 CentOS뿐 아니라 Fedora Project도 재정적으로 지원하고 있다. Fedora 리눅스는 Red HatEnterprise Linux의 베타 버전 개념이며 미리 최신 기능을 테스트하기 위한 용도로 제작된다. 이렇게 미리 만들어진 Fedora 리눅스를 안정화시켜서 Red Hat Enterprise Linux를 완성하고 이 Red Hat EnterpriseLinux를 가지고 CentOS를 만들게 되는 것이다. 예를 들어 CentOS 8 이 제작된 흐름은 Fedora28(2018년 5월) → RHEL 8 (2019년 5월) → CentOS 8 (2019년 9월)로 보면 된다.

### CentOS 8을 설치하기 위한 하드웨어 요구 사항
- 진짜 컴퓨터에 CentOS 8을 설치하기 위한 최소/권장 하드웨어 사양은 다음과 같다(우리는 가상머신을 사용하기 때문에 다음 요구 사항과 차이가 있을 수 있다)
	- CPU: 64bit CPU
	- 하드디스크 여유 공간: 20GB 이상의 여유 공간 권장(추가 설치 부분에 따라 달라질 수 있음)
	- 메모리 : 권장 4GB (최소 2GB)

- 그밖의 자세한 사항은 CentOS 문서CentOS Documentalon의 릴리스 노트(https://wiki.centos.org/Manuals/ReleaseNotes/CentOSStream)를 참조하자.

* * * 
# 실습 환경 구축

## Oracle Virtual Box 설치
- [VirtualBox 다운로드](https://www.virtualbox.org/wiki/Downloads)
	- Windows OS를 사용하는 경우 [Windows Hosts](https://download.virtualbox.org/virtualbox/6.1.34/VirtualBox-6.1.34a-150636-Win.exe)  클릭
	- Mac OS를 사용하는 경우 [OS X hosts](https://download.virtualbox.org/virtualbox/6.1.34/VirtualBox-6.1.34-150636-OSX.dmg) 클릭 
	
	![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image4.png)
	
- 다운로드 받은 설치파일을 실행하여 다음과 같이 설치합니다.
	
	![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image5.png)
	
	![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image6.png)
	
	![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image7.png)

	![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image8.png)
	
	![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image9.png)
	
	![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image10.png)
	
- 설치가 완료 되면 다음과 같은 화면을 볼 수 있습니다.
	![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image11.png)
	
## 실습을 위한 가상머신 설치 

- 실습을 위해서는 3개의 CentOS와 1개의 Windows 11 가상머신을 설치해야 합니다.
- 다음과 같이 가상공간을 만들어 생성합니다. 
- 우선은 Server 명칭으로 가상머신 공간을 다음과 같이 생성합니다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image12.png)

- 메모리 크기는 RAM 용량을 의미합니다. 1GB 정도로 설정하였으나 클 수록 쾌적하게 테스트 할 수 있으므로 여유가 있다면 좀 더 설정해도 됩니다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image13.png)


![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image14.png)

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image15.png)


- 가상 하드디스크는 사용하는 용량대로 커지게 하고 최대 가능 사이즈를 조정할 수 있도록 동적 할당으로 체크합니다.
![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image16.png)

- 하드디스크는 넉넉하게 최대 80GB정도로 설정합니다(하드 용량이 넉넉하지 않다면 50G 정도 설정합니다.)

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image17.png)


- 네트워크 설정은 NAT로 설정합니다.

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image18.png)

- Server(B), Client 명칭으로 동일한 방법으로 가상머신을 생성합니다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image19.png)

## CentOS 리눅스 설치
- CentOS 리눅스 설치하는 방법은 몇 가지 있지만, 가장 쉽고 일반적인 방법은 DVD를 이용해서 윈도우와 비슷한 설치 마법사 환경으로 설치하는 것이다. 
- CentOS 리눅스는 CentOS 웹사이트에서 [다운로드](https://www.centos.org/download/) 할 수 있다.

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image20.png)

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image21.png)



### 가상머신 : Server 설치

- 설정 -> 저장소 -> 컨트롤러 IDE 의 추가 버튼 클릭 -> 추가 -> 다운받은 CentOS-Stream-8을 선택 -> 선택 클릭 

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image22.png)

- 확인 버튼을 클릭
![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image23.png)

- 시작 버튼을 클릭하여 Server 가상머신을 시작한다.

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image24.png)

- Intstall CentOS Stream 8-stream을 선택한다.

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image25.png)

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image26.png)

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image27.png)

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image28.png)

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image29.png)

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image30.png)

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image31.png)

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image32.png)

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image33.png)

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image34.png)

![image35](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image35.png)

#### 리눅스 파티션
- 디스크 파티션에 관해 알아야 할 내용이 있다. 우선 리눅스 파티션은 루트 파티션이라고 부르는 '/' 파티션과 'swap' 파티션 2개만 있어도 운영이 가능하다. 물론 실무에서는 실무에서는 리눅스를 운영할 때는 지금과 같이 파티션을 두개로 나누지 않고 필요한 용도에 따라서 다양하게 분할한다.
- 일반적인 용도로는 80G 하드디스크를 기준으로 다음과 같이 나눌 수 있으니 절대적인 기준은 아니며 리눅스의 용도에 따라 달라질 수 있다.

|마운트 포인트|권장 크기|비고|
|-----|------|------|
|/|10GB|루트 파티션|
|/bin||기본 명령어가 들어 있음|
|/sbin||시스템 관리용 명령어가 들어 있음|
|/etc||시스템 환경 설정과 관련된 파일이 들어 있음|
|/boot||4G|부팅 저장 커널이 저장됨
|/media||외부 장치를 마운트하기 위해 제공됨|
|/usr|설치할 응용 프로그램에 따라 크기 다름(주로 20GB 내외)|응용 프로그램이 주로 저장됨|
|/lib||프로그램의 라이브러리가 저장됨|
|/dev||장치 파일들이 저장됨|
|/proc||시스템 프로세서 정보, 프로그램 정보, 하드웨어 정보 등이 들어 있음|
|/tmp|4GB|임시파일이 저장됨|
|/var|10GB|로그, 캐시 파일 등이 저장됨|
|/root||시스템 관리자인 root의 홈 디렉토리|
|/home|사용자가 많을 수록 많이 할당(나머지 용량)|사용자별 공간|
|/lost+found|파일 시스템 복구를 위한 디렉토리|
|swap 파티션|RAM의 2배 정도|RAM 부족 시 사용되는 공간|

- 최소 루트 파티션(/)과 swap 파티션만 생성해도 운영이 가능한 이유는 루트 파티션(/)만 생성하면 상기 표에 나오는 나머지 파티션(/bin, /etc, /boot, /usr, /tmp, /var, /home 등)이 모두 루트 파티션(/) 아래 종속되기 때문이다.

![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image36.png)

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image37.png)

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image38.png)

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image39.png)

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image40.png)

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image41.png)

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image42.png)

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image43.png)

![image44](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image44.png)

![image45](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image45.png)

![image46](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image46.png)

![image47](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image47.png)

![image48](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image48.png)

![image49](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image49.png)

![image50](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image50.png)

![image51](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image51.png)

![image52](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image52.png)

![image53](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image53.png)

![image54](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image54.png)

![image55](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image55.png)

![image56](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image56.png)

![image57](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image57.png)

![image58](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image58.png)

![image59](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image59.png)

![image60](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image60.png)

![image61](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image61.png)

![image62](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image62.png)

```
gsettings set org.gnome.software download-updates false
systemctl disable dnf-makecache.service
systemctl disable dnf-makecache.timer
```

![image63](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image63.png)


- Server의 IP는 10.0.2.100으로 변경할 것이다.
- [현재 활동]에서 즐겨찾기의 [터미널] 아이콘을 실행한다.
- 터미널에서 관련 디렉토리로 이동한 후 파일을 편집한다.

```
cd /etc/sysconfig/network-scripts/ -> 네트워크 설정 파일이 저장된 디렉토리로 이동
ls    -> ifcfg-xxxx 파일 확인(예 : ifcfg-enp0s3)
gedit ifcfg-xxxx
```

![image64](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image64.png)

- 다음과 같이 내용을 수정하자 다음은 Server에 고정 IP를 할당하는 것이다(대소문자를 정확히 구분하고 각 글자 사이는 띄어쓰기 없이 입력해야 한다.)
	- 수정 : BOOTPROTO=dhcp  -> BOOTPROTO=none
	- 추가 : IPADDR=10.0.2.100
	- 추가 : NETMASK=255.255.255.0
	- 추가 : GATEWAY=10.0.2.2
	- 추가 : DNS1=8.8.8.8

![image65](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image65.png)


- 터미널에서 다음 명령을 입력하여 설정한 내용을 적용시키고 컴퓨터를 재부팅 한다.
	- nmcli connection down 장치 이름 -> 네트워크 장치 중지
	- nmcli connection up 장치_이름 -> 네트워크 장치 시작
	- reboot -> 컴퓨터 재부팅
	
- 다시 재부팅 되면 [목록에 없습니까?]를 클릭한 후 root/password로 로그인 한다.
- 왼쪽 상단의 [현재활동]->[터미널]을 선택해서 터미널을 연다.

![image66](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image66.png)

- ifconfig enp0s3

![image67](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image67.png)

- 보안이 설정된 SELinux 기능을 끄자.
- 터미널에서 다음 명령을 입력해 SELinux 설정 파일을 편집하자

```
gedit /etc/sysconfig/selinux -> 파일 편집
```

- 편집기가 열리면 6행의 'SELINUX=enforcing'을 'SELINUX=disabled'로 수정하고, 저장한 후 편집기를 닫는다.

![image68](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image68.png)

- exit 명령으로 터미널을 닫는다.

- 한글 사용을 위해 약간의 설정이 필요하다.
	- 바탕화면에서 마우스 오른쪽 버튼을 클릭한 후 [설정]을 클릭한다. [설정] 초기화면이 아니라면 왼쪽 위 \<\<\>를 클릭해서 설정 초기화면으로 돌린다.
	- [지역 및 언어]를 선택하고 [입력 소스]의 [한국어]를 선택한 후 <->를 눌러서 삭제한다. 즉, '한국어(Hangul)' 하나만 남겨둬야 한다. 설정을 마쳤으면 오른쪽 위에 있는 <X>를 클릭해서 [설정] 창을 닫는다.
	
![image69](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image69.png)

- 이제부터는 한글이 잘 변경된다. 왼쪽 위의 [현재활동] -> [터미널]을 선택한 후 한글을 입력해보자. 한/영 전환은 Shift + Space이다.

![image70](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image70.png)

- 앞으로 자주 사용될 패키지를 미리 설치해놓자. dnf -y install firewall-config 명령으로 설치한다.

![image71](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image71.png)


- 오른쪽 위에 있는 전원 모양 버튼을 클릭하고 다시 전원 모양 버튼을 클릭한 후 \<컴퓨터 끄기\>를 클릭해서 Server를 종료한다. 이로써 Server의 설치와 설정은 완전하게 마무리 되었다.

![image73](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image73.png)

- 만약 전체 메모리가 8GB 이상이라면 2048MB 이상으로 조정한다.

![image74](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image74.png)

- 설정이 완료된 Server를 스냅샷하자
	- 설치된 가상머신의 오른쪽 더보기 메뉴를 클릭한 후 '스냅샷'을 선택합니다.
	
	![image75](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image75.png)
	
	- 상단의 스냅셧 메뉴 중에서 '찍기'를 선택합니다.
	
	![image76](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image76.png)
	
	- 스냅샷 이름과 설명을 입력한 후 클릭하면 스냅샷이 생성됩니다.
	
	![image77](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image77.png)
	
	![image78](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image78.png)
	
	- 스냅샷은 여러번 찍을 수 있으며 트리 형태의 단계로 저장됩니다.
	- 만일 가장 최근에 찍은 스냅샷이 있는데, 이전 스냅샷으로 복원을 한 다음 다시 스냅샷을 찍으면 가상 머신의 변경점을 기준으로 트리가 생성되어 여러 시나리오를 만들 수 있습니다.
	



	
	