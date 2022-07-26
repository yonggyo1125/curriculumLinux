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

### 메일 클라이언트 - 에볼루션

### 메신저 - 피진

### FTP 클라이언트 - gftp

