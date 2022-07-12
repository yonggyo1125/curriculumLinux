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

- 메모리 크기는 RAM 용량을 의미합니다. 2GB 정도로 설정하였으나 클 수록 쾌적하게 테스트 할 수 있으므로 여유가 있다면 좀 더 설정해도 됩니다.

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

- 언어를 한국어로 선택하고 계속 진행을 클릭한다.

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image26.png)

- 시간과 날짜 항목을 선택 한 후

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image27.png)

- 지역은 "아시아", 도시는 "서울"로 선택한 후 "완료" 버튼을 클릭합니다.

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image28.png)


- 네트워크 설정을 클릭합니다.

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image29.png)

- 네ㅌ워크가 꺼 있는데 켭으로 변경 한 후 완료를 클릭합니다.

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image30.png)

- 소스트웨어 선택을 클릭 한 후 

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image31.png)

- 워크스테이션을 선택하고 완료 버튼을 클릭합니다.

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image32.png)


- 설치 목적지를 클릭합니다.

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image33.png)

- 로컬 표준 디스트에 노출되어 있는 하드 디스크를 선택하고 저장소 구성은 "사용자 정의"를 선택합니다. 그런 후에 "완료" 버튼을 클릭합니다.

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image34.png)

- 수동 파티션 설정 항목에서 "표준 파티션"으로 선택하고 하단의 "+" 버튼을 클릭합니다.

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

- 적재 지점에 "swap"이라고 입력하고 희망용량은 현재 가상머신에 할당된 램 용량의 2배로 지정합니다. 그런 후에 "적재 지점 추가"를 클릭합니다.
- swap 영역은 램 용량이 부족할때 사용하는 하드 공간입니다.

![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image36.png)

- 다시 "+" 버튼을 클릭하고 적재 지점에 "/" 를 입력하고 "적재 지점 추가"를 클릭합니다.

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image37.png)

- 생성된 내용을 확인하고 "완료" 버튼을 클릭합니다.

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image38.png)

- root 비빌번호를 클릭합니다.

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image39.png)

- root 비번은 연습의 편의성을 위해 "password"로 입력하고 "완료"를 두번 클릭합니다.

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image40.png)


- 전부 설정이 완료되면 "설치 시작" 버튼을 클릭합니다.

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image41.png)

- 다음과 같이 설치가 시작됩니다.

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image42.png)

- 설치가 완료되면 다음과 같은 화면이 노출되는데, "라이센스 정보"를 클릭합니다.

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image43.png)

- "약관에 동의합니다."에 체크하고 완료 버튼을 클릭합니다.

![image44](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image44.png)

- 사용자 생성 버튼을 클릭한 후 성명 : centos, 사용자 이름 : centos, 비밀번호는 centos로 생성합니다. 
- 실습의 편의성을 위해 동일하게 입력합니다.

![image45](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image45.png)

- "설정 완료" 버튼을 클릭합니다.

![image46](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image46.png)

- 초기 설정은 root 권한이 다소 많이 필요하므로 애초에 root 권한으로 로그인합니다. 
- "목록에 없습니까?"를 클릭합니다.

![image47](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image47.png)

- 사용자 이름은 "root"로 입력하고 "다음"버튼을 클릭합니다.

![image48](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image48.png)
 
- 설치시 설정한 "root" 비밀번호를 입력하고 "로그인" 버튼을 클릭합니다.

![image49](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image49.png)

- 초기설정에서 언어는 "한국어"로 선택하고 "다음" 버튼을 클릭합니다.

![image50](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image50.png)

- 입력 부분에도 "한국어(Hangul)"로 선택하고 "다음"버튼을 클릭합니다.

![image51](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image51.png)

- 다음 버튼을 클릭합니다.

![image52](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image52.png)

- "건너뛰기"를 클릭합니다.

![image53](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image53.png)


- 준비 완료 페이지가 나오면 "CentOs Stream 시작" 버튼을 클릭합니다.

![image54](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image54.png)

- 기본 화면이 작으므로 화면 사이즈를 조정합니다. 오른쪽 상단의 "전원 모양" 버튼 오른쪽에 화살표 버튼을 클릭하고 팝업 하단의 도구 모양의 아이콘을 클릭합니다.

![image55](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image55.png)

- 설정 페이지가 나오면 "장치"를 선택하고 

![image56](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image56.png)

- 디스플레이를 선택, 해상도를 1024 X 768 정도로 선택합니다.

![image57](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image57.png)

- 적용을 누릅니다.

![image58](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image58.png)

- "바뀐 사항 유지"를 클릭합니다.

![image59](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image59.png)

- 실습의 편의를 위해 화면 자동 화면 잠금을 해제 합니다.
- "개인정보"를 클릭하고 "화면 잠금"에서 자동 잠금, 알림표시를 모두 "끔" 상태로 변경합니다.

![image60](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image60.png)

- 실습의 편의를 위해 대기 모드 역시 해제 합니다. 
- "전원"을 클릭하고 "절전" 항목을 "안함"으로 변경합니다.

- 실습의 편의를 위해 소프트웨어 업데이트 기능도 해제 합니다.
	- "현재 활동"을 클릭하고 제일 아래 있는 프로그램 표시 아이콘을 클릭해서 "모두"를 선택한다. 그리고 "소프트웨어"를 클릭해서 실행한다.
	
	![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image8.png)
	
	- 상단의 더보기 메뉴를 클릭한 후 "업데이트 기본 설정"을 선택하고 모두 "끔"으로 만든 후에 창을 닫는다.
	
	![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image6.png)
	
	![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image7.png)

![image61](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image61.png)

- [현재 활동]을 클릭하고 "터미널"을 클릭합니다.
 
![image62](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/image62.png)

- 터미널에서 다음 명령어를 차례로 입력해 자동으로 업데이트 되는 기능을 끕니다.

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
	

### 가상머신 : Server(B) 설치

- Server(B)는 Server와 달리 X 윈도를 사용하지 않고 텍스트 모드에서만 사용한다. 그래서 설치가 빠르고 사용할 때도 상당히 가볍게 운영된다.

- Server(B)의 설치 과정도 앞 Sever 설치 과정과 대부분 비슷한다.
- "설정(S)" -> "저장소" ->컨트롤러 IDE에서 "비어있음"을 선택하고 다운받은 CentOS-Stream-8...iso 파일을 선택한다.
- "시작(T)" 버튼을 클릭한 후 가상머신을 시작합니다.
- Intstall CentOS Stream 8-stream을 선택한다.
- 잠시 후 언어 선택 화면이 나온다. Server(B)는 텍스트 모드로 사용할 것이므로 그냥 영문판으로 두고 \<Continue\>를 클릭한다.
> 텍스트 모드에서는 한글 입출력이 되지 않는다.

![bimage1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image1.png)

- Keyboard는 English로 되어 있고 Language Support는 English(United States)로 되어 있을 것이다. 그대로 두고 "Time & Date"를 클릭한다.

- Region은 "아시아", City는 "Seoul"로 선택하고 "Done"을 클릭한다.

![bimage3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image3.png)

- 오른쪽의 "Network & Host Name"을 클릭한다. 오른쪽 끝의 \<OFF\> 스위치를 클릭해서 \<ON\>으로 만들면 네트워크 정보가 보일 것이다. \<Done\>을 클릭한다.

![bimage2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image2.png)


![bimage4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image4.png)

- "Software Selection"을 보면 "Server with GUI"가 선택되어 있을 것이다. 클릭해서 "Minimal Install"로 선택하고 "Done"을 클릭한다.

> "Minimal Install"을 선택하면 텍스트 모드에 최소한의 패키지만 설치된다. 강의에서는 필요한 패키지가 있을 때마다 추가로 설치해서 사용할 것이다.

![bimage5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image5.png)

- "Installation Destination" 부분을 확인하면 "Automatic partitioning selection"으로 되어 있을 것이다. 변경해야 하므로 클릭한다.
- "Installation Destination"에서는 80GB 크기의 하드 디스크가 그림처럼 보인다. 하드디스크 그림을 천천히 2회 클릭하여 하드디스크가 파란색으로 선택되고 체크 모양의 아이콘이 보이는 상태가 되는 것을 확인한다. 그리고 아래쪽의 "Custom"을 선택한 다음 "Done"을 클릭한다.

![bimage6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image6.png)

- "MANUAL PARTITIONING"에서는 중간쯤 "Standard Partition"으로 변경하고, 아래쪽 "+"를 클릭해서 Mout Point는 사상 메로미로 사용되는 swap을, Desired Capacity는 4G를 할당한 후 "Add mount point"를 클릭한다.

![bimage7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image7.png)

![bimage8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image8.png)

- 다시 "+"를 클릭한 후 이번에는 Mount Point로 "/"를 선택하고, Desired Capacity는 비워 놓은 채 "Add mount point"를 클릭한다. 그러면 4GB를 제외한 나머지 용량이 루트 파티션 "/"에 할당된다.

![bimage9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image9.png)

- 최종적으로 다음과 같이 설정되었으면 "Done"을 클릭해서 설정을 마친다. 또 "SUMMARY OF CHANGES"가 나오면 "Accept Changes"를 클릭한다.

![bimage10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image10.png)


- USER SETTINGS의 Root Password를 설정한다.
- root 비번은 실습의 편의를 위해 password로 입력하고 "Done"을 2회 클릭한다.

![bimage11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image11.png)

- USER SETTINGS의 User Creation을 클릭하고 centos라는 이름의 사용자를 생성한다. 암호도 기억하기 쉽게 centos로 입력하고 "Done"을 2회 클릭한다.

![bimage13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image13.png)

- 다시 "INSTALLATION SUMMARY"가 나오면 오른쪽 아래의 "Begin Installation"이 활성화된다. 클릭해서 설치를 진행한다.

![bimage12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image12.png)

- 본격적으로 잠시 설치가 진행될 것이다.

![bimage14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image14.png)

- 설치가 완료 되었으면 "Reboot"를 클릭해서 재부팅한다.

- 컴퓨터가 다시 켜지면 일부 설정을 추가로 해줘야 한다.
	- 부탁 화면이 나온다. 몇 초를 기다리거나 첫 번째 행이 선택된 상태에서 그냥 "Enter"를 누르면 부팅된다.
	
	- 잠시 후 텍스트 환경의 로그인 화면이 나온다. Server(B) 컴퓨터도 root 사용자로 접속해서 사용할 것이다. "localhost login"에 "root"를 입력하고 "Enter"를 누른다. 그리고 "Password"에 "password"를 입력하고 "Enter"를 누른다(암호를 입력하면 화면은 보이지 않으므로 그냥 입력하고 "Enter"를 누르면 된다). 로그인되면 프롬프트가 "[root@localhost ~]#으로 보일 것이다.
	
	![bimage15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image15.png)

	
- 필요한 패키지를 미리 설치해 놓는다.

```
dnf -y install bind-utils net-tools wget unzip bzip2
```

![bimage16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image16.png)


- Server(B)는 10.0.2.200으로 변경할 것이다.
- 터미널에서 관련 디렉토리로 이동한 후, 파일을 편집하자

```
clear  -> 화면을 깨끗하게 한다.
cd /etc/sysconfig/network-scripts/  -> 네트워크 설정 파일이 저장된 디렉토리로 이동
ls    -> ifcfg-xxxx 파일 확인(예 : ifcfg-enp0s3)
vi ifcfg-xxxx  -> 앞에서 확인한 파일 편집
```

![bimage17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image17.png)


- vi에서 내용을 편집하려면 먼저 "A"를 누른다. 그러면 왼쪽 아래에 "-- INSERT --"가 표시된다. 이제 부터는 메모장처럼 키보드의 모든 키를 이용해서 편하게 사용하면 된다(단, 숫자패드는 작동하지 않을 수 있으므로 숫자는 키보드 위쪽 키를 사용하자. 또 아직 "ESC"는 누르면 안된다.)
- 일단 다음과 같이 내용을 수정한다. 다음은 Server(B)에 고정IP를 할당하는 것이다.(대소문자를 정확히 구분하고 글자 사이에 띄어쓰기 없이 입력해야 한다.)

	- 수정 : BOOTPROTO=dhcp  -> BOOTPROTO=none
	- 추가 : IPADDR=10.0.2.200
	- 추가 : NETMASK=255.255.255.0
	- 추가 : GATEWAY=10.0.2.2
	- 추가 : DNS1=8.8.8.8


![bimage18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image18.png)

- 수정/입력을 마쳤으므로 "Esc" -> :wq -> "Enter"를 차례로 누르고 입력한 후 저장하고 종료한다. 그러면 #프롬프트가 다시 나온다.
- 터미널에서 다음 명령을 입력하여 설정한 내용을 적용시키고 컴퓨터를 재부팅한다.

```
nmcli connection down 장치 이름  ->네트워크 장치 중지(예 : enp0s3)
nmcli connection up 장치 이름  -> 네트워크 장치 시작
reboot  -> 컴퓨터 재부팅
```

![bimage19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image19.png)

- root/password로 로그인한다.
- ip addr 명령을 입력해 네트워크 정보를 확인하자. 설정한10.0.2.200으로 보이면 된다.

![bimage20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image20.png)


- ping -c 3e www.google.com 명령이 잘 응답하면 인터넷이 잘 동작하는 것이다.

![bimage21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image21.png)


- 보안이 설정된 SELinux 기능을 끄자
	- vi /etc/sysconfig/selinux 명령을 입력해 일단 SELinux 설정 파일을 연다.
	- vi 편집기가 열리면 "A"를 누른다. 그러면 제일 아래에 '-- INSERT --"가 표시될 것이다. 7행의 SELINUX=enforcing을 SELINUX=disabled로 수정한다.
	
	![bimage22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image22.png)
	
	- "Esc" -> :wq -> "Enter"를 차례로 누르고 입력한 후 저장하고 종료한다. 그러면 # 프롬프트가 다시 나온다.
	
- halt -p 명령을 입력해 시스템을 종료하자. Server (B)의 설정은 마무리 되었다.
	
- 설치된 가상머신의 오른쪽 더보기 메뉴를 클릭한 후 '스냅샷'을 선택합니다.
	
![bimage23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image23.png)

- 상단의 스냅셧 메뉴 중에서 '찍기'를 선택합니다.

![bimage24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image24.png)

	
- 스냅샷 이름과 설명을 입력한 후 클릭하면 스냅샷이 생성됩니다.

![bimage25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image25.png)

![bimage26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/server(B)/image26.png)


### 가상머신 : Client 설치

- 앞서 만들어 놓은 Client 가상머신에 CentOS 8을 설치한다. 조금 전에 설치한 Server와 설치 과정이 상당히 비슷하므로 여기서는 차이점 위주로 설명한다. Server 가상머신과의 큰 차이점은 Client 가상머신의 경우 고정 IP가 아닌 동적 IP를 주로 사용하고 디스크 파티션이 자동으로 진행된다는 것 정도다. 또한 Client 가상머신은 root가 아닌 centos 사용자로 접속해 사용할 것이다.

- 설정 -> 저장소 -> 컨트롤러 IDE 의 추가 버튼 클릭 -> 추가 -> 다운받은 CentOS-Stream-8을 선택 -> 선택 클릭
- 확인 버튼을 클릭
- 시작 버튼을 클릭하여 Client 가상머신을 시작한다.

	- CentOS 8 설치가 시작된다. 가상머신 안을 클릭해서 마우스 포커스를 가상머신으로 옮긴 후 첫 번째 줄의 Intstall CentOS Stream 8-stream을 선택한다.
	- 잠시 초기 설정이 진행된다,.
	- X 윈도가 나오고 언어 선택화면이 나온다. 왼쪽에서 아래로 스크롤하여 "한국어"를 선택한 후 오른쪽의 "한국어(대한민국)"를 선택하고 "계속 진행"을 클릭한다.

- "설치 요약"이 나온다.
	- "Keyboard"는 "한국어"로 되어 있고 "언어 지원"도 한국어(대한민국)"로 되어 있을 것이다. 그대로 두고 "시간 및 날짜"를 클릭한다.
	- 지역은 "아시아"로 도시는 "서울"로 선택하고 "완료"를 클릭한다.
	- 오른쪽의 "네트워크 및 호스트 이름"을 클릭한다. 오른쪽에 있는 "끔" 스위치를 "켬"으로 만들면 네트워크 정보가 보일 것이다. "완료"를 클릭한다.
	- "소프트웨어 선택"을 보면 "서버 - GUI 사용"이 선택되어 있을 것이다. 클릭해서 "워크스테이션"으로 선택하고 오른쪽의 "GNOME 응용 프로그램"을 선택한 후 "완료"를 클릭한다.
	
	![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image1.png)
	
	- "설치 목적지" 부분을 확인하면 "자동 파티션 설정 선택"으로 되어 있을 것이다. 변경해야 하므로 클릭한다.
	- "설치 목적지"에서는 장착한 80GB크기의 하드디스크가 그림으로 보인다. 하드디스크 그림을 천천히 2회 클릭하여 하드디스크가 파란색으로 선택되고 체크 모양의 아이콘이 보이는 상태를 확인한다. 그리고 아래쪽의 "자동 설정"이 선택된 것을 확인하고 "완료"를 클릭한다.
	
	![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image2.png)
	
	- "사용자 설정"에서 "root 비밀번호"를 클릭해서 리눅스 관리자인 root 암호를 지정하자.
	- root의 암호는 기억하기 쉽도록 password로 입력하자. 그리고 "완료"를 2회 클릭한다.
	- "사용자 생성"을 클릭한 후 centos라는 이름의 사용자를 생성하자. 암호도 기억하기 쉽게 centros로 입력하자. "완료"를 2회 클릭한다.
	- 이제는 한동안 본격적으로 설치가 진행될 것이다. 컴퓨터 성능에 따라 수 분 ~ 수십 분이 걸릴 수 있다. 
	- 설치가 완료되었으면 "재부팅"을 클릭해서 재부팅한다.
	
- 컴퓨터가 다시 켜지면 일부 설정을 추가로 해줘야 한다.
	- 부팅 화면이 나온다. 몇 초를 기다리거나 첫 번째 행이 선택된 상태에서 그냥 "Enter"를 누르면 부팅된다.
	- "초기 설정"에서 "Licence Information"을 클릭하여 아래쪽 "약관에 동의합니다"를 체크하고 "완료"를 클릭한다. 그리고 오른쪽 "설정 완료"를 클릭해서 진행한다.
	- 다시 부팅되면 잠 시 후 X 윈도 로그인 화면이 나온다. "목록에 없습니까?"를 클릭해서 root 사용자로 로그인한다. 암호는 root 사용자의 암호인 "password"를 입력하고 "로그인"을 클릭한다.
	- 그놈(GNOME) 초기 설정 화면이 나오고 먼저 "환영합니다" 화면이 등장한다. 이미 한국어가 선택되어 있을 것이다. "다음"을 클릭한다.
	- "입력"이 나온다. 첫 번째에 있는 "한국어(Hangul)"를 선택하고 "다음"을 클릭한다.
	- "개인 정보"가 나오면 그대로 두고 "다음"을 클릭한다.
	- "온라인 계정"도 그대로 두고 "건너뛰기"를 클릭한다.
	- 마지막 창에서 "CentOS Linux 시작"을 클릭한다.
	- "시작하기(GNOME HELP)"창이 나온다. 오른쪽 위의 <X>를 클릭해서 닫는다.
	
- CentOS 8은 백그라운드로 새로운 패키지를 자동 업데이트하도록 설정되어 있다. 이 자동 업데이트 기능을 꺼 놓자.
	- 왼쪽 상단 "현재 활동"을 클릭하고 "터미널"을 클릭해서 터미널을 열자
	- 터미널에서 다음 명령어를 차례로 입력하여 자동으로 업데이트되는 기능을 끄자. 앞의 두 명령 결과로 아무 메시지도 나오지 않으면 되고, 세 번째 명령 결과로 "Removed /etc/systemd~~" 메시지가 나오면 된다.
	
	```
	gsettings set org.gnome.software download-updates false
	systemctl disable dnf-makecache.service
	systemctl disable dnf-makecache.timer
	```

- Client 가상머신은 root 사용자가 접속하지 못하도록 하자
	- gedit /etc/pam.d/gdm-password 명령을 입력해 편집기를 열자.
	- 그리고 5행쯤의 빈 줄에 다음을 추가로 써 준다. 글자가 틀리지 않도록 주의하자. 입력이 끝나면 저장하고 편집기를 닫는다.
	
	```
	auth required pam_succeed_if.so	user != root quiet
	```
	
	![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image3.png)
	
	- reboot 명령으로 재부팅한다.
	
- root 사용자로 접속이 안 된다는 것을 확인하자
	- 로그인 창에서 "목록에 없습니까?"를 클릭하고 root 사용자로 접속해보자. 암호를 입력하고 "로그인"을 클릭하면 인증에 실패할 것이다.
	
	![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image4.png)
	
	- "취소"를 클릭하고 centos 사용자를 클릭한 후 암호 "centos"를 입력해서 로그인한다.
	- 그놈(GNOME)의 초기 설정 화면이 나오고 먼저 "환영합니다" 화면이 등장한다. 이미 한국어가 선택되어 있을 것이다. "다음"을 클릭한다.
	- "입력"이 나온다. 첫 번째에 있는 "한국어(Hangul)"를 선택하고 "다음"을 클릭한다.
	- "개인 정보"가 나오면 그대로 두고 "다음"을 클릭한다.
	- "온라인 계정"도 그대로 두고 "건너뛰기"를 클릭한다. 
	- 마지막 창에서 "CentOS Linux 시작"을 클릭한다. 
	- "시작하기(GNOME Help)"창이 나온다. 오른쪽 위의 "X"를 클릭해서 닫는다.
	
- centos 사용자 환경으로 사용하기 위해 몇 가지 더 설정할 것이 남았다. 바탕화면에서 마우스 오른쪽 버튼을 클릭한 후 "설정"을 선택한다. 
	- "개인 정보"를 클릭하고 "화면 잠금"을 클릭해서 "자동 화면 잠금"과 "알림 표시"를 "끔"으로 변경하자. 그리고 "화면 잠금" 창을 닫는다.
	- 이번에는 "전원"을 클릭하고 "빈 화면"을 "안 함"으로 변경하자
	- "지역 및 언어"를 선택하고 "입력 소스"의 "한국어"를 선택한 후 "-"를 눌러서 삭제한다. 즉, "한국어(Hangul)" 하나만 남겨둬야 한다. 설정을 마쳤으면 오른쪽 위의 X를 클릭해서 "설정" 창을 닫는다.
	
- Client 가상 머신의 배경 화면을 바꿔서 Server 가상 머신과 구분되도록 하자
	- 바탕 화면에서 마우스 오른쪽 버튼을 클릭한 후 "배경 바꾸기"를 선택한다.
	- "배경"을 클릭한다.
	
	![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image5.png)
	
- 다른 배경 이미지나 사진을 선택한다.
> 사진을 사용하려면 웹에서 적당한 이미지를 다운받아 "사진" 폴더에 저장해놓는다. 일례로 https://www.gnome-look.org/ 사이트의 Wallpaper를 사용하면 된다.


- 소프트웨어 업데이트 기능도 끄자
	- "현재 활동"을 클릭하고 제일 아래 있는 프로그램 표시 아이콘을 클릭해서 "모두"를 선택한다. 그리고 "소프트웨어"를 클릭해서 실행한다.
	
	![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image8.png)
	
	- 상단의 더보기 메뉴를 클릭한 후 "업데이트 기본 설정"을 선택하고 모두 "끔"으로 만든 후에 창을 닫는다.
	
	![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image6.png)
	
	![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image7.png)
	
- Client 가상머신에 별도의 로그인 절차 없이 자동으로  centos 사용자가 접속되도록 하자.

> 서버용으로 사용되는 리눅스에 자동으로 로그인하는 것은 보안에 상당히 좋지 않지만 Client 가상머신은 개인용 PC라는 전제하에서 설정해본다.

	- "현재활동" -> "터미널"을 선택한다.
	- su - 명령을 사용해서 root 권한으로 접속하자(암호는 password를 입력한다). 다음 명령을 사용해서 파일을 편집한다.
	
	```
	vi /etc/gdm/customer.conf
	```
	
	![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image9.png)
	
	- "A"를 누른 후 "demon" 아래에 다음 2줄을 추가하자. 그리고 "Esc"를 누르고 ":wq"를 입력한 후 "Enter"를 누르면 저장 및 종료된다.
	
	```
	AutomaticLoginEnable=True
	AutomaticLogin=centos  -> 자동 로그인할 사용자 계정
	```
	
	![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image10.png)
	
	- reboot 명령을 입력해보자. 재부팅된 후 별도의 입력 없이 centos 사용자로 자동 접속될 것이다.
	- 오른쪽 위의 전원 버튼을 눌러 가상머신을 종료한다.
	
	
	
- 설치된 가상머신의 오른쪽 더보기 메뉴를 클릭한 후 '스냅샷'을 선택합니다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image11.png)

- 상단의 스냅셧 메뉴 중에서 '찍기'를 선택합니다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image12.png)

	
- 스냅샷 이름과 설명을 입력한 후 클릭하면 스냅샷이 생성됩니다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/1~2%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B0%9C%EC%9A%94%2C%20%EC%8B%A4%EC%8A%B5%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%B6%95/images/Client/image13.png)

### 가상머신 : WinClient 설치

- windows10 ISO 파일을 생성하는 도구를 [다운로드](https://www.microsoft.com/ko-kr/software-download/windows10) 받는다.
- iso 파일이 생성되면 가상머신으로 windows10을 설치한다.


### 실습용 가상머신 파일 다운로드

- [다운로드](https://drive.google.com/drive/folders/1jLtrrE4Lmq77pJLYgrvCEe5UiDm9AcCA?usp=sharing)
