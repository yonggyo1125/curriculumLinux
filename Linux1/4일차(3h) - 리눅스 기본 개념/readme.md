# 리눅스 기본 개념

## 에디터 사용

- Windows의 메모장처럼 X 윈도에서 제공하는 편리한 에디터로 gedit이 있다. 터미널에서 간단히gedit 파일_이름 명령을 입력하면 해당 파일을 편집할 수 있다.

- 이보다 더 전통적으로 사용되어 온 에디터로는 vi 에디터가 있다. 그런데 유닉스/리눅스를 입문하는사용자가 vi 에디터를 처음 사용하면 좀 당황하게 된다. vi는 'visual'의 약어인데 그다지 비주얼적으로 느껴지지 않기 때문이다. 하지만 vi 에디터는 모든 유닉스/리눅스 시스템에 기본으로 포함되어있으며 반드시 사용할 수 있어야 하므로 잠깐 시간을 내서 사용해보자.

> 텍스트 모드인 Server(B)의 경우 gedit을 사용할 수 없으므로 vi 에디터를 꼭 사용할 수 있어야 한다.

### 실습1
- 리눅스에서 자주 사용되는 에디터를 사용하자.

- step0
	- Server를 사용하자.
	- 바탕 화면 왼쪽 위에서 [현재 활동] →[터미널]을 선택해 터미널을 연다.

- step1
	- 터미널에서 gedit 명령을 입력하자.
	-  에디터가 열리면 아무 글자나 입력한다(한/영 전환은 [Shift] + [Space]를 누른다).
	
	![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image2.png)
	
	- 오른쪽 위의 \<저장\>을 클릭해서 적당한 이름을 입력하고, 저장 위치를 [홈] 폴더로 선택한 후 \<저장\>을 클릭해 저장한다.
	
	![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image3.png)
	
	- 현재 사용자는 root 사용자인데, root 사용자의 홈 폴더인 "/root"에 저장한 것이다. 만약 centos 사용자라면 홈 폴더는 "/home/centos" 폴더가 된다.
	- gedit의 오른쪽 위 \<X\>를 클릭해서 gedit을 종료한다. 그리고 터미널에서 gedit "/root/test.txt" 명령을 입력하면 기존 파일이 열릴 것이다. 앞서 설명한 것처럼 gedit은 Windows의 메모장과 비슷한 용도로 사용하면 된다. 다시 gedit 을 종료한다.
	
- step2
	- 이번에는 vi 에디터를 사용해보자. 우선 터미널에서 vi 명령을 입력하면 다음과 같이 실행된다.
	
	![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image4.png)
	
	-  우선 vi 에디터를 종료해보자. [Esc]를 누른 후 'q'를 입력하고 [Enter]를 누르면 종료된다. 입력 시 화면 왼쪽 아래에 입력하는 글자가 보일 것이다. 이렇게 작동하는 것을 <b>'ex 모드' 또는 '라인 명령 모드'</b>라고 부른다.
	- 이번에는 vi 에디터로 새로운 파일을 만들어보자. <b>vi new.txt</b> 명령을 입력하면 빈 화면이 열리고 왼쪽 아래에 'new.txt[New File]'이라는 문구가 보인다 (new.txt 파일이 이미 존재하면 그 파일을 열어서 보여준다). 이 상태를 '명령 모드'라고 한다. 아직 글자를 입력할 수는 없으며, vi 에디터로 어떤 일을 하게 될지 명령을 기다린다.
	- 그 상태에서 "I" 또는 "A"를 누른다(이는 글자를 입력 Insert하거나 추가 Append하겠다는 명령을 내린 것이다). 그러면 왼쪽 아래에 '-- INSERT --'라고 표시되고 글자를 입력할 수 있다. 이 상태를 입력 모드'라고 한다. 적절히 글자를 입력해보자.
	
	![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image5.png)
	
	- 글자를 모두 입력했으면 저장하고 vi 에디터를 종료한다. 우선 글자를 입력하는 '입력 모드'에서 Esc를 누르면 <b>'명령 모드'</b>가 나온다. 화면에서는 왼쪽 아래에 '-- INSERT --' 라는 표시가 없어질 뿐 별다른 변화가 보이지 않는다.
	- 그리고 'wq' 를를 입력해 Enter를 누르면 저장하고 종료하게 된다.
	
	![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image6.png)
	
	- vi 에디터 사용법 개요도
	
	![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image1.png)
	
- step3
	- 이번에는 vi 에디터를 실행하고 글자를 입력한 후 입력한 내용을 test2.txt라는 파일에 저장하는 것을 연습한다.
	- 터미널에서 vi 명령을 입력한다. 그러면 상기 그림의 명령 모드로 진입한다
	- 글자를 입력하려면 입력 모드로 전환해야 하므로 "I" 또는 "A"를 누른다. 그러면 입력 모드로 들어간다. 왼쪽 아래에 '-- INSERT --'가 보일 것이다. 
	- 필요한 내용을 모두 입력한다.
	- 입력이 끝났으면 "Esc"를 눌러서 명령 모드로 빠져나온다. 왼쪽 아래에 '--  INSERT --'가 없어진다.
	- 내용을 저장하기 위해 ex 모드로 들어가는 ":" 을 누르고(왼쪽 아래에 콜론이 보인다), w test2.txt를 입력한 후 "Enter"를 누른다(왼쪽 아래에 'test2.txt [New] 2L, 25C written'이라는 문구가 보인다. 이는 2줄, 25문자가 저장되었다는 의미다). 이 상태는 ex 모드에서 [Enter]입력했으므로 다시 명령 모드로 돌아온 것이다.
	- 모든 작업을 마쳤으므로 vi 에디터를 종료해야 한다. 다시 ex 모드로 가기 위해 ':q!'를 입력한 후 "Enter"를 누른다. 'q!'의 의미는 기존에 변경된 내용은 무시하고 종료하라는 의미다. 바로 앞에서 저장한 후 변경된 것이 없으므로 이번에는 그냥 'q'라고만 입력해도 된다.
	
- step4
	- 이번에는 더 간단하게 텍스트를 입력한 다음 파일을 저장하고 바로 종료하는 작업을 수행해보자.
	- 터미널에서 vi 명령을 입력한다.
	- "I" 또는 "A"를 입력한 후 문서에 필요한 내용을 입력한다.
	- "Esc"를 누른 후 ':wq test3.txt'를 입력하고 [Enter]를 누르면 저장과 동시에 종료된다. 생각보다 간단하다.

- step5
	- 이번에는 기존 파일을 열어서 수정하고 저장해보자.
	- 터미널에서 vi test3.txt 명령을 입력하면 기존 파일이 열린다.
	- "I" 또는 "A"를 누른 후 문서를 수정하거나 추가한다.
	- "Esc"를 누른 후 ':wq test3.txt'를 입력하고 "Enter"를 누르면 저장과 동시에 종료된다.

- step6
	- 시존 파일을 열어서 수정했ㅎ지만 실수로 잘못 수정했다고 가정하고, 이번에는 저장하지 말고 그냥 종료해보자
	- 터미널에 "vi test3.txt" 명령을 입력한다.
	- "I" 또는 "A"를 누른 후 문서를 수정한다.
	- 그런데 실수로 잘못 수정했다. 수정한 내용을 저장하지 않고 VI 에디터를 닫으려면 "Esc"를 누른 후 ":q!"를 입력하고 "Enter"를 누르면 된다.
	
- step7
	- exit 명령을 입력해서 터미널을 닫는다.

> CentOS에 포함된 vi 에디터의 경우, 기존 vi 에디터의 기능을 향상시킨 vim (Vi IMproved) 에디터가 정확한 명칭이다. 하지만 vi 명령을 입력해도 자동으로 vim 에디터가 실행되므로 앞으로 그냥 vi 에디터라고 부르겠다

### 실습2
- vi 에디터가 비정상적으로 종료되었을 때 생성되는 파일을 확인하고 조치법을 알아

- step0
	- Server를 사용하자.
	- 바탕 화면 왼쪽 위의 [현재 활동] →[터미널]을 선택해서 터미널을 연다.

- step1
	- 터미널에서 vi test1.txt 명령을 입력해 파일을 열고 "I"또는 "A"를 누른 후 아무거나 약간 수정한다. 그리고 정상적으로 종료하지 말고 터미널 오른쪽 위에 있는 \<X\>를 클릭해 비정상적으로 종료한다. 경고 창이 나오면 \<터미널 닫기\>를 클릭한다.
	
	![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image7.png)
	
- step2
	- 터미널을 다시 연다.
	- 다시 vi test1.txt 명령을 입력하면 다음과 같은 창이 나온다.
	
	![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image8.png)
	
	- 이 창은 기존 test1.txt 파일의 수정 작업이 정상적으로 종료되지 않았기 때문에 나타난다.
	
>  임시 스왑 파일(swap file).test1.txt.swp가 존재하는 것은 앞에서 test1.txt 파일의 수정 작업이 정상적으로 종료되지 않았기 때문이다. 즉 vi test1.txt 명령을 입력하면 자동으로 test1.txt.swp가 생성되며, vi 에디터를 정상적으로 종료하면 이 파일은 자동으로 제거된다. 그러므로 이 파일이 남아 있다는 것은 기존 작업이 정상적으로 종료되지 않았다는 의미다. 참고로 파일 이름 앞에 '.'가 붙으면 숨김 파일을 뜻한다. 
	- "Space bar"를 몇 번 누른 후 "Esc"를 누르고 ":q!"를 입력해서 일단 vi 에디터를 닫는다.

- step3
	- 비정상 종료된 파일의 스왑 파일 이름은 '파일 이름.swp'다. 그러므로 test1.txt의 스왑 파일은 .test1.txt.swp다. Is -a 명령을 입력해 파일을 확인하고 rm -f .test1.txt.swp 명령을 입력해 해당 스왑 파일을 삭제하자.
	
	![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image9.png)
	
- step4
	- 이제는 test1.txt 파일을 정상적으로 편집할 수 있을 것이다. 가끔 만날 수 있는 상황이므로 잘 기억해두자.

- 이렇게 해서 vi 에디터의 기본 사용법을 확인해보았다. 그런데 vi 에디터는 지금 소개한 것보다 훨씬 많은 기능을 제공한다. 명령 모드에서 입력 모드로 전환하는 명령들을 요약하면 다음과 같다. 여러 개가 있지만 "I" 나 "A"정도만 주로 사용한다.

#### 명령 모드에서 입력 모드로 전환하기 위한 키 입력

|키|설명|키|설명|
|----|------|----|------|
|i|현재 커서의 위치부터 입력|I|현재 커서 줄의 맨 앞에서부터 입력(Shift + i)|
|a|현재 커서의 위치 다음 칸부터 입력|A|현재 커서 줄의 맨 마지막부터 입력(Shift + a)|
|o|현재 커서의 다음 줄에서 입력|O|현재 커서의 이전 줄에 입력(Shift + o)|
|s|현재 커서 위치의 한 글자를 지우고 입력|S|현재 커서의 한 줄을 지우고 입력(Shift + s)|


- 명령 모드에서 커서를 이동할 때는 4개의 화살표 키와 [Page Up] / [Page Down] 등을 이용하면 되지만, 그 외에도 일반 키보드로 그러한 효과를 낼 수 있다. 아주 오래 전에 만들어진 키보드에는 화살표 키나 [Page Up] / [Page Down]이 없는 것도 있어 만들어진 기능이다. 요즘 키보드는 대부분 화살표 키와 [Page Up], [Page Down], [Home], [End]가 있으므로 다음 표에서 아래 두 줄을 잘 기억하면 편리하게 사용할 수 있다.

|키|설명|키|설명|
|----|------|----|------|
|h|커서를 왼쪽으로 한 칸 이동과 같은 의미|j|커서를 아래로 한 칸 이동과 같은 의미|
|k|커서를 위로 한 칸 이동과 같은 의미|l|커서를 오른쪽으로 한 칸 이동과 같은 의미|
|Ctrl + F|다음 화면으로 이동[Page Down]과 같은 의미|Ctrl + B|이전 화면으로 이동 ([Page Up]과 같은 의미)|
|^|현재 행의 처음으로 이동([Home]과 같은 의미)|$|현재 행의 마지막으로 이동([End]와 같은 의미)|
|gg|제일 첫 행으로 이동|G|제일 끝 행으로 이동|
|숫자G|해당 숫자의 행으로 이동|:숫자[Enter]|해당 숫자의 행으로 이동|

- 명령 모드에서 삭제, 복사, 붙여넣기와 관련된 키는 다음과 같다.

|키|설명|키|설명|
|----|------|----|------|
|x|현재 커서가 위치한 글자 삭제([Del]과 같은 의미)|X|현재 커서가 위치한 앞 글자 삭제([Backspace]와 같은 의미)|
|dd|현재 커서의 행 삭제|숫자dd|현재 커서부터 숫자만큼 행 삭제|
|yy|현재 커서가 있는 행을 복사|숫자yy|현재 커서부터 숫자만큼 행을 복사|
|p|복사한 내용을 현재 행 이후에 붙여넣기|P|복사한 내용을 현재 행 이전에 붙여넣기|

- 명령 모드에서 문자열을 찾는 키는 다음과 같다.

|키|설명|키|설명|
|----|------|----|------|
|/문자열[Enter]|해당 문자열을 찾음(현재 커서 이후로)|n|찾은 문자 중에서 다음 문자로 이동|


- 그 외에도 ex 모드(라인 명령 모드)에서 가장 많이 사용하는 두 가지 정도만 더 소개한다. 문자열을 치환하려면 ':%s/기존문자열/새문자열' 형식으로 사용해야 한다. 예를 들어 'centos'라는 글자를 모두 linux'로 바꾸려면 '%s/centos/linux'라고 입력한다.

- 그리고 'set number'를 입력하면 vi 에디터 앞에 행 번호가 표시되므로 더 편리하게 사용할 수 있다.

## 도움말 사용법

- 리눅스에는 많은 명령어가 있으며 각 명령어의 옵션까지 합하면 수천 개가 넘는다. 이 명령어들을 모두 외울 수도 없거니와 외우려고 하는 것도 무모한 일이다.

- 그래서 필요한 것이 'man' 명령어다. 'man'은 manual의 약어로, 리눅스에 포함된 체계화된 도움말이다. 사용법은 <b>man \<명령어\></b>로 아주 간단하다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image10.png)


- 위쪽 행과 아래쪽 행으로 이동하려면 "위/아래 버튼" 또는 "K"/"J"를 사용하고, 페이지 단위로 이동하려면 [Page Up] [Page Down] 또는 [Space bar]/B 를 사용한다.

- 또한 도움말 중 특정 단어를 검색하고 싶으면 '/단어'를 실행해서 해당 단어들을 찾으면 된다. 이때 "N"을 누르면 다음 단어로 계속 넘어간다. 종료하려면 "Q"를 누른다.


#### man 명령어

- man 명령어는 섹션(Section)을 1~9까지 9개 페이지로 나눈다. <b>man Is</b> 명령 결과의 왼쪽 위에 나오는 'LS(1)'는 섹션 1번에 있는 도움말을 의미한다. 즉 man 명령은 <b>man [섹션 번호] 명령어</b> 명령으로 검색할 수 있다. Is 명령어의 경우, <b>man 1 Is</b> 명령으로 사용해도 된다. 하지만 특별히 섹션 번호를 지정하지 않으면 1번 섹션부터 9번 섹션까지 차례로 검색해 가장 먼저 만나는 도움말을 출력해준다.

- 참고로 섹션1은 명령어, 섹션 2~3은 프로그래밍, 섹션 4는 디바이스, 섹션 5는 파일 형식, 섹션 6은 게임, 섹션 7은 기타 주제, 섹션 8은 시스템 관리, 섹션 9는 커널 관련 설명을 포함한다.


## 마운트와 CD/DVD/USB 활용

- Windows에서는 마운트(mount)라는 개념이 별도로 사용되지 않기 때문에 리눅스를 처음 사용할 때 마운트가 다소 생소하게 느껴진다. 
- 리눅스에서 하드디스크의 파티션, CD/DVD, USB 메모리 등을 사용하려면 지정한 위치에 연결해야 한다. 이렇게 물리적인 장치를 특정한 위치(대개는 폴더)에 연결시키는 과정을 '<b>마운트</b>'라고 한다. 실제 사용은 어렵지 않으니 실습을 통해 익혀보자.


### 실습3

- CD/DVD를 마운트해보자.

- step0
	- <code>Server</code> Server를 처음 설치 상태로 초기화하자
	- root 사용자로 접속한다. 
	- 바탕 화면 왼쪽 위의 [현재 활동] →[터미널]을 선택해서 터미널을 연다.

- step1
	- <code>Server</code> Server의 기존 마운트 정보를 확인해보자.
	- mount 명령을 입력해 현재 마운트된 장치들을 확인해보자.
	
	![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image11.png)
	
	- 결과가 좀 복잡한데, 우선 "/dev/sda2"가 루트 파티션 ('/')에 마운트된 것만 확인한다.  Server를 설치할 때 '/'를 sda2에 76GB로 설정했기 때문에, "/dev/sda2"가에 계속 마운트되어 있던 것이다.
	
	
- step2
	- <code>Server</code>이제는 Server에 CD/DVD를 넣어보자.
	- 우선 기존에 CD/DVD가 마운트되어 있을 수도 있으니 <b>umount /dev/cdrom</b> 명령을 입력해서 마운트를 해제하자. 기존 마운트를 해제하는 명령으로 오류가 나도 상관 없다.
	
	![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image12.png)
	
	- 먼저 VirtualBox에 CD나 DVD를 넣어보자. 각 가상머신의 설정에서 저장소의 CD 모양 아이콘을 마우스 오른쪽 버튼으로 클릭한 후 CentOS8 ISO 파일을 선택한다. 설정이 끝나면 확인을 클릭한다.
	
	![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image13.png)
	
	
	- 잠시 기다리면 자동으로 화면 위쪽에 DVD가 연결되었다는 표시가 잠깐 나왔다가 사라진다.
	
	![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image14.png)
	
	- 터미널에서 <b>mount</b> 명령을 입력하면 제일 아래에 CD/DVD 장치인 "/dev/sr01"이 "/run/media/root/CentOS-Stream-8-x86_64" 디렉터리에 자동으로 마운트되어 있는 것을 확인할 수 있다.
	
	![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image15.png)
	
- step3
	- Server에 마운트된 CD/DVD를 사용해보자.
	- 자동으로 마운트된 CD/DVD의 디렉터리는 "/run/media/"다. 그 아래 디렉터리 이름은 현재 root 사용자의 이름과 CD/DVD의 Label 이름이며 디렉터리가 자동 생성된다. 즉 CentOS 8 DVD의 Label은 "CentOS-8-BaseOS-x86_64"이므로 마운트된 폴더는 "/run/media/root/CentOS-8-BaseOS-x86_64"가 되는 것이다.
	- DVD 패키지가 들어 있는 디렉터리로 이동해보자.
	
	```
	cd /run/media/root/Ce[Tab]    -> 데렉토리 이동
	pwd        -> 현재 디렉터리 위치를 보여줌
	ls
	```
	
	![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image16.png)
	
	- DVD 안의 파일을 확인해보자.
	
	```
	cd BaseOS/Pa[Tab]     -> BaseOS 아래 Packages 디렉토리로 이동
	ls 
	```
	
	![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image17.png)
	
	- BascOS/Packages 디렉터리 안에는 알파벳 순으로 정렬된 rpm 파일이 들어 있다.  CentOS를 설치할 때 이 파일들이 자동으로 설치된 것이다.
	- DVD를 더 이상 사용하지 않는다면 <b>umount /dev/cdrom</b> 명령을 입력해 마운트를 해제한다.
	
	![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image18.png)
	
	- 그런데 메시지를 보니 target is busy'라고 나오면서 마운트 해제에 실패한다. 지금 작업 중인 디렉터리가 DVD가 마운트된 "/run/media/root/"의 하위 디렉터리이기 때문이다. cd 등의 명령을 입력해 마운트 디렉터리가 아닌 디렉터리로 이동한 후 "umount /dev/cdrom" 명령으로 마운트를 해제해야 한다.
	
	![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image19.png)
	
	- 결국 DVD의 마운트를 해제할 때 현재 마운트된 디렉터리에서 명령을 실행하면 안 된다. 처음 리눅스를 사용할 때 자주 실수하는 부분이므로 잘 기억해두자.
	
	- mount 명령을 입력해서 확인하면 아까와 달리 "/dev/sr0"이 마운트되어 있지 않을 것이다. 
	- DVD의 마운트를 완전히 해제하려면 설정 -> 저장소 -> 컨트롤러 IDE에서 CD를 선택 -> 오른쪽 CD 모양의 아이콘을 선택 -> 가상드라이브에서 디스크 꺼내기 클릭 한다.
	
- step4
	- <code>Client</code> 이번에는 Client에서 USB 메모리를 사용해보자. CD/DVD와 크게 다르지 않다. USB 포트 장치는 Client에 장착시켰다.
		
	- Client를 부팅한다. 사용자로 자동 로그인된다.
	-  이제 진짜 컴퓨터에 USB 메모리를 꽂는다. 
	
	![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image20.png)
	
	- 잠시 기다리면 바탕 화면 상단에 USB가 연결된 것이 확인된다. [현재 활동] [파일]을 선택하면 Windows의 파일 탐색기와 비슷한 [파일 관리자] 프로그램이 열리고 USB 내부 내용을 확인할 수 있다. [파일 관리자] 왼쪽에 있는 USB 메모리의 레이블(label)을 클릭하면 된다.
	
	![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image21.png)
	
	![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image22.png)
	
	- 현재 USB 메모리는 Client에 인식되어 있는 상태다. 그래서 호스트 컴퓨터의 파일 탐색기에서는 USB 메모리 연결이 확인되지 않는다.

	- 터미널을 열고 직접 해당 디렉터리로 이동해서 다른 곳의 파일을 복사해보자.

	```
	cd /run/media/현재사용자이름/USB이름 	   -> 대소문자 구분
	pwd        -> 현재 디렉토리 출력
	ls            -> 파일 목록을 보여줌
	cp  /boot/con[Tab] .      -> 파일(/boot/confiog~~파일)을 현재 디렉토리(.)에 복사(제일 뒤에 . 있음).
	ls
	```
	
	![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image23.png)
	
	- CD/DVD와 달리 USB 메모리에는 당연히 읽기/쓰기가 가능하다.
	- mount 명령을 입력해서 USB 메모리가 마운트된 장치를 확인하자.
	
	![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image24.png)
	
	- 제일 아래를 보면 "/dev/sda1" 이라는 장치로 인식되어 있음을 확인할 수 있다.
	- USB 사용이 끝났다면, VirtualBox에서 USB 메모리 마운트를 해제하자. 
	
	![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image25.png)
	
	- 호스트 컴퓨터의 파일 탐색기에서 확인하면 USB 메모리가 확인되며, 아까 CentOS에서 복사했던 파일도 확인할 수 있
	- Client에서 오른쪽 위의 전원 아이콘을 클릭하고, 다시 전원 아이콘을 클릭한 후 <컴퓨터 끄기>를 선택해서 Client를 종료한다.
	
	
> Windows에서 USB 메모리의 파일 시스템은 FAT32 또는 NTFS를 주로 사용한다. 파일 탐색기에서 USB 메모리를 마우스 오른쪽 버튼으로 클릭한 후 [속성]을 선택해 내용을 살펴보면 확인할 수 있다.

> 어떤 파일 시스템을 사용해도 괜찮지만, CentOS는 기본적으로 FAT32 방식의 USB만 인식할 수 있다. 그러므로 이번 실습을 위해 USB 포맷 시 FAT32로 지정해서 포맷해야 한다 

- step5
	- <code>Server(B)</code> 이번에는 X 윈도가 없는 Server(B)의 텍스트 모드에서 CD/DVD와 USB 메모리를 사용해보자.
	- 이번 실습은 USB 메모리의 내용이 지워질 수도 있다. USB 메모리에 중요한 데이터가 들었다면 백업한 후 실습을 진행하자.
	- 왼쪽 Server(B)를 클릭해 Server(B) 실행을 준비한다(아직은 부팅하지 않는다).
	-  Server (B)에는 USB 장치를 추가하지 않았으므로 USB 장치를 추가하자.
	
	![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image27.png)
	
	- 이제 USB 장치 및 CD/DVD가 모두 장착되었으므로 Server (B)를 부팅하고 root 사용자로 접속한다.
	
	![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image26.png)
	
	- mount 명령을 입력해 기존에 마운트된 장치가 있는지 확인한다. CD/DVD 장치인 "/dev/sr0" 과 USB 장치인 "/dev/sdb1" 은 아직 마운트되어 있지 않다.
	- 먼저 CentOS 8 DVD ISO 파일을 넣어보자 그리고 USB 메모리도 연결한다.
	
	- mount 명령을 다시 입력해보자. CD/DVD를 넣거나 USB 메모리를 연결하기 전과 차이가 없을 것이다. 즉 텍스트 모드에서는 CD/DVD를 넣거나 USB 메모리를 연결했다고 자동으로 마운트되는 것이 아니다. 
	
	- CD/DVD 장치 이름은 전통적인 "/dev/cdrom"으로 제공된다. 하지만 USB 장치 이름은 종종 변할 수 있으므로 <b>Is /dev/sd\*</b> 명령을 입력해 장치 이름을 확인하자.
	
	![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image28.png)
	
	- /dev/cdrom 링크 파일이며 /dev/sr0 이 실제 CD/DVD 장치다. 하지만 대부분의 리눅스는 /dev/cdrom 링크 파일을 제공하므로 그냥 /dev/cdrom CD/DVD 장치라고 기억해놓는 것이 편리하다.
	-  /dev/sdb1 이 방금 장착한 USB 메모리의 장치 이름이다. 실습 상황에따라 달라질 수 있다.
	-  /dev/sd\*는 하드디스크나 USB 메모리 등을 의미한다. "/dev/sda"는 CentOS가 설치된 최초 하드디스크를 나타내며 /dev/sdb 는 추가한 USB 메모리를 나타낸다. 독자의 상황에 따라 USB 메모리의 이름은 달라질 수 있다.
	- CD/DVD 및 USB 메모리를 직접 마운트시켜보자. 이번에는 /media 디렉터리에 연결하겠다. 그런데/media 디렉터리 아래에 하위 디렉터리가 없기 때문에 먼저 /media 아래에 연결할 적절한 디렉터리를 만들어 마운트한다.
	
	```
	mkdir /media/cdroom    -> CD/DVD를 의존하는 디렉터리 생성
	mkdir /media/usb         -> USB 메모리를 마운트하는 디렉토리 생성 
	mount /dev/cdrom  /media/cdrom       -> CD/DVD 마운트
	mount /dev/sdb1  /media/usb            -> USB 메모리 마운트
	```
	
	![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image29.png)
	
	- mount 명령을 입력해 마운트한 장치의 디렉터리를 확인해보자. 그리고 <b>Is /media/cdrom</b> 명령과 <b>Is/media/usb</b> 명령을 입력해 해당 파일들이 잘 보이는지 확인하자.
	
	![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image30.png)
	
	![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image31.png)
	
	- 만약 /media/usb 디렉터리에서 파일 이름이 깨진 상태로 보인다면, 해당 파일 이름이 한글일 것이다. 텍스트 모드에서는 한글을 지원하지 않는다.
	- 마찬가지로 USB 메모리 (/media/usb 디렉터리)에 필요한 파일을 저장하거나 복사할 수 CentOS 리눅스의 아무 파일이나 USB 메모리에 복사하자.
	
	```
	cp /media/usb/py*  .    --> 적당한 파일을 현재 디렉토리에 복사(제일 뒤에 . 있음)
	ls
	cp	ana* /media/usb   -->적당한 파일을 USB 메모리에 복사
	ls /media/usb
	```
	
	![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image32.png)
	
	- 사용이 끝났다면 <b>umount 마운트장치</b> 명령를 입력해 마운트된 장치의 연결을 해제하자. 아무 메시지도 안 나오면 마운트 해제된 것이다.
	
	![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/4%EC%9D%BC%EC%B0%A8(3h)%20-%20%EB%A6%AC%EB%88%85%EC%8A%A4%20%EA%B8%B0%EB%B3%B8%20%EA%B0%9C%EB%85%90/images/image33.png)
	
	
	- 그런데 이번에는 장치 이름인 /dev/cdrom 이나 /dev/sdb1 이 아니라, 마운트된 디렉터리인 /media/cdrom과 /media/usb 를 언마운트시켰다. 이렇게 언마운트시켜도 잘 작동한다(단, 현재 디렉터리가/media/cdrom이나 /media/usb 면 안 된다. 그럴 경우 언마운트되지 않고 target is busy'라는 메시지가 나올 것이다).
	
	- 이제는 VirtualaBox에서 USB 메모리의 마운트를 해제한다. 또한 DVD의 연결도 끊는다. 그리고 halt -p 명령으로 Server (B)를 종료하자.
	- 호스트 컴퓨터의 파일 탐색기에서 확인하면 USB 메모리가 연결되어 있고 앞서 CentOS에서 복사했던 파일도 확인할 수 있다. 이것은 호스트 컴퓨터와 Server (B)가 파일을 주고받을 때 유용하게 사용할 수 있는 방법이므로 잘 기억해두자.
	
####  CD/DVD 장치
- CD/DVD 장치 이름을 "/dev/cdrom"으로 사용했는데, "/dev/sr0"과 "/dev/cdrom"은 동일하게 취급해도 된다(사실 "/dev/cdrom"은 "/dev/sr0"에 링크된 파일이다).

- 리눅스에 따라서 "/dev/sr0"이라는 이름은 변경될 수 있으나, "/dev/cdrom"이라는 링크 이름은 대부분 고정되어 있다. 그러므로 앞으로는 CD/DVD 장치를 "/dev/cdrom"으로 기억하는 것이 편리할 것이다.








