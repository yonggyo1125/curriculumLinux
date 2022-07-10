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

- 하드디스크는 넉넉하게 최대 20GB정도로 설정합니다.

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



### Server 설치

