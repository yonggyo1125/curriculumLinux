# 그놈 데스크톱 환경 설정

- CentOS에서 기본으로 제공하는 X 윈도의 오픈 데스크톱 환경인 그놈GNOME을 사용자 취향에 맞게설정해보자. 그놈은 Microsoft Windows의 GUI(Graphical User Interface) 환경과 비슷하게 느낄 수 있도록 구성되어 있으므로 처음 리눅스를 사용하는 사람이 갖는 거부감을 많이 줄여준다. 

- 실습은 서버용이 아닌 PC용으로 설치된 CentOS라고 가정할 것이므로, 그놈이 설치된 Client 가상머신을 주로 이용할 것이다. 그놈은 다른 많은 리눅스도 기본으로 사용하는 보편적인 데스크톱 환경이다.

## 실습1
X 윈도의 바탕 화면과 테마를 설정해본다.

### step 0

- Client를 처음 설치 상태로 초기화하자
- Client 가상머신의 RAM을 2GB (=2048 MB)로 올리고 부팅하자
- Client 가상머신은 자동으로 centos 사용자로 로그인된다. 오른쪽 위의 전원 버튼을 클릭하면 확인할수 있다.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image1.png)

- 바탕 화면 왼쪽 위의 [현재 활동] →[터미널]을 선택해서 터미널을 연다.

### step1

바탕 화면을 바꿔보자.

- 바탕 화면에서 마우스 오른쪽 버튼을 클릭하고 [배경 바꾸기]를 선택한다.
- 왼쪽 [배경(B)]를 클릭하면 몇 개의 배경 이미지가 나온다. 그중 원하는 것을 클릭하고 \<선택\>을클릭한다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image2.png)

- 마음에 드는 바탕 화면이 없다면 그놈 웹 사이트에서 여러 가지 이미지를 구할 수 있다. 
- 왼쪽 위 [현재 활동]을 클릭해서 [Firefox 웹 브라우저]를 실행한 후 http://gnome-look.org/ (또는 http://ftp.gnome.org/pub/gnome/teams/art.gnome.org/archive/ ) 에 접속해 마음에 드는 이미지를 선택한다. 
- 왼쪽에서 [Wallpapers Gnome]을 선택하면 많은 배경화면이 나온다. 그중 하나를 선택하자.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image3.png)

- 그림이 나오면 마우스 오른쪽 버튼으로 클릭하고 [바탕 화면 배경 설정]을 선택하면 바로 배경으로 지정된다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image4.png)

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image5.png)

### step2

모양새(=테마)도 변경해보자

- 왼쪽 위 [현재 활동] -> [프로그램 표시] -> [유틸리티] -> [터미널]을 클릭한다.
- <b>su -c 'dnf -y install gnome-tweak-tool'</b> 명령을 입력해 우선 관련 패키지를 설치하자. 암호는 root의 비밀번호인 password를 입력한다.

> 패키지 설치는 root 권한으로 해야 한다. <b>su -c '명령어'</b> 명령은 root 권한으로 명령어를 수행하도록 한다.

- <b>gnome-tweaks</b> 명령을 입력해 [기능 개선] 창을 연다. 왼쪽에서 [모양새]를 선택하고 오른쪽 테마들을 적당한 것으로 바꿔보자. 그리고 오른쪽 위의 \<X\>를 눌러 종료한다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image6.png)

- 왼쪽 위의 [현재 활동] → [프로그램 표시]를 클릭하면 배경색, 타이틀 바, 아이콘 등이 아까와 달라졌음을 확인할 수 있다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image7.png)


### step3

처음 부팅 시의 GRUB 화면은 검은 화면에 글자만 나온다. 이번에는 GRUB에 그림이 나오도록 변경해보자.

- 우선 http://gnome-look.org/ (또는 http://ftp.gnome.org/pub/gnome/teams/art.gnome.org/archive/ )에서 적당한 Wallpaper를 선택하고 그림에서 마우스 오른쪽 버튼을 클릭한 후 [이미지를 다른 이름으로 저장] 을 선택해 파일을 저장해놓자. 필자는 wall.png로 저장해놓았다.

> 꼭 http://gnome-look.org 에서 다운로드 받을 필요는 없으며 어떤 PNG 그림 파일이든 관계없다.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image8.png)

- 저장한 그림 파일을 /boot/grub2/ 폴더로 옮겨놓는다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image9.png)

- <b>su -c 'gedit /etc/default/grub'</b> 명령으로 grub 파일 맨 아래에 다음 내용을 추가한 후, 중간에 위치한 GRUB_TERMINAL_OUTPUT 행 앞에 '#'을 붙여 주석으로 처리한다. 설정이 끝나면 저장하고 닫는다.

```
GRUB_BACKGROUND="/boot/grub2/wall.png"
```

> gedit을 실행할 때 '\*\* (gedit : 2738):dconf-WARNING ~~' 경고가 나와도 무시하자. 언어 설정과 관련된 약간의 버그 때문인데 실행과는 상관 없다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image10.png)

- <b>su -c 'grub2-mkconfig -o /boot/grub2/grub.cfg'</b> 명령을 입력해 변경된 내용을 새로 GRUB에 적용시킨다.
- <b>reboot</b> 명령어를 입력해 재부팅한다.
- 이제 초기 GRUB 화면에 설정한 배경 이미지가 출력될 것이다.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image11.png)

* * * 
# X 윈도 응용 프로그램

## 파일 브라우저 - 노틸러스

- 노틸러스는 그놈(GNOME) 데스크톱 환경에서 제공되는 파일 관리자로, Windows의 '파일 탐색기'와 비슷한 역할을 한다고 보면 쉽게 이해할 수 있다. 
- Windows에서 사용하는 것과 거의 비슷하므로 사용이 직관적이고 간편하다. 또 이 노틸러스를 이용해서 다양한 작업도 할 수 있다. 

## 실습2

노틸러스를 사용해보자. 

### step0 

- Client를 처음 설치 상태로 초기화하자
- PC의 메모리가 충분하다면 가상머신의 RAM을 2GB (=2048 MB)로 올리고 부팅하자. 
- centos 사용자로 자동 로그인된다.

### step1

노틸러스의 기본적인 사용법을 익혀보자.

- 왼쪽 위의 [현재 활동] → [파일]을 선택하거나 터미널에서 <b>nautilus</b> 명령을 입력한다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image12.png)

- 노틸러스가 실행되고, 기본으로 현재 사용자의 홈 디렉터리가 나타난다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image13.png)

- 오른쪽 빈 공간에서 마우스 오른쪽 버튼을 클릭하고 [새 폴더]를 선택하면 새로운 폴더를 만들 수 있다.

>  폴더'와 '디렉터리'는 엄격하게는 구분할 수 있지만 그냥 같은 용어라고 생각해도 무방하다. 대개 폴더는 GUI(GraphicUser Interface) 환경에서 디렉터리는 TUI (Text User Interface) 환경에서 부르는 용어다.

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image14.png)

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image15.png)

- 새로 만든 폴더를 더블클릭해서 안으로 들어가보자. 왼쪽 위에는 현재 폴더의 위치가 나타난다. 현재 사용자인 centos 사용자의 홈 폴더는 /home/centos/ 이므로, 현재 폴더는 /home/centos/LinuxFolder/ 라는 의미다.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image16.png)

- 왼쪽의 [다른 위치]를 클릭하자. 그러면 오른쪽에 컴퓨터 (루트폴더인 '/' 폴더)가 보일 것이다. 이것을 클릭해서 들어가보자. 여기서 폴더 아이콘에 'X'가 붙은 폴더는 현재 사용자인 CentOS의 권한으로 접근할 수 없음을 나타낸다.

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image17.png)

- 그 외에 Windows에서 사용하던 복사(Ctrl + C), 잘라내기 (CTRL + X), 붙여넣기(CTRL + V) 단축키도 사용할 수 있다.

- 파일 실행도 바로 가능하다. 왼쪽 [사진] 폴더로 이동한 후 사진 파일이 있으면 더블클릭해서 이미지 보기 프로그램과 연결할 수 있다.

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image18.png)

- 바탕 화면에서 마우스 오른쪽 버튼을 클릭해 [설정] 아이콘을 클릭하고, 왼쪽 제일 아래 [자세히 보기]를 선택한 후 다시 왼쪽 [기본 프로그램]을 클릭한다. 더블클릭하면 자동으로 연결할 프로그램을 바꿀 수 있다. 필요한 경우 변경하면 된다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image19.png)

### step2

이번에는 CD/DVD 또는 ISO 파일을 레코딩해보자.

- [현재 활동] → [프로그램 표시] → [브라세로]를 클릭한다.

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image20.png)

-  왼쪽에서 [데이터 프로젝트]를 클릭하자.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image21.png)


- 왼쪽 위의 [현재 활동] → [파일]을 선택해서 노틸러스를 열고 적당한 파일을 브라세로 화면에 끌어다놓는다. 필요한 파일을 모두 끌어왔으면 \<굽기\>를 클릭한다.

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image22.png)

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image23.png)

- 별도의 빈 CD나 DVD를 넣지 않았다면 이미지 (iso) 파일로 저장될 것이다. 파일명을 적당히 변경하고 \<이미지 만들기\>를 클릭한다.

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image24.png)

- 이미지가 잘 만들어졌으면 \<닫기\> 버튼을 클릭하고 브라세로도 종료한다.

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image25.png)

### step3

ISO 파일을 마운트해서 사용해보자.

[현재 활동] -> [파일]을 선택한 후 노틸러스에서 내 폴더(/home/centos/)의 myphoto.iso 파일을 확인한다.

- myphoto.iso 파일을 마우스 오른쪽 버튼으로 클릭하고 [디스크 이미지 마운트(으)로 열기]를 선택한다 (암호를 물어보면 centos를 입력한다).

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image26.png)

- [파일]의 왼쪽 [다른 위치]를 클릭하면 마운트된 장치가 확인된다.

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image27.png)

- 마운트된 [데이터 디스크]를 클릭하면 myphoto.iso 내부의 파일들이 확인된다.

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image28.png)

- 마운트를 해제하려면 왼쪽 다른 위치를 다시 클락한 후 오른쪽 '마운트 해제' 아이콘을 누른다.

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image29.png)


## 인터넷 응용 프로그램

### 웹 브라우저 - Firefox

- CentOS에서 기본으로 제공하는 웹 브라우저이며 많은 기능과 안전성을 제공한다. 필요한 경우 최신 버전으로 업그레이드할 수도 있다.

- Firefox는 CentOS에서도 제공하지만 최신 버전은 http://www.mozilla.or.kr/ 에서 직접 다운로드할 수 있다. 실습을 통해 직접 업그레이드해보자. 

## 실습3 
- Firefox를 직접 다운로드해서 최신 버전으로 업그레이드하자. 또 현재 영문판 Firefox를 한글판 Firefox로 변경하자.

### step0

Client를 처음 설치 상태로 초기화하자.

- Client 가상머신의 RAM을 2GB (=2048 MB)로 올리고 부팅하자.
- Client 가상머신은 centos 사용자로 자동 로그인된다.

### step 1

기존에 설치된 Firefox 버전을 확인해보자.

- [현재 활동] → [Firefox]를 선택해서 Firefox를 실행한 후 오른쪽 끝 '더보기 메뉴' 아이콘을 클릭하 [도움말] → [firefox 정보]를 선택해 버전을 확인한다.

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image30.png)

- 터미널에서 <b>rpm -gi firefox</b> 명령을 입력해 버전을 확인할 수도 있다. 버전은 91.10.0 이고 이 프로그램의 URL도 보여준다.

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image31.png)

- 한국어용 최신 버전을 다운로드하기 위해 https://www.mozilla.org/ko/firefox/all/ 에 접속한 후 아래로 스크롤해서 한국어 버전 64bit Linux용을 클릭하고 다운로드하자. 현재 시점의 최신 버전이 다운로드된다. 잠시 기다리면 다운로드가 시작되는데 \<파일 저장\>을 선택해서 저장해놓는다.

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image32.png)

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image33.png)

### step2

- 다운로드가 완료되면 열린 웹 브라우저를 닫는다. 그리고 다운로드한 Firefox 새 버전을 설치한다.

- 원칙적으로는 기존의 Firefox를 <b>dnf remove firefox</b> 명령으로 삭제해야 하지만, 이런 경우 메뉴의 아이콘 등이 사라지고 다시 등록해야 하는 번거로움이 있으므로 그냥 최신 파일로 덮어씌우는 방식을 사용한다.

- 다운로드한 파일의 압축을 풀고 새로운 버전의 Firefox를 사용하자. 다음 명령을 차례로 실행하면 된다.

```
cd ~/다운로드/   
	-> 현재 사용자의 '다운로드' 디렉토리로 이동(/home/centos/다운로드/ 디렉토리)
tar xfj fire[Tab]    -> 압축 풀기
su           -> root 사용자 권한 얻기
mv firefox /usr/local/
chown -R root.root /usr/local/firefox/
	-> Firefox 관련 파일을 모두 root 사용자 소유로 변경
cd /usr/local/bin/
ln -s /usr/local/firefox/firefox .
	-> 현재 디렉토리(/usr/local/bin/)에 firefox 링크를 새로 생성(제일 뒤에 . 이 있다)
```

![image34](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image34.png)


- [현재 활동] -> [Firefox]를 실행한다.
- [Firefox를 기본 브라우저로 설정] 을 클릭한다.

![image35](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image35.png)

- 오른쪽 끝 Firefox 메뉴의 [도움말] → [Firefox 정보]를 선택해 비전을 확인하면 한글판 103.0으로 바뀐 것을 확인할 수 있다.

![image36](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image36.png)

### 메일 클라이언트 - 에볼루션

- 에볼루션(Evolution)은 MS Outlook과 비슷한 기능을 하는 이메일 클라이언트로, 처음 실행할 때 메일서버와 계정을 입력해야 한다. evolution 패키지를 설치한 후 [현재 활동] → [에볼루션]을 선택하거나 터미널에서 <b>evolution</b> 명령을 실행하면 된다. 

![image37](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image37.png)

### 메신저 - 피진

- 피진은 Bonjour, Google Talk, ICQ 등의 메신저 서비스 프로그램으로 사용할 수 있다. [현재 활동] -> [프로그램 표시] -> [Pidgin] 을 선택하거나 터미널에서 <b>pidgin</b> 명령을 실행하면 열 수 있다.

![image38](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image38.png)

### FTP 클라이언트 - gftp

- CentOS 8에서는 gftp를 제공하지 않으므로, Fedora Linux 29의 사이트( https://archives. fedoraproject.org/pub/archive/fedora/linux/releases/29/Everything/x86_64/os/Packages/g/gftp-2.0.19-19.fc29.x86_64.rpm )에서 다운로드한 후 <b>su -c 'dnf -y install gftp\*.rpm'</b> 명령으로 설치한다.

- 설치 후에는 [현재 활동] -> [프로그램 표시] -> [gFTP]를 클릭하거나 <b>gftp</b>명령을 실행하면 열 수 있다.

![image39](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image39.png)

![image40](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image40.png)

![image41](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image41.png)

## 사운드 설정

### 사운드 설정

- CentOS 8은 설치될 때 대부분의 사운드 카드를 인식해서 자동으로 설치한다.

- 지금 사용하는 Client 가상머신에는 사운드 카드가 설치되어 있다. X 윈도 화면 오른쪽 위의 [설정] 아이콘을 클릭하거나 
- <b>gnome-control-center</b> 명령을 실행한 후, [설정]창이 열리면 왼쪽 아래에 있는 [소리] 아이콘을 클릭한다. [소리] 창에서 기본 사운드 설정을 할 수 있다. 
- 출력 음량을 어느 정도 올리고 [스피커 시험]을 클릭해서 테스트할 수도 있다.

![image42](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image42.png)

### 음량 조정

- 바탕 화면 오른쪽 위에 있는 [볼륨] 아이콘을 클릭하면 된다. 아래의 [소리 설정]을 클릭하면 다음처럼 사운드 설정 창이 나온다.

![image43](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image43.png)


## 멀티미디어 응용 프로그램

### 음악 재생과 인터넷 라디오 재생

- [현재 활동] → [리듬박스]를 클릭하거나 <b>rhythmbox</b> 명령을 실행하면 열 수 있다. 왼쪽의 [라디오]를 클릭하면 재생 가능한 인터넷 라디오 방송국이 나온다.

![image44](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image44.png)

### DVD 재생 및 동영상 플레이어

- [현재 활동] → 프로그램 표시 → [모두] → [동영상]을 선택한다. 또는 <b>totem</b> 명령을 실행해도 된다. 
- 위쪽 [채널]을 클릭하고 "The Guardian Videos"를 클릭하면 인터넷상에서 제공되는 동영상을 볼 수 있다.

- 동영상을 보려면 코덱(Codec)을 설치해야 하는데 일반적인 과정은 좀 복잡하므로 다음 URL에서 다운받아 설치한다.

- [http://download.hanbit.co.kr/centos/8/ffmpeg.tar.bz2](http://download.hanbit.co.kr/centos/8/ffmpeg.tar.bz2) 

- 코덱 설치 방법
	- <b>su</b> 명령어로 root 권한을 얻는다. 
	- <b>tar xfj ffmpeg.tar.bz2</b> 명령으로 압축을 푼다.
	- ffmpeg 폴더로 이동해서 <b>dnf -y install \*.rpm</b> 명령으로 관련 rpm을 설치한다.
	- 동영상 플레이어를 종료하고 다시 실행한다.
	
![image45](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image45.png)

## 문서 편집기/뷰어

### gedit
- 일반적인 텍스트 편집기로 Windows의 메모장 정도라고 보면 된다. 
- [현재 활동] → [프로그램 표시] → [텍스트 편집기]를 선택하거나 gedit 명령을 실행한다.


### 문서보기

- PDF, XPS, TIFF 등의 다중 문서를 볼 수 있는 간편한 뷰어 프로그램이다. 
- [현재 활동] → [프로그램 표시] → [유틸리티] → [문서 보기]를 선택하거나 <b>evince</b> 명령을 실행한다.

![image46](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image46.png)

## Foxit PDF Reader

무료이며 PDF 파일 전용 뷰어인 Foxit Reader를 사용해보자.

### 실습4

Foxit Reader를 설치하고 사용하자.

#### step 0

Client를 처음 설치 상태로 초기화하자

- Client 가상머신의 RAM을 2GB (=2048 MB)로 올리고 부팅하자.
- Client 가상머신은 centos 사용자로 자동 로그인된다.

#### step 1

설치 파일을 다운로드하자.

- 웹 브라우저로 https://www.foxitsoftware.com/downloads/ 에 접속한 후 Foxit Reader(FoxitReader.enu.setup.2.4.4.0911.x64.run.tar.gz) 파일을 다운로드하자. 그리고 \<파일 저장\>을 선택해서 파일을 저장해놓자. 다운로드가 완료되면 웹 브라우저를 닫는다.

![image48](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image48.png)

- 다운로드 폴더로 이동한 후 터미널에서 다음 명령을 실행하고 설치하자.

```
cd ~/다운로드/   -> 현재 사용자의 '다운로드' 디렉토리로 이동
ls -l Foxit*
tar xfz Foxit* -> 압축 해제
ls
./Foxit*.run  -> 설치 진행(기본값으로 진행)
```

![image49](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image49.png)

- 나머지는 계속 \<Next\> 및 \<Finish\>를 클릭해서 진행한다.

#### step 2

설치가 완료된 Foxit Reader를 실행해보자.

- [현재 활동] → [프로그램 표시] → [Foxit Reader]를 선택한다. 
- 메뉴의 [도움말] → [언어] → [영어]를 선택해서 영문 환경으로 만든다.

> Foxit Reader는 한글 환경에서 약간의 충돌이 발생할 수 있다.

- 메뉴의 [파일] → [열기]를 선택해서 pdf 파일을 연다. 사용법은 Windows용 Foxit Reader와 동일하다.

![image50](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image50.png)

## CD/DVD 레코딩-브라세로

- CentOS 8은 CD/DVD를 레코딩하는 툴로 브라세로(Briasero)라는 프로그램을 제공한다. \<실습 2\>에서 사용한 것과 마찬가지로 일반적인 CD/DVD 레코딩 프로그램과 사용법이 비슷해 쉽게 사용할 수 있다.

- 바탕 화면 왼쪽 위의 [현재 활동] → [프로그램 표시] → [브라세로]를 선택하거나 <b>brasero</b> 명령을 실행하면 된다.

![image47](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image47.png)

## 그래픽 프로그램

- Windows의 경우 많은 그래픽 응용 프로그램이 존재한다. 예를 들면 포토샵(Photoshop)이나 페인트샵(Pantshop) 같은 그래픽 편집 프로그램과 각종 그래픽 뷰어 프로그램이 있다. 
- CentOS도 이와 유사한 기능을 하는 프로그램을 제공하며, 특히 GIMP(GNU Image Manipulation Program)는 포토샵과 비교해도 거의 대등한 기능과 역할을 수행하는 뛰어난 그래픽 편집 프로그램이다.

### 그래픽 편집 - GIMP

- Windows의 포토샵과 비슷한 그래픽 응용 프로그램이다. 
- 먼저 <b>su-c 'dnf -y install gimp'</b> 명령을 실행해 설치한다. 
- 설치 후 메뉴의 [현재 활동] → [프로그램 표시] → [GNU Image Manipulation Program]을 선택하거나 <b>gimp</b> 명령을 실행한다.

![image51](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image51.png)


### 그림 보기 -eog(Eye Of Gnome)

- Windows의 [사진] 앱 같이 여러 가지 그림 파일을 보여주는 그래픽 뷰어 프로그램이다. 
- [현재 활동] → [프로그램 표시] → [유틸리티] → [이미지 보기]를 선택하거나 eog 명령을 사용한다.

![image52](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image52.png)

### 스크린샷

- 화면을 캡쳐할 때 사용한다. [현재 활동] → [프로그램 표시] → [유틸리티] → [스크린샷]을 실행하면 된다.

![image53](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image53.png)

### LibreOffice(리브레오피스)

- PC의 활용도가 가장 높은 분야 중 하나는 바로 문서 작성 및 표 계산일 것이다. 이번에는 Microsoft Office와 견주어도 별로 뒤떨어지지 않으며 오픈 소스로 제공되는 LibreOffice를 사용해보자. 이 프로그램의 특징은 MS Office와 호환성이 아주 우수하다는 점이다. 따라서 MS Office 때문에 Windows에서 리눅스로 옮기지 못하는 사용자에게는 어느 정도 보상이 될 것이다. 또 사용법도 크게 르지 않으므로 짧은 시간에 익숙하게 사용할 수 있다.

- MS Office에 워드(Word), 엑셀(Excel), 파워포인트(Powerpoint), 액세스(Access)가 있듯이 LibreOffice에도 워드에 대응하는 라이터(Writer), 엑셀에 대응하는 캘크(Calc), 파워포인트에 대응하는 임프레스(Impress), 액세스에 대응하는 베이스(Base)가 있다. 그 외에 그리기 툴인 드로우(Draw), 수식 작성 툴인 매쓰(Math)도 제공한다.

> LibreOffice 제품<br><br>LibreOffice는 원래 OpenOffice라는 제품에서 갈라져 나온 제품이다. OpenOffice는 오랫동안 오픈 소스오피스 제품으로 사용되어 왔으나, OpenOffice를 후원하는 오라클(Oracle)사의 정책에 반발해서 2010년11월, 많은 개발자가 OpenOffice에서 독립해 LibreOffice를 개발하게 되었다. LibreOffice의 Libre'는 라틴어로 자유(Free)를 의미한다. 즉 '자유롭게 사용할 수 있는 오피스'라는 의미를 담은 이름이다. LibreOffice는 Windows용, Mac용, Linux용 모두를 무료로 배포하며 한국어 사이트는 http://ko.libreoffice.org/ 다.

### 실습5
 
- 리브레오피스 최신 버전을 설치하자.


#### step0

Client 가상머신에서 진행한다.

#### step1

https://ko.libreoffice.org/download/libreoffice-fresh/ 주소에서 Linux x64 (rpm)용 [기본 설치 프로그램]과 [한국어 언어팩]을 내려받자.

![image54](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image54.png)

#### step2

다운로드 받은 파일을 설치하자.

다운로드 받은 파일은 설치 rpm 파일인 LibreOffice_7.3.5_Linux_x86-64_rpm.tar.gz(252MB)와 한글팩인 LibreOffice_6.3.3_Linux_x86-64_rpm_langpack_ko.tar.gz(0.8MB)다. 두 파일의 압축을 tar xfz 명령으로 각각 푼다.

![image55](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image55.png)

- 압축이 풀린 ~/다운로드/LibreOffice_7.3.5.2_Linux_x86-64_rpm/RPMS/ 폴더로 이동해서 <b>su -c 'dnf -y install \*.rpm'</b> 명령으로 설치를 시작한다. 리브레오피스 관련 파일이 모두 설치될 것이다.

![image56](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image56.png)

- 설치가 완료ㅕ되면 다시 ~/다운로드/LibreOffice_7.3.5.2_Linux_x86-64_rpm_langpack_ko/RPMS/ 폴더로 이동해서 <b>su -c 'dnf -y install \*.rpm</b> 명령으로 설치를 시작한다. 한글 언어팩이 설치될 것이다.

![image57](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image57.png)

#### step 3

- 설치가 완료되었다.
- 터미널에서 <b>libreoffice7.3</b> 명령을 실행한다.

![image58](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image58.png)

### 워드프로세서 – Writer

- [현재 활동] → [프로그램 표시] → [LibreOffice Writer]를 선택하거나 <b>libreoffice7.3 --writer</b> 명령을 실행한다. MS Word의 파일 포맷인 doc와 docx를 지원하며, PDF 파일로 저장하는 기능도 있다. 

### 스프레드시트 - Calc

- [현재 활동] - [프로그램 표시] → [LibreOffice Calc]를 선택하거나 <b>libreoffice7.3 --calc</b> 명령을 실행한다. MS Excel의 파일 포맷인 xls xlsx 를 지원하며, PDF 파일로 저장하는 기능도 있다. 

### 프레젠테이션 툴 - Impress

-[현재 활동] → [프로그램 표시] → [LibreOffice Impress]를 선택하거나 <b>libreoffice7.3 --impress</b>명령을 실행한다. MS Powerpoint의 파일 포맷인 ppt와 pptx를 지원하며, PDF 파일로 저장하는기능도 있다.

## 소프트웨어 센터

- CentOS는 '소프트웨어 센터'라는 응용 프로그램 스토어를 제공한다. CentOS 소프트웨어 센터에서는 검색을 통해 원하는 소프트웨어를 클릭만으로 설치할 수 있다. 
- 소트프웨어 센터를 실행하려면 [현재 활동]→[소프트웨어]를 선택한다.

> 소프트웨어 센터에서 검색되는 패키지는 터미널에서 dnf 명령으로 설치해도 된다.

![image59](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image59.png)

- 필요한 소프트웨어를 클릭하거나 검색해서 설치하면 된다. 이미 설치된 소프트웨어는 오른쪽 위에 파란색으로 체크 표시가 되어 있다.
- 설치되지 않은 소프트웨어를 클릭해서 \<설치\>를 클릭하면 자동으로 다운로드 및 설치가 된다.
- 설치 완료 후 \<실행\>을 클릭하면 실행된다.

* * * 
# 리눅스에서 Windows 응용 프로그램 실행

- 리눅스에서 Windows 응용 프로그램을 사용하는 방법은 여러 가지로 연구되어 왔고, 지금도 계속 개발 및 발전 중이다. 그중 가장 확실한 방법은 가상머신 소프트웨어를 이용하는 것이다. 지금 우리가 Windows 환경에서 VirtualBox를 이용해 리눅스를 사용하듯이, 리눅스 환경에서도 가상머신 소프트웨어를 이용해서 Windows를 사용할 수 있다.

- 리눅스에서 가동이 가능한 가상머신 소프트웨어로는 VMware Workstation for Linux, Oracle VirtualBox for Linux, KVM/Qemu, Xen 등이 있으며, CentOS에서 자체적으로 제공하는 가상머신 소프트웨어도 있다. CentOS에서 설치 가능한 Oracle VirtualBox 가상머신 프로그램을 사용해보겠다.

> Windows 응용 프로그램 작동<br><br>리눅스에서 Windows 응용 프로그램을 작동시키는 방법에는 가상머신을 사용하지 않고 직접 Windows 응용 프로그램을 설치하도록 도와주는 프로그램도 있다. Wine, PlayOnLinux, CrossOver 등이 대표적인 패키지며, 필요한 경우 자세한 사용법은 독자가 직접 인터넷을 검색해보자. 설정이 좀 까다롭고 생각만큼 Windows 응용 프로그램이 원활하게 작동하지 않을 수도 있다.

## 실습6

가상머신 프로그램을 이용해 CentOS 안에 Windows를 설치해보자.

### step 0

- Client를 처음 설치 상태로 초기화하자.
- 부팅하면 자동으로 centos 사용자로 접속된다.

### step 1

- VirtualBox를 사용하는 데 필요한 추가 패키지를 미리 설치하자. 
- 터미널에서 다음 명령을 실행하면 약 100개 이상의 패키지가 설치될 것이다. 설치가 완료되면 exit 를 2회 입력해서 터미널을 닫는다.

```
su -   -> root로 접속
dnf -y install make perl patch kernel-devel elfutils-libelf-devel
```

### step 2

- 오라클사에서 제작한 VirtualBox라는 가상머신 프로그램을 설치해보자.

- 웹 브라우저로 https://www.virtualbox.org/wiki/Linux_Downloads 에 접속해서 [Oralce Linux8 / Red Hat Enterprise Linux 8 / CentOS 8]을 클릭한 후 다운로드하자.

![image60](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image60.png)

- 터미널을 열고 다음 명령으로 다운로드한 VirtualBox를 설치하자.

```
cd ~/다운로드/   -> 폴더 이동
ls Virtual*    -> 파일 확인
su -c 'dnf -y install Virtual*'  -> 설치
```

![image61](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image61.png)

- VirtualBox를 사용하기 위해 마지막 설정을 진행하자.

```
su -
usermod -a -G vboxusers centos   -> centos 사용자를 vboxusers 그룹에 추가
/usr/lib/virtualbox/vboxdrv.sh setup  -> 시간이 몇 분 걸림
/sbin/vboxconfig   -> 시간이 몇 분 걸림
exit
```

![image62](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image62.png)

### step 3

- 가상머신을 생성하자.
- [현재 활동] → [프로그램 표시] → [Oralce VM VirtualBox]를 실행하거나 <b>virtualbox</b> 명령을 입력한다. [Oracle VM VirtualBox 관리자]가 실행되면 \<새로 만들기\>를 클릭한다.

![image63](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/12~14%EC%9D%BC%EC%B0%A8(9h)%20-%20X%20%EC%9C%88%EB%8F%84%EC%9A%B0/images/image63.png)



