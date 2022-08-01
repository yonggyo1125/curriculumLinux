# 셸의 기본

- 셸은 사용자가 입력한 명령을 해석해 커널로 전달하거나, 커널의 처리 결과를 사용자에게 전달하는역할을 한다. 
- 쉽게 말해 Server (B)의 '텍스트 모드'나 X 윈도의 '터미널'처럼 명령을 입력하는 환경이 셸이라고 생각해도 무방하다.

## CentOS의 bash 셸


- CentOS에서 기본적으로 사용하는 셸은 bash(Bourne Again SHell)이다. '배시 셸'이라고 읽으며 Bourne Shell(sh)을 기반으로 Korn Shell(ksh)과 CShells(csh)의 좋은 점을 합한 것이라고 보면 된다. 
- bash의 특징은 다음과 같다.
	- Alias 기능(명령어 단축 기능)
	- History 기능(위 아래 화살표)
	- 연산 기능
	- Job Control 기능
	- 자동 이름 완성 기능([Tab])
	- 프롬프트 제어 기능
	- 명령 편집 기능

> alias 명령은 긴 명령을 줄여서 사용할 때 편리하다. 예를 들어 Is al을 Is2라는 명령어로 사용하고 싶다면 alias Is2="ls-al" 명령으로 정의하면 된다.

## 셸 명령문 처리 방법

- 셸 명령문은 명령문과 함께 여러 가지 옵션이나 인자(Argument)를 사용할 수 있으며, 형식은
 다음과 같다.

```
(프롬프트) 명령어 [옵션...] [인자...]
```

- 예를 들면 다음과 같이 다양한 옵션과 인자를 사용해서 명령을 사용해왔다.

```
# ls -l
# rm -rf /mydir
# find . / -name "*.conf"
```

## 환경 변수

- 셸은 여러 가지 환경 변수 값을 갖는데, 선정된 환경 변수는 <b>echo $환경변수이름</b> 형식으로 명령을 실행하면 확인할 수 있다. 예를 들어 호스트 이름을 출력하려면 <b>echo $HOSTNAME</b> 명령을 실행한다. 주요 환경 변수와 그 설명은 다음과 같다.

#### bash의 주요 환경 변수

|환경 변수|설명|환경 변수|설명|
|----|------|----|------|
|HOME|현재 사용자의 홈 디렉토리|PATH|실행 파일을 찾는 디렉토리 경로|
|LANG|기본 지원되는 언어|PWD|사용자의 현재 작업 디렉토리|
|TERM|로그인 터미널 타입|SHELL|로그인에서 사용하는 셸|
|USER|현재 사용자의 이름|DISPLAY|X 디스플레이 이름|
|COLUMNS|현재 터미널의 컬럼 수|LINES|현재 터미널 라인 수|
|PS1|1차 명령 프롬프트 변수|PS2|2차 명령 프롬프트(대개 '\>')|
|BASH|bash 셸의 경로|BASH_VERSION|bash 버전|
|HISTFILE|히스토리 파일의 경로|HISTSIZE|현재 사용자 이름|
|LOGNAME|로그인 이름|LS_COLORS|ls 명령어의 확장자 색상 옵션|
|MAIL|메일을 보관하는 경로|OSTYPE|운영체제 타입|

- 환경 변수 값을 변경하려면 <b>export 환경변수=값</b> 형식을 실행한다. 그 외의 환경 변수는 <b>printenv</b> 명령을 실행하면 출력된다. 단, 일부 환경 변수는 <b>printenv</b> 명령을 실행해도 나타나지 않는다는 사실에 주의하자.

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image1.png)

## 셸 스크립트 프로그래밍 실습

- 리눅스의 셸 스크립트는 C 언어와 유사한 방법으로 프로그래밍할 수 있다. 왜냐하면 리눅스의 대부분을 C 언어로 작성했기 때문이다. 그래서 프로그래밍 언어 (특히 C 언어)를 다뤄본 적이 있는 독자라면 쉽게 셸 스크립트를 익힐 수 있을 것이다.

- 셸 스크립트도 일반적인 프로그래밍 언어와 비슷하게 변수, 반복문, 제어문 등을 사용할 수 있다. 또한 별도로 컴파일하지 않고 텍스트 파일 형태로 셸에서 바로 실행할 수 있다. 그래서 셸 스크립트는주로 vi 에디터나 gedit으로 작성하는 편이다.

- 셸 스크립트를 공부하면 좋은 이유는 리눅스의 많은 부분이 셸 스크립트로 작성되었기 때문이다. 예를 들어 GRUB 2의 설정 파일인 /boot/grub2/grub.cfg 파일도 셸 스크립트 문법을 사용한다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image2.png)

### 셸 스크립트 작성과 실행

- vi name.sh 명령이나 gedit name.sh 명령을 실행해 다음과 같은 간단한 셸 스크립트를 작성해보자.

> 셸 스크립트 파일의 확장명을 지정하지 않거나, 다른 것으로 지정해도 되지만 사용자가 작성한 셸 스크립트 파일은 되도록 확장명을 sh로 지정하자. 그러면 파일 이름만으로 이 파일이 셸 스크립트 파일인지 알 수 있다.

#### name.sh

```
1 #!/bin/sh
2 echo "사용자 이름: " $USER
3 echo "홈 디렉토리: " $HOME
4 exit 0
```

- 소스 설명
	- 1행 : 특별한 형태의 주석 (#!)으로 bash를 사용하겠다는 의미다. 첫 행에 꼭 써줘야 한다.
	- 2행 :  echo 명령은 화면에 출력하는 명령이다. 먼저 "사용자 이름"이라는 글자를 출력하고, 옆에는 $USER라는 환경 변수의 내용을 출력한다.
	- 4행 : 종료 코드를 반환하게 해준다. 만약 다른 스크립트에서 이 스크립트를 호출한 후 제대로 실행되었는지 확인하려면 적절한 종료 코드를 반환하는 것이 중요하다.<br>즉 이 행은 실제 스크립트 실행과 무관하지만, 셀 스크립트는 실행 중간에 문제가 생겨도 무조건 성공했다는 메시지를 반환하기 때문에 직접 마지막 행에서 성공인지 실패인지를 반환하는것이 좋다. 0은 성공을 의미한다.


- 셸 스크립트를 실행하는 방법에는 크게 두 가지가 있다.

#### sh 명령으로 실행

- <b>sh 스크립트파일</b> 명령으로 실행할 수 있다. 셸 스크립트 파일의 속성을 변경할 필요가 없다는 장점이있다.

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image3.png)

#### '실행 가능' 속성으로 변경한 후 실행

- 먼저 셸 스크립트 파일의 속성을 '실행 가능'으로 변경한 후 스크립트파일 명령을 실행한다

```
# chmod +x name.sh
# ./name.sh
```

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image4.png)

- <b>chmod +x 파일명</b> 명령은 현재 파일의 속성에 '실행 가능' 속성을 추가하라는 의미다.

> <b>./스크립트파일</b> 명령에서 '.' 은 현재 디렉터리를 의미한다. 그러므로 현재 디렉터리의 스크립트 파일을 실행하라는 의미다. 반드시 현재 디렉터리인 './'를 입력하는 이유는 현재 디렉터리 (이 예에서는 /root) 가 $PATH 환경 변수에 설정되어 있지 않기 때문이다. 일반적으로 명령이나 스크립트 이름을 입력하면 셸은 $PATH 환경 변수에 설정된 디렉터리만 찾아본다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image5.png)

- 지금부터는 별도로 언급하지 않아도 셸 스크립트 소스를 직접 입력하고 저장한 후 실행해서 결과를 확인하면 된다.

#### 셸 스크립트 사용

- 지금 작성한 셸 스크립트는 root 사용자 권한으로 작성한 것이므로, root 사용자만 사용할 수 있다. 
- 이 셸 스크립트를 다른 사용자도 사용하게 하려면 /usr/local/bin/ 디렉터리에 복사하고 권한을 755로 변경하면 된다. 
- 보안상 위험할 수도 있으므로 이 작업은 root 사용자만 할 수 있다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image6.png)

### 변수

- 변수는 필요한 값을 계속 변경해 저장한다는 개념이다. 셸 스크립트의 구조는 변경할 필요가 없는데 설정해야 하는 값이 상황에 따라 다르다면 변수에 필요한 값을 계속 바꿔가는 방법으로 프로그래밍해서 다양한 상황에 대처할 수 있다.

#### 변수의 기본

- 셸 스크립트에서는 변수를 사용하기 전에 미리 선언하지 않으며, 처음 변수에 값이 할당되면 자동으로 변수가 생성된다.
- 변수에 넣는 모든 값은 문자열(String)로 취급한다. 즉, 숫자를 넣어도 문자로 취급한다.
- 변수 이름은 대소문자를 구분한다. 즉, $aa라는 변수 이름과 $AA라는 변수 이름은 다르다. 변수를 대입할 때 '=' 좌우에는 공백이 없어야 한다.
<br>
- 터미널에서 직접 다음을 입력해보자.

```
testval = hello   -> 오류! '=' 앞뒤에 공백이 있다
testval=hello
testval=Yes Sir    -> 오류! 값의 공백은 " "로 묶어야 한다.
testval="Yes Sir"
testval=7+5      -> 정상이지만 "7+5"라는 문자열로 인식한다.
```

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image7.png)

#### 변수의 입력과 출력

- '$'라는 문자가 들어간 글자를 출력하려면 ''로 묶어주거나 앞에 '\'를 붙여야 한다. 또한 ""로 변수를 묶어줘도 되며 묶어주지 않아도 된다. 

#### var1.sh

```
1 #!/bin/sh
2 myvar="Hi Lee"
3 echo $myvar
4 echo "$myvar"
5 echo '$myvar'
6 echo \$myvar
7 echo 값 입력 : 
8 read myvar
9 echo '$myvar' = $myvar
10 exit 0
```

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image8.png)

- 소스 설명
	- 3행 : 'Hi Woo'라는 정상적인 값을 출력한다.
	- 4행 : 3행과 동일한 효과다.
	- 5행 : '$myvar'라는 글자를 출력한다.
	- 6행 : \$는 $를 글자로 취급하게 한다. 결국 5행과 동일한 효과다.
	- 8행 : 변수 myvar에 키보드로 값(문자열)을 입력한다.

> '$변수'와 "$변수"는 일반적으로 동일하게 인식한다. 하지만 변수에 입력된 값에 공백이 포함될 수 있다면, 공백 때문에 발생할 수 있는 논리 오류를 방지하는 데 도움이 되는 "$변수" 형식으로 사용하는 것이 좋다.

#### 숫자 계산

- 변수에 넣은 값은 모두 문자열로 취급한다고 했다. 
- 만약 변수에 들어 있는 값에 + -,\*, / 등의 연산을 하려면 expr 키워드를 사용하면 된다. 
- 단, 수식과 함께 꼭 키보드 숫자1 왼쪽에 있는 역따옴표(\`)로 묶어줘야 한다. 그리고 수식에 괄호를 사용하려면 그 앞에 꼭 역슬래시 (\\) 를 붙여줘야 한다. 또 +, -, / 와 달리 곱하기 (\*) 기호도 예외적으로 앞에 역슬래시 (\\)를 붙여줘야 한다.


#### numcalc.sh

```
1 #!/bin/sh
2 num1=100
3 num2=$num1+200
4 echo $num2
5 num3=`expr $num1 + 200`
6 echo $num3
7 num4=`expr \( $num1 + 200 \) / 10 \* 2`
8 echo $num4
9 exit 0
```

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image9.png)

- 소스 설명
	- 3행 : 문자열로 취급함 -> 모두 붙여서 써야 한다.
	- 5행 : 숫자로 취급해서 계산함  -> 각 단어마다 띄어쓰기를 해야 한다.
	- 7행 : 괄호와 '\*'앞에는 역슬래시 (\\) 를 붙인다.

#### 파라미터 변수

- 파라미터(Parameter) 변수는 $0 $1, $2 등의 형태를 갖는다. 이는 실행하는 명령의 부분 하나하나를 변수로 지정한다는 의미다. 예를 들어 <b>dnf -y install gftp</b> 명령을 실행한다고 가정하면, 파라미터 변수는 다음과 같이 지정할 수 있다.

||||||
|----|----|----|----|----|
|명령|dnf|-y|install|gftp|
|파라미터 변수|$0|$1|$2|$3|

- 즉 $0에는 dnf가, $1에는 y를 저장한다. 그리고 명령 전체의 파라미터 변수는 $\*로 표현한다.

#### paravar.sh

```
1 #!/bin/sh
2 echo "실행파일 이름은 <$0>이다"
3 echo "첫번째 파라미터는 <$1>이고, 두번째 파라미터는 <$2>다"
4 echo "전체 파라미터는 <$*>다"
5 exit 0
```

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image10.png)

### if문과 case문

- if 문과 case 문의 기본 사용 방법을 살펴보자.

#### 기본 if문

- 대부분의 프로그래밍 언어에서 지원하는 if문을 살펴보자. 기본 문법은 다음과 같다.

```
if [ 조건 ]
then
	참일 경우 실행
fi
```

> 주의할 점은 [조건] 사이의 각 단어에는 모두 공백이 있어야 한다는 것이다. 실수하기 쉬우므로 꼭 기억하자.

#### if1.sh

```
1 #!/bin/sh
2 if [   "lee" = "lee"  ]
3 then 
4   echo "참입니다"
5 fi
6 exit 0
```

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image11.png)

- 2행 : '\[ \]' 사이에는 참과 거짓을 구분하는 조건식이 들어간다. '='은 문자열이 같은지를 비교하며 "!="은 문자열이 같지 않은지 비교한다. if1.sh에서는 조건식이 참이므로 4행을 실행한다. 또 '\[ \]' 대신 test라는 키워드를 사용할 수도 있다. 2행과 <b>if test "woo" = "woo"</b>는 동일한 구문이다.

#### if~else문

- 참인 경우와 거짓인 경우를 구분해서 실행한다. 형식은 다음과 같다.

```
if [ 조건 ]
then
    참인 경우 실행
else
    거짓인 경우 실행
fi
```

#### if2.sh

```
#!/bin/sh
if [ "lee" != "lee" ]
then
   echo "참입니다"
else 
   echo "거짓입니다"
fi 
exit 0
``` 

> 중복 if문을 위해서 else if 가 합쳐진 elif 구문도 사용할 수 있다.

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image12.png)

#### 조건문에 들어가는 비교 연산자

- 조건문에 들어가는 비교 연산자에는 문자열 비교 연산자와 산술 연산자가 있다. 다음 표를 참고한다.

|문자열 비교|결과|
|-----|------|
|"문자열1" = "문자열2"|두 문자열이 같으면 참|
|"문자열1" != "문자열2"|두 문자열이 같지 않으면 참|
|-n "문자열"|문자열이 NULL(빈 문자열)이 아니면 참|
|-z "문자열"|문자열이 NULL(빈 문자열)이면 참|

- 산술 비교 연산자는 다음과 같다.

|산술 비교|결과|
|-----|------|
|수식1 -eq 수식2|두 수식(또는 변수)이 같으면 참|
|수식1 -ne 수식2|두 수식(또는 변수)이 같지 않으면 참|
|수식1 -gt 수식2|수식1이 크다면 참|
|수식1 -ge 수식2|수식1이 크거나 같다면 참|
|수식1 -lt 수식2|수식1이 작으면 참|
|수식1 -lte 수식2|수식1이 작거나 같으면 참|
|!수식|수식이 거짓이면 참|

#### if3.sh

```
#!/bin/sh
if [ 100 -eq 200 ]
then
   echo "100과 200은 같다."
else 
   echo "100과 200은 다르다"
fi
exit 0
```

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image13.png)

#### 파일과 관련된 조건

- if 문에서 파일을 처리하는 조건은 다음과 같다.

|파일 조건|결과|
|-----|------|
|-d 파일이름|파일이 디렉토리면 참|
|-e 파일이름|파일이 존재하면 참|
|-f 파일이름|파일이 일반 파일이면 참|
|-g 파일이름|파일에 set-group-id가 설정되면 참|
|-r 파일이름|파일이 읽기 가능이면 참|
|-s 파일이름|파일 크기가 0이 아니면 참|
|-u 파일이름|파일에 set-user-id가 설정되면 참|
|-w 파일이름|파일이 쓰기 가능 상태면 참|
|-x 파일이름|파일이 실행 가능 상태면 참|

#### if4.sh

```
1 #!/bin/sh
2 fname=/lib/systemd/system/sshd.service
3 if [ -f $fname ]
4 then 
5    head -5 $fname
6 else 
7    echo "sshd 서버가 설치되지 않았습니다."
8 fi
9 exit 0
```

![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux1/18~20%EC%9D%BC%EC%B0%A8(9h)%20-%20%EC%89%98%20%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/images/image14.png)

- 소스 설명
	- 2행 : fname 변수에 httpd 서버 실행 파일인 /lib/systemd/system/sshd.service 저장
	- 3행 : fname 변수에 저장된 /lib/systemd/system/sshd.service 파일이 일반 파일이면 참이므로 5행을 실행, 그렇지 않으면 거짓이므로 7행을 실행
	- 5행 : fname에 들어 있는 파일의 앞 5줄 출력

#### case~esac문

- if문은 참과 거짓이라는 두 가지 경우만 사용할 수 있다(이를 '2중 분기'라고 한다). 그런데 여러 가지 경우의 수가 있다면 if문을 계속 중복해서 사용해야 하므로 구문이 복잡해진다. 이때 사용하는 것이 case문이다. 이를 '다중 분기'라고 한다.

#### case1.sh
