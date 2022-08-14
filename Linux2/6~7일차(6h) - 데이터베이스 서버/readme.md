# DBMS의 개념과 간단한 SQL문

## DBMS 관련 용어와 역할의 이해

- MariaDB 및 Oracle을 운영하기 전에 DBMS와 관련된 기본 용어를 소개하겠다. 어떤 역할을 하는지 명확히 이해해보자. 먼저 관련 용어의 사전적인 정의를 살펴보자.

#### 관련 용어

|관련 용어|사전적 정의|
|----|-------|
|데이터(Data)|자료|
|테이블(Table)|데이터를 표 형식으로 표현|
|데이터베이스(Database)|테이블을 저장하는 저장 공간 또는 테이블의 집합|
|DBMS(DataBase Management System)|데이터베이스들을 관리하는 소프트웨어|
|레코드(Record) 또는 로우(Row)|테이블의 행|
|필드(Field) 또는 컬럼(Column)|테이블의 열|
|데이터 타입(Data Type)|각 필드에 입력할 값의 타입(정수, 문자, 날짜 등)|
|필드 이름|각 필드(열)의 이름|
|주 키(Primary Key)필드|레코드를 식별하기 위한 유일한 값을 갖고 비어 있지 않은 필드|
|외래 키(Foreign Key)필드|다른 테이블의 주 키와 대응되는 필드|
|RDBMS(Relational DBMS)|관계형 DBMS|
|SQL(Structured Query Language)|'구조화된 질의 언어'라는 의미로 DB에서 정보를 얻거나 생성 및 갱신하려고 정의한 표준 언어(규격)|

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image1.png)

- 인터넷 쇼핑몰 업체의 데이터베이스를 간략하게 나타낸 것이다. 쿠팡, 옥션, 인터파크, G마켓 등의 인터넷 쇼핑몰이라고 생각하면 이해하기 쉬울 것이다. 이 데이터베이스에는 회원으로 가입한 고객의 정보와 고객이 구매한 물품의 정보가 들어 있다.

- 데이터(Data)
	- hong, 홍길동, 22살, 경기 등의 단편적인 정보를 데이터라고 한다. 누가 "홍길동에 속해 있는 데이터가 무엇이지?"라고 묻는다면 "나이는 22살이고 집은 경기도입니다." 정도로 대답할 수 있을 것이다. 이처럼 정보는 있으나 완전히 체계적으로 정리되지 않은 것을 데이터라고 생각하면 된다.

- 테이블(Table)
	- 단편적인 정보를 표 형태로 체계화시켜 구성한 것을 테이블이라고 한다. 위 그림의 큰 원통 안에는 테이블 2개가 있다. 또 각 테이블에는 이름을 붙일 수 있다. '고객 정보', '구매 정보'가 테이블의 이름이다.

- 데이터베이스(Database)
	- 고객 정보인 CUSTOMER, 구매 정보인 PURCHASE 같은 테이블이 들어 있는 커다란 저장소라고 생각하면 된다. 데이터베이스는 위 그림처럼 주로 원통 모양으로 그린다. 그리고 각 데이터베이스에는 이름을 붙인다.  shopping_db, mysql, test라는 3개의 데이터베이스가 있다. 이 중 mysql과 test 데이터베이스는 시스템에서 제공하는 데이터베이스며, shopping_db는 사용자가 생성한 데이터베이스다. 데이터베이스를 더 쉽게 이해하고 싶다면 '커다란 저장소(원통 모양)에 테이블을 생성'하는 것이라고 생각하자.

- DBMS(DataBase Management System)
	- 원통 모양의 데이터베이스를 관리하기 위한 소프트웨어를 DBMS 또는 데이터베이스 서버라고 부른다.
	- 사람들은 종종 DBMS를 줄여서 데이터베이스라고 부르기도 하지만, 강의에서는 서로 다른 것으로 구분하겠다(이 용어는 소프트웨어 도구마다 조금씩 다르다) 위 그림을 보면 데이터베이스는 3개의 원통, 즉 테이블을 생성할 수 있는 공간을 의미하며, DBMS는 이 데이터베이스들을 관리하는 소프트웨어 명확히 나타나 있다.
	- 3개의 데이터베이스를 감싸는 점선이 DBMS라고 생각하면 된다. DBMS 소프트웨어에는 많은 종류가 있다. 그중에서 MariaDB 및 Oracle이라는 제품을 이용할 것이다.

- 레코드(Record) 또는 로우(Row)
	- 테이블의 행을 말한다. 위 그림에서 'hong-홍길동-22-경기'가 하나의 레코드다. 그러므로 CUSTOMER 테이블에는 4개의 레코드가 있는 것이다. 이 레코드가 내포하는 의미는 '하나의 완전한 정보'로 생각할 수 있다. 즉 '고객 정보' 테이블에서 하나의 레코드만 살펴보면 해당 고객의 모든 정보를 파악할 수 있다(이는 단순한 테이블의 예다. 여러 개의 테이블이 관계된 테이블에서는 하나의 레코드만으로 모든 정보를 파악할 수 없다).
	
- 필드(Field) 또는 컬럼(Column)
	- 테이블의 열을 말한다. 여기서 각각의 필드는 반드시 이름을 갖고 있다는 것이 중요하다. 이를 '필드 이름Field Name'이라고 부른다. 위 그림의 데이터베이스 중 shopping_db의 CUSTOMER 테이블은 4개의 필드로 구성되어 있으며, 각각의 필드 이름은 ID, NAME, AGE, ADDRESS다. 각 필드는 데이터 타입Data Type이 지정되어 있다. 즉, 각 필드에 입력할 값의 타입을 결정해놓아야 한다. 예를 들어 NAME 필드는 문자로 지정해야 한다. 누가 이름에 1234 와 같은 숫자를 넣으면 안 되기 때문이다. 마찬가지로 AGE 필드는 숫자(정수)로 지정해야 한다. 나이에 '좀 많음' 같은 글자를 넣어서는 안된다.
	
- 주 키(Primary Key) 필드
	- 주 키 필드란 단순히 '필드 중에서 비어 있지 않고 중복되지 않는 필드'라고 생각할 수 있다.
	- 인터넷 사이트에 회원 가입했을 때를 생각해보자. 처음 가입 시 아이디를 생성하는 칸에 자신이 원하는 아이디를 입력하고 \<중복 확인\>이라는 버튼으로 기존 가입자가 내가 사용하려는 아이디를 사용하는지 확인했다. 누가 이미 원하는 아이디를 사용하고 있다면 독자는 같은 아이디로 가입할 수 없을 것이다. CUSTOMER 테이블이 바로 회원 가입 시 입력하게 되는 정보를 단순화한 것이다. 4개의 필드 중 ID 필드가 주 키 필드다. 아이디는 중복되지 않아야 하고 또 비어 있어도 안 된다. 아이디 없이 회원에 가입하는 것은 불가능하기 때문이다.
	- 이처럼 주 키 필드의 특징은 중복되지 않고 비어 있는 값(NULL이라 부른다)을 허용하지 않는다는 것이다. 만약 NAME 필드를 주 키로 설정한다면 어떨까? 당연히 동명이인이 있을 수 있으므로 주 키로 설정하면 안 된다. 주 키 필드의 중요한 역할은, 테이블에서 주 키 필드의 값만 안다면 정확히 어떤 레코드인지 구분할 수 있다는 것이다. CUSTOMER 테이블에서 해당 사용자의 아이디만 안다면 이름, 나이, 주소와 같은 정보를 정확히 추출해 낼 수 있다. 그래서 사람의 기본 정보와 관련된 테이블에서 주 키 필드를 지정할 때는 인터넷 회원 가입의 경우 주로 아이디를, 학생과 관련된 정보 시스템의 경우 주로 학번을, 나머지 기타 정보 시스템의 경우 주로 주민등록번호를 사용한다.
	- 이번에는 PURCHASE 테이블의 주 키 필드를 생각해보자. 단순히 생각하면 CUSTOMER 테이블처럼 고객 ID인 CUST_ID 필드를 주 키로 설정하면 될 것처럼 보인다. 하지만 그럴 경우 아주 위험한 결과를 초래할 수 있다.
	- 주 키의 정의를 다시 생각해보자. 주 키는 중복되지 않고 NULL이 아닌 값이어야 한다. 만약 PURCHASE 테이블에서 CUST_ID 필드를 주 키로 설정했다면, 제일 처음 구매한 dang이라는 사용자는 두 번 다시 이 쇼핑몰에서 물건을 살 수 없다. 다음에 물건을 살 때 주 키 필드인 CUST_ID 필드에 이미 dang이라는 값이 들어 있으므로, dang이라는 값을 또 넣는다면 중복 값을 사용하는 것이기 때문에 주 키의 정의에 어긋난다. 우습게도 주 키 설정 하나를 잘못한 결과, 우리 쇼핑몰에서는 회원 한 명이 물건 한 개를 사면 다시는 물건을 구매할 수 없게 되어 버린다. 이는 다른 필드도 마찬가지다. DATE 필드를 주 키로 설정한다면? 우리 쇼핑몰은 하루에 물건을 하나씩만 팔아야 할 것이다. PRODUCT 필드를 주 키로 설정한다면? 같은 물건을 두 번 다시 팔 수 없다.
	- 그렇다면 PURCHASE 테이블에는 주 키로 설정할 만한 적당한 필드가 없어 보인다. 그럴 경우 주 키를 설정하지 않아도 된다. 하지만 주 키는 설정하는 것이 바람직하므로 제일 앞에 일련번호를 의미하는 'NO'라는 필드를 생성해서 사람들이 물건을 살 때마다 차례로 1, 2, 3, 4, ...로 증가시키며 값을 입력하게 만드는 것이 좋다. 중복될 일도 없고 NULL 값이 들어가지도 않을 것이므로 주 키로 설정하기에 아주 적절한 필드가 되기 때문이다. 그래서 PURCHASE 테이블의 주 키를 'NO' 필드로 설정한 것이다.

- 외래 키(Foreign Key)필드
	- 외래 키 필드는 2개의 테이블을 연관시키는 필드다. 위 그림에서는 PURCHASE 테이블의 CUST_ID 필드가 CUSTOMER 테이블 ID 필드의 외래 키가 된다.
	- 외래 키의 필요성 역시 명확하다. 예를 들어 우리 쇼핑몰의 회원이 아닌데도 어떤 사람이 물건을 사려고 하면 아마 물건을 살 수 없고 (구매 정보 테이블에 레코드를 입력할 수 없고), 먼저 회원 가입을 해야할 것이다(고객 정보' 테이블에 레코드가 입력되어야 한다).
	- 또 위 그림의 CUSTOMER 테이블에서 hong이라는 사용자의 레코드를 삭제한다면? 원칙적으로는 삭제되지 않는다. PURCHASE 테이블에 hong이라는 사용자가 있기 때문이다. 이 경우 PURCHASE 테이블의 hong이라는 CUST_ID 필드의 레코드를 모두 삭제한 후, CUSTOMER 테이블의 hong 레코드를 삭제해야 한다.

- RDBMS(Relational DBMS)
	- 관계형 DBMS는 지금 설명한 테이블과의 관계성 Relationship을 기반으로 한 DBMS를 말한다. Oracle, SQL Server, MariaDB 등 DBMS 대부분은 관계형 DBMS이거나 관계형 DBMS를 지원한다.

- SQL(Structured Query Language)
	- DBMS가 하는 일들을 대략 이야기하면 데이터베이스 생성, 테이블 생성, 레코드 입력/수정/삭제 등의 작업이다. 그런데 이러한 작업을 진행할 때 사람에게 말하듯 "어이~ MariaDB씨 레코드를 삭제하세요”라고 할 수는 없을 것이며, DBMS가 알아듣는 언어로 이야기해야 할 것이다. 이렇게 DBMS가 알아듣는 언어를 SQL이라고 부른다.


## 필수 SQL문

- 먼저 데이터베이스 개발자가 아닌 데이터베이스 관리자 입장에서 필수로 알아야 할 SQL문을 살펴본다. 이번에는 SQL의 원형 Prototype만 살펴보고, 다음 절에서 MariaDB를 설치한 후 지금 익히는 원형으로 데이터베이스를 구축하고 운영하는 실습을 해보겠다. 원형은 SQL문을 처음 접해서 생소한 독자라도 꼭 필요한 것들이니 눈으로라도 익혀두자. 또한 지금 설명하는 SQL문은 MariaDB에 적용되는 SQL문 위주인데, 다른 DBMS도 대부분 비슷하게 적용된다는 사실을 기억하자.

- 먼저 유닉스와 리눅스가 대소문자를 명확히 가리는 반면, SQL문은 대소문자를 구분하지 않는다(단, 테이블 이름 같은 일부 예외는 있다). 하지만 필자는 SQL문의 예약어는 주로 대문자로, 사용자가 입력하는 부분은 주로 소문자로 표기해서 가독성을 높여보겠다.

- 또한 MariaDB의 SQL문 제일 뒤에는 꼭 세미콜론(;)을 넣어야 한다. 물론 일부 SQL문은 넣지 않아도 실행되지만, 그냥 무조건 넣는다고 생각하자.

### 데이터베이스와 관련된 SQL문

#### 데이터베이스 이름 조회
- 구문: SHOW DATABASES;
- 이 명령을 입력하면 결과는 shopping_db, mysql, test 3개의 데이터베이스 이름이 나올 것이다.

#### 사용할 데이터베이스 지정

- 구문: USE 데이터베이스이름;
- 예: USE shopping_db;
- 지금부터 shopping_db라는 데이터베이스를 사용하겠다는 의미다.

#### 데이터베이스 생성

- 구문: CREATE DATABASE 데이터베이스이름; 
- 예: CREATE DATABASE shopping_db;
- shopping_db라는 이름의 데이터베이스를 생성한다. 이 구문은 비어 있는 데이터베이스를 만들어줄 뿐 안에는 아무 내용도 없다.

#### 데이터베이스 삭제

- 구문: DROP DATABASE 데이터베이스이름:
- 예: DROP DATABASE shopping_db;
- shopping_db 데이터베이스가 완전히 삭제된다.

### 테이블 운영과 관련된 SQL문

#### 테이블 이름 조회
- 구문: SHOW TABLES;
- 현재 선택한 데이터베이스에 있는 테이블 이름을 조회한다. 예를 들어 현재 선택한 데이터베이스가 shopping_db라는 데이터베이스라면 CUSTOMER, PURCHASE라는 2개의 테이블 이름이 나온다.

#### 테이블 구조(형태) 조회

- 구문: EXPLAIN 테이블이름; 또는 DESC 테이블이름;
- 예: EXPLAIN customer;
- CUSTOMER 테이블의 필드 이름, 데이터 타입 등의 정보를 보여준다.

#### 테이블 생성

- 구문: CREATE TABLE 테이블이름 (필드이름1 필드타입1, 필드이름2 필드타입2 ...., ....);
- 예: CREATE TABLE customer (id CHAR(10), name VARCHAR(10), age INT, ADDRESS VARCHAR(30));
- '고객 정보' 테이블을 생성한다.

> 위 그림에서는 보기 쉽게 데이터베이스 이름과 테이블 이름에 한글을 사용했지만, 실제로는 데이터베이스 이름과 테이블 이름, 필드 이름에 한글을 사용하면 안 된다. 일부 DBMS 소프트웨어는 테이블 이름/필드 이름을 한글로 지정하는 것을 지원하지만, 그래도 한글을 사용하는 것은 바람직하지 않다. 한글은 실제 데이터인 레코드의 값(홍길동, 서울 등)을 입력할 때만 사용해도 충분하다.

#### MariaDB의 데이터 형식

- 테이블 생성에서 각 필드의 타입을 지정할 때 사용할 수 있는 자료형은 몇 가지가 있다. 그중 자주 사용하는 것만 살펴보자.
	- VARCHAR(n): 최대 n개의 크기를 갖는 가변 길이 문자열
	- CHAR(n): n개의 문자가 저장되는 고정 길이 문자열
	- INT: 정수형 숫자
	- FLOAT: 실수형 숫자
	- DATE: 날짜를 저장
	- TIME: 시간을 저장

- 이 중에서 VARCHAR와 CHAR는 거의 같은 형태지만 다른 점이 있다. 예를 들어 VARCHAR(100)과 CHAR(100)이라고 정의했다면 'ABCDE'라는 글자를 저장할 때 VARCHAR 타입은 이름 그대로 가변적으로 5바이트만 사용한다. 하지만 CHAR 타입은 무조건 100바이트를 확보한 후 5바이트만 글자를 쓴다. 즉 95바이트가 낭비된다.
- VARCHAR 타입은 공간을 가변적으로 사용하므로 입력될 데이터의 크기를 예상하기 어려울 때 사용하면 적절하다. 예를 들어 주소 같은 정보의 경우, 어떤 사람은 길 수도 있고 어떤 사람은 짧을 수도 있으므로 VARCHAR 타입을 사용하기에 적절하다고 할 수 있다. 하지만 주민번호/학번 같이 자릿수가 고정된 데이터를 입력할 때는 CHAR 타입이 더 적당하다. CHAR 타입은 길이가 고정되어 있으므로 VARCHAR 타입과 비교했을 때 속도 면에서 약간 유리하다.


#### 테이블 삭제

- 구문: DROP TABLE 테이블이름;
- 예: DROP TABLE customer;
- customer 테이블 삭제

#### 테이블 수정
- 구문: ALTER TABLE 옵션
- 예: ALTER TABLE customer MODIFY name CHAR(20);
	- customer 테이블의 name 필드 데이터 타입을 CHAR (20)으로 변경
	
- ALTER TABLE customer CHANGE name fullname CHAR(10);
	- customer 테이블의 name 필드 이름을 fullname으로 바꾸고 자릿수는 CHAR(20)으로 지정

- ALTER TABLE customer ADD phone VARCHAR(20) AFTER name;
	- customer 테이블에서 name 필드 바로 다음에 전화번호를 의미하는 phone 필드 추가
ALTER TABLE customer DROP age:
	- customer 테이블에서 age 필드 삭제

### 레코드 입력/삭제/수정과 관련된 SQL문

#### 레코드 입력
- 구문: INSERT INTO 테이블이름 VALUES (값1, 값2, ..., ...);
- 예: INSERT INTO customer VALUES ('hong', '홍길동', 22, ‘경기');
	- 위 그림의 customer 테이블에 홍길동 고객의 레코드 입력

#### 레코드 삭제
- 구문: DELETE FROM 테이블이름 WHERE 조건;
- 예: DELETE FROM customer WHERE id=hong";
	- customer 테이블에서 id 필드 값이 'hong'인 레코드 삭제

#### 레코드 수정

- 구문: UPDATE 테이블이름 SET 필드이름1=수정할값1, 필드이름2=수정할값2, ...  WHERE 조건;
- 예:UPDATE customer age=25 WHERE id=hong';
	- customer 테이블에서 id필드 값이 'hong'인 레코드의 age 필드 값을 25로 수정

### 테이블 조회

#### 테이블 조회
- 구문: SELECT 필드이름1, 필드이름2, ..., ... FROM 테이블이름 WHERE 조건;
- 예: SELECT \* FROM customer;
	- customer 테이블에서 모든 레코드의 모든 필드 조회
- SELECT id, name FROM customer;
	- customer 테이블에서 모든 레코드의 id 필드와 name 필드 값 조회
- SELECT id, name FROM customer WHERE id = "john';
	- customer 테이블에서 id필드 값이 “john'인 레코드의 id 필드와 name 필드 값 조회
- SELECT id, name FROM customer WHERE age >= 25;
	- customer 테이블에서 age 필드 값이 25 이상인 레코드의 id필드와 name 필드 값 조회

- 우선 이 정도만 알아두면 앞으로 우리가 사용할MariaDB를 운영하는 데 큰 불편은 없을 것이다.

* * * 
# MariaDB 설치와 운영

- 리눅스를 DBMS로만 사용해도 충분히 그 진가를 발휘할 수 있다. 이번 절에서는 리눅스를 DBMS서버 전용으로 운영한다고 가정하고 MariaDB의 최신 버전을 설치 및 운영해보자.

> MySQL과 MariaDB<br><br>오픈 소스 기반의 데이터베이스로 MySQL이 오랫동안 가장 많이 사용되어 왔다. 그런데 MySQL이 Sun사에인수되고 다시 Sun사가 오라클(Oracle)사에 인수되자, 오라클사의 라이선스 정책에 동조하지 않는 주요 핵심 개발자들이 2009년도에 퇴사해서 별도의 데이터베이스 도구를 개발했는데, 이것이 MariaDB다. 그러므로MariaDB는 MySQL과 거의 동일한 제품이라고 보면 된다. 현재는 CentOS를 비롯한 많은 리눅스 진영에서MySQL 대신 MariaDB를 기본 DBMS로 제공한다.

## MariaDB 서버 및 클라이언트 다운로드와 설치

### 실습 1

Server를 DBMS 전용 서버로 운영하자.

#### step 0

- Server를 처음 설치 상태로 초기화하자
- 부팅하고 root 사용자로 접속한다.

#### step 1

- MariaDB를 다운로드하자. CentOS 8은 MariaDB 10.3 버전을 포함하지만, 이번에는 직접 MariaDB 사이트에서최신 버전인 10.8.3 버전의 RPM 파일을 다운로드해서 설치해보자.

- 웹 브라우저로 https://mariadb.org/ 에 접속한 후 \<Download\>를 클릭하자.

- MariaDB Repositories 탭을 선택하고 CentOS8 (x86_64)를 선택하고 버전은 10.8을 선택한다.

#### step 2
- 확인한 레포지토리 주소 및 설정을 vi 에디터를 이용하여 추가한다. 

```

vi /etc/yum.repos.d/MariaDB.repo
```

```
# MariaDB 10.8 CentOS repository list - created 2022-08-13 04:23 UTC
# https://mariadb.org/download/
[mariadb]
name = MariaDB
baseurl = https://ftp.harukasan.org/mariadb/yum/10.8/centos8-amd64
module_hotfixes=1
gpgkey=https://ftp.harukasan.org/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image3.png)

- <b>dnf -y install MariaDB-server</b> 명령어를 실행하여 MariaDB 서버를 설치한다.

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image4.png)

- 다음 명령을 차례로 입력해 서비스를 가동하자. 참고로 MariaDB의 서비스 이름은 mariadb다.

```
systemctl restart mariadb     -> 서비스 시작
systemctl enable mariadb    -> 서비스 상시 가동
systemctl status mariadb     -> 서비스 가동 확인
```

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image5.png)

> 서비스 등록 차이<br>CentOS 8에 포함된 서버 패키지를 dnf 명령으로 설치하면 lib/systemd/system/ 디렉터리에 서비스이름.service 또는 서비스이름.socket으로 등록된다. 이 서비스를 시작/중지하려면 <b>systemctl start/stop 서비스이름</b> 명령을 사용하고 상시 가동하려면 <b>systemctl enable 서비스이름</b> 명령을 사용한다.

- firewall-config 명령을 입력해 [방화벽 설정]을 실행한다. [설정]에서 [영구적]을 선택한 후 [영역]에서 [public]이 선택된 상태로 오른쪽 [서비스] 탭 [mysql]의 체크를 켜 MariaDB 서버를 열어주자. 설정을 적용하기 위해 메뉴의 [옵션] - [Firewalld 다시 불러오기]를 선택한 후 [방화벽 설정]을 닫는다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image6.png)

> 각 서버의 포트 번호는 /etc/services 파일에 설정되어 있다. mysql의 포트는 3306이다.

- 이제는 MariaDB 클라이언트 프로그램을 이용해서 MariaDB 서버에 접속해보자. MariaDB 클라이언트 프로그램의 실행 명령인 <b>mysql</b>을 입력한다. [MariaDB [(none)]\>] 프롬프트가 나오면 서버에 정상적으로 접속된 것이다. 이제 앞 절에서 배운 SQL문을 사용하면 된다. 우선은 <b>exit</b> 명령을 입력해 종료한다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image7.png)

## Windows에서 리눅스 MariaDB 서버로 접속

- 데이터베이스 서버에는 중요한 정보를 많이 보관한다. 그래서 대부분의 DBMS는 사용자와 관련된 보안 정책이 별도로 있다. 즉 아무나 DBMS에 접속할 수 있는 것이 아니라 허가받은 사용자만 접속할 수 있는 것이다.

- 여기서 이야기하는 사용자란 '데이터베이스 사용자'를 말하며 '운영체제 사용자'와는 별개의 개념이다. \<실습 1\>에서 아직 MariaDB 서버에 별도의 데이터베이스 사용자를 지정한 적이 없다. 그런데 mysql 명령을 입력하니까 아무런 확인 절차 없이 그냥 MariaDB 서버에 접속할 수 있었다. 그렇다면 운영체제의 root 사용자는 권한이 막강하므로 MariaDB 서버도 그냥 접속된 것일까? 그렇지는 않다. CentOS를 설치했을 때를 기억해보자. 별도의 사용자로 생성하지 않아도root 사용자는 원래 존재했었고, 설치 과정 중에서 root 사용자의 비밀번호만 지정했었다.

- 마찬가지로 MariaDB 서버를 설치하면 별도의 데이터베이스 사용자를 생성하지 않아도 root라는 이름의 데이터베이스 사용자가 자동으로 생성되며, 비밀번호는 지정하지 않은 상태로 설치된다
- 데이터베이스 사용자인 root는 MariaDB 서버 안에서 모든 권한을 실행할 수 있는 데이터베이스 관리자다. 운영체제 사용자인 root와 우연히 이름만 같을 뿐 전혀 별개의 사용자다.

- 그래서 원칙적으로 MariaDB 서버에 접속하려면 <b>mysql -h 접속할컴퓨터 -u DB사용자이름 -p</b> 명령을 실행한 후, 데이터베이스 사용자의 비밀번호를 입력해서 접속해야 한다.

- 그런데 옵션을 모두 생략하고 mysql 명령만 실행하면, 우선 MariaDB가 설치된 컴퓨터를 현재 컴퓨터로 간주하고 현재 운영체제의 사용자와 같은 이름인 root 사용자 권한으로 비밀번호 없이 접속하게 된다. 즉, 지금 우연히도 현재 사용 중인 컴퓨터에 현재 운영체제 사용자 이름과 데이터베이스 사용자의 이름이 root고, 아직 데이터베이스 사용자인 root에 비밀번호를 넣어준 적이 없으므로 MariaDB 서버에 그냥 접속되는 것이다.

- 그러므로 MariaDB 서버를 설치한 직후에는 데이터베이스 사용자 root의 비밀번호를 먼저 지정하여 데이터베이스 보안의 기본을 지켜야 한다. 지금은 DBMS에 데이터를 입력한 적이 없으므로 별 문제가 없지만, 실무에서 이를 무시하면 추후에 아주 치명적인 보안 문제가 발생할 수도 있다.



### 실습 2

MariaDB의 기본적인 보안 환경을 설정하자. 이번에는 Windows에서 리눅스의 MariaDB 서버에 접속해서 실습하자.

#### step 1

<code>Server</code> 보안에 중요한 데이터베이스 관리자 root의 비밀번호를 설정하자.

- <b>mysqladmin -u root password '1234'</b> 명령을 입력해 데이터베이스 관리자 root의 비밀번호를 1234로 변경하자.

![image8](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image8.png)

- 이제 외부에서 접속할 때는 mysql 명령을 입력해서 접속할 수 없다. <b>mysql -h localhost -u root -p</b>명령을 입력해 MariaDB 서버에 접속한 후, 비밀번호를 별도로 입력해야 한다. 접속이 되었으면 <b>exit</b>로 종료하자.

> MariaDB 10.8의 경우 설치된 컴퓨터에서 로그인한 운영체제의 관리자(root)는 비밀번호 없이 접속을 허용한다. 즉 Linux에서 root 사용자로 로그인했다면 mysql 명령만으로도 접속이 가능하다. 이전 버전인 10.3에서는 현재 로그인한 운영체제 사용자가 누구든 비밀번호를 입력해야 했다.

![image9](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image9.png)

#### step 2

<code>WinClient</code> 또는 호스트 운영체제 꼭 MariaDB 서버가 설치된 컴퓨터에서만 MariaDB 클라이언트를 사용하는 것은 아니다. 당연히 다른 컴퓨터에서도 MariaDB 서버에 접속할 수 있어야 한다. 이번에는 Windows에서 Server에 설치된 MariaDB 서버에 접속해보자.

- MariaDB 서버에 접속하려면 MariaDB 클라이언트가 필요하다. 웹 브라우저를 실행하고 http://www.mariadb.org/ 에 접속한 후 \<실습 1\>의 과정을 참고해서 Windows용 MariaDB 10.8.x 클라이언트를 다운로드하여 설치하자.

> 리눅스용은 서버와 클라이언트 프로그램을 별도로 제공하지만, Windows용은 1개 파일에 서버와 클라이언트가 모두 포함되어 있으므로 설치 중간에 필요한 내용을 선택해서 설치해야 한다.

- 다운로드한 파일로 설치를 시작한다. 처음에 환영 메시지가 나오면 \<Next\>를 클릭한다.

- 라이선스 관련 내용이 나오면 [I accept the terms ……]에 체크하고 \<Next\>를 클릭한다. 
- [Custom Setup]이 나오면 [Database instance] 앞에 있는 디스크 모양의 아이콘을 클릭해서 [Entire feature will be unavailable]을 선택하여 설치되지 않게 설정한다. 같은 방식으로 [Development Components]와 [Third party tools]도 설치되지 않게 설정한다. 최종적으로는 다음과과 같이 [Client Programs]만 설치되도록 설정하고 \<Next\>를 클릭한다.

![image10](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image10.png)

- [Ready to install MariaDB 10.8]에서 \<Install\>을 클릭하고 설치를 시작한다. 설치가 완료되면 \<Finish\>를 클릭한다.

#### step 3

<code>WinClient 또는 호스트 운영체제</code> Windows에서 리눅스의 MariaDB 서버로 접속해보자.

- [Windows + R]을 누르고 cmd 명령을 입력해서 명령 프롬프트를 실행한 다음, MariaDB 클라이언트가 설치된 C:\Program Files\MariaDB 10.8\bin\ 또는 C:\Program Files (x86)\MariaDB 10.8\bin\으로 이동하고, mysql 명령을 입력한다. 접속이 안 될 것이다.

- 접속이 안 되는 이유를 파악해보자. mysql 클라이언트 명령은 아무런 옵션 없이 실행할 경우, 현재 클라이언트 프로그램이 설치된 컴퓨터에 MariaDB 서버가 설치되어 있을 것이라고 생각하고 접속한다. 지금은 WinClient(또는 호스트 운영체제)에 MariaDB 클라이언트만 설치했을 뿐, MariaDB 서버는 설치하지 않았으므로 접속할 MariaDB 서버가 없는 것이다.
 
- 이제 Server (10.0.2.100)에 접속하도록 지정하자. <b>mysql -h 호스트이름또는 IP주소 -u 사용자이름 -p</b> 명령을 입력해 접속하자.

![image11](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image11.png)

- 비밀번호까지 입력하는 부분이 나와서 이번 실습에서 설정한 데이터베이스 사용자 root 의 비밀번호 1234를 정확히 넣었다. 그런데도 접속이 되지 않았다.
- 여기서 MariaDB가 관리하는 사용자의 개념이 하나 더 나온다. MariaDB는 이메일 주소와 비슷한 형식으로 사용자 이름을 사용한다. 즉 '사용자이름@호스트이름또는IP주소' 형식으로 사용자를 관리한다. 그래서 MariaDB 서버에서 비밀번호를 1234로 지정한 데이터베이스 사용자 root의 정식 이름은 'root@localhost'였던 것이다.
- 원칙적으로 MariaDB 서버에 접속하는 MariaDB의 클라이언트 명령은 <b>mysql -h 서버호스트이름또는 IP주소 -u 사용자이름 -p</b> 명령을 실행해 접속해야 한다. 그러면 내부적으로 사용자 이름에 '사용자이름@현재컴퓨터 IP'를 붙여서 접속하게 된다.
- 다시 Windows에서 접속할 때 입력한 명령인 <b>mysql -h 10.0.2.100 -u root -p</b> 명령을 살펴보자. 일단 Server IP의 컴퓨터에 MariaDB 서버가 설치되어 있으므로 사용자 인증만 받으면 접속이 승인된다. 그런데 문제는 Windows에서 입력한 root 사용자의 정식 이름이 root@WindowsIP주소다. 필자의 경우 root@10.0.2.5이 되는 것이다. MariaDB 서버에 접속이 허용된 DB 사용자는 root@localhost(또는 root@127.0.0.1) 만 있을 뿐 root@10.0.2.5 라는 사용자는 존재하지 않으므로 접속이 거부된 것이다.

> MariaDB 서버에 접속하는 것이 좀 까다롭게 느껴질 수도 있지만, 이는 보안을 위해 꼭 필요한 부분이다. 즉, 데이터베이스 사용자 이름과 비밀번호만 안다고 아무 컴퓨터에서나 접속할 수 없게 설정하는 것이다. MariaDB 서버에 접속하려면 접속하는 컴퓨터까지 지정해놓은 곳에서만 접속해야 한다.

#### step 4

- <code>Server</code> 사용자 개념을 파악했으므로 WinClient에서 접속할 사용자를 생성하자. MariaDB 서버 관리자인 root와 혼동되므로 Windows 사용자는 winuser로 생성하자.

- 먼저 MariaDB의 사용자가 들어 있는 user 테이블을 확인하자. 터미널에서 <b>mysql -u root -p</b> 명령을 입력해 MariaDB 서버에 접속한다. 접속 후 다음 SQL문을 입력해 mysql 데이터베이스에 있는 'user' 테이블을 조회해보자.

```
USE mysql;
SELECT user, host FROM user WHERE user NOT LIKE '';  -> 사용자 이름이 비어 있는 것은 제외
```

![image12](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image12.png)

-  mysql 데이터베이스에 있는 user 테이블의 user 열과 host 열을 조회한 결과다. 현재 MariaDB 서버를 사용할 수 있는 mysql 및 root라는 이름의 사용자가 있는데 정식 이름은 mysql@localhost, root@localhost다. 즉, 현재 컴퓨터에서 접속할 경우에만 데이터베이스 사용자 root로 접속할 수 있는 것이다.

- WinClient의 정확한 IP 주소만으로 사용자를 생성할 수 있다. 필 WinClient의 IP 주소가 192.168.111.137이므로 사용자이름@10.0.2.5 사용자를 생성하면 된다. 그런데 WinClient는 동적 IP 주소를 사용하기 때문에 재부팅할 때마다 IP 주소가 바뀔 수 있으므로 문제가 발생한다. 이를 해결하려면 10.0.2.000으로 시작하는 IP 주소 모두가 접속할 수 있게 사용자를 생성하면 된다. <b>GRANTALL ON \*.\* TO winuser@'10.0.2.%' IDENTIFIED BY '4321';</b> 구문을 입력한다.

![image13](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image13.png)

- 네 번째 주소인 000 부분에 %를 썼다는 것을 주의해서 살펴보자.
- 사용자를 생성하고 확인해보니 winuser@10.0.2.% 이름의 사용자가 생성된 것을 알 수 있다. 이제 10.0.2.000 IP 주소의 컴퓨터는 모두 winuser로 암호 4321 을 사용하면 접속할 수 있다.

#### GRANT 구문
- GRANT는 사용자를 생성해주는 SQL문이다. 형식은 다음과 같다.

```
GRANT 사용권한 ON 데이터베이스이름.테이블이름 TO 사용자이름@'호스트이름' IDENTIFIED BY '비밀번호';
```


- 사용권한을 ALL PRIVILIEGES 또는 ALL로 설정하면 모든 권한을 다 준다는 의미다. 권한의 일부만 주려면 SELECT, INSERT, UPDATE, DELETE 등의 권한을 별도로 줄 수 있다.

- '데이터베이스이름.테이블이름'을 \*.\*로 설정하면 모든 데이터베이스와 모든 테이블에 접근이 가능하다는 의미다. 만약 mysql 데이터베이스의 user 테이블만 사용할 수 있게 허락하려면 mysql.user라고 설정하면 된다.

- 즉, 입력한 GRANT ALL ON \*.\* TO winuser@‘10.0.2.%' IDENTIFIED BY '4321';구문을 해석하면 다음과 같다.

- '사용자 winuser@10.0.2.%의 비밀번호를 4321로 새로 생성하라. 그리고 모든 데이터베이스와 테이블에 모든 권한을 행사할 수 있도록 하라.'

#### step 5

- <code>WinClient 또는 호스트 운영체제</code> 명령 프롬프트에서 다시 <b>mysql -h 10.0.2.100 -u winuser -p명령</b>을 입력해 winuser 사용자로 접속해보자. 바로 앞에서 winuser 사용자의 비밀번호는 4321로 지정해줬다.


![image14](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image14.png)

- 정상적으로 접속된다. 이제 Server에서든 WinClient에서든 똑같이 MariaDB 서버에 접속해서 사용할 수있다.

## MariaDB 데이터베이스 생성과 운영
- 다음 실습은 Server에 접속해 진행하자

### 실습 3 

쇼핑몰의 데이터베이스를 MariaDB 서버에 구축하자. 

#### step 0
 
 ```
 mysql -h 10.0.2.100 -u winuser -p4321   -> p 뒤에 암호를 붙여 써야 한다.
 ```

![image15](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image15.png)

#### step 1

<code>WinClient 또는 호스트 운영체제</code>

- <b>CREATE DATABASE shopping_db CHARACTER SET utf8;</b> 구문을 입력해 쇼핑몰의 데이터베이스에 해당하는 shopping_db를 생성하고 <b>SHOW DATABASES;</b> 구문을 입력해 잘 생성되었는지 확인한다.

> 데이터베이스 생성 시 <b>'CHARACTER SET utf8'</b> 옵션을 지정하면 한글 입출력이 문제없이 잘 되지만, MariaDB 버전에 따라서 생략해도 별 문제가 없기도 한다.

![image16](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image16.png)

> <b>데이터베이스가 저장되는 디렉터리</b><br><br><b>SHOW DATABASES</b> 구문을 실행했을 때 보이는 데이터베이스의 실체는 운영체제 입장에서 디렉터리일 뿐이다. 그리고 내부에 정의된 테이블은 파일 형태를 갖는다. 위치는 /var/lib/mysql/ 이다.<br>SHOW DATABASES 구문을 실행해서 출력된 mysql. shopping_db, test 등의 데이터베이스가 디렉터리 형태로 존재한다는 것을 확인할 수 있다.

- shopping_db 데이터베이스 안에 customer (고객 정보) 테이블과 purchase (구매 정보) 테이블을 생성한다.

```
USE shopping_db;
CREATE TABLE customer (
	id VARCHAR(10) NOT NULL PRIMARY KEY,
	name VARCHAR(5), 
	age INT,
	address VARCHAR(5));

CREATE TABLE purchase (
	no INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	cust_id VARCHAR(10),
	date CHAR(8),
	product VARCHAR(5));
```

![image17](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image17.png)

> 테이블 생성 시 사용한 예약어의 의미는 다음과 같다.<br>- NOT NULL: Null 값을 허용하지 않는다.<br>- PRIMARY KEY : 해당 필드를 주 키로 지정한다.<br>- AUTO_INCREMENT : 별도의 값을 입력하지 않고, 자동으로 입력 값이 증가하는 필드로 만든다.

- <b>DESC customer;</b> 구문과 <b>DESC purchase;</b> 구분을 차례로 입력해 생성한 두 테이블의 구조를 확인해보자.

![image18](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image18.png)

- 다음 SQL문을 참고해 테이블에 레코드를 입력한다. customer 테이블에는 4개행, purchase 테이블에는 5개 행을 입력한다.

```sql
INSERT INTO customer VALUES ('hong', '홍길동', 22, '경기');
INSERT INTO customer VALUES ('dang', '당탕이', 23, '충북');
INSERT INTO customer VALUES ('ppuni', '이뿌니', 30, '서울');
INSERT INTO customer VALUES ('john', '존밴이', 28, '강원');
INSERT INTO purchase VALUES (null, 'hong', '20160122', 'TV');
INSERT INTO purchase VALUES (null, 'ppuni', '20160211', 'TV');
INSERT INTO purchase VALUES (null, 'john', '20160211', '냉장고');
INSERT INTO purchase VALUES (null, 'hong', '20160222', '세탁기');
INSERT INTO purchase VALUES (null, 'john', '20160311', '비디오');
```

> purchase 테이블의 no(일련번호) 필드는 auto_increment 옵션을 설정해 자동으로 증가하게 했다. 그러므로 행을 삽입할 때 no 필드 부분은 null 값으로 입력하는 것이다. 그러면 알아서 1,2,3, .…으로 자동 증가하며 값이 입력된다.

- <b>SELECT \* FROM customer;</b> 구문과 <b>SELECT \* FROM purchase;</b> 구문을 입력해 데이터를 확인해본다.
- <b>exit</b> 구문을 입력해 종료한다.

* * * 
# Oracle Database Express 설치와 운영

- DBMS 중에서 가장 많이 사용되는 Oracle을 CentOS에 설치해보자. 그리고 설치한 Oracle을 활용하는 환경도 알아보자.

> Oracle을 구동하려면 높은 사양의 컴퓨터가 필요하다. 특히 Oracle Database Enterprise/Standard는 최소 2GB의 메모리 용량이 필요하다. 지금 우리가 사용할 Oracle Database Express 11g 512MB 메모리에서 잘 작동하기 때문에 VirtualBox상에서 큰 문제없이 구동할 수 있다. 또, 아무런 비용도 지불할 필요 없이 무료로 사용할 수 있다(상용 Oracle은 상당히 고가다).<br>기본적인 사용법은 모든 Oracle이 비슷하므로 무료이며 비교적 저사양에서도 잘 작동하는 Oracle Database Express11g로 사용법을 익히자.

## Oracle Database Express 11g 설치

### 실습 4

Server에 리눅스용 Oracle Database Express 11g를 설치하자.

#### step 0

- Server를 처음 설치 상태로 초기화하자.
- 아직 부팅하지 말고 Memory를 2GB (=2048MB)로 올리자.
- 부팅하고 root 사용자로 접속한다. 
- 터미널을 열고 <b>dnf -y install libnst</b> 명령으로 관련 패키지를 설치해놓자.


#### step 1

오라클사(http://www.oracle.co.kr) 에서 Oracle Database Express 11g를 다운로드하자.

- 웹 브라우저로 https://www.oracle.com/database/technologies/xe-prior-releases-downloads.html 에 접속해서 [Oracle Database 11gR2 Express Edition for Linux x64]를 클릭한다.
- 다운로드 페이지에 접속하면 [Accept License Agreement]를 클릭하고 [Oracle Database Express Edition 11g Release 2 for Linux x64]를 클릭해 다운로드하자. 다운로드한 파일 이름은 oracle-xe11.2.0-1.0.x86_64.rpm.zip이며 약 301MB 정도다.
- Oracle을 다운로드하려면 오라클사에 회원으로 가입되어 있어야 한다. 가입은 무료이므로 회원으로 가입한 적이 없다면 가입하자. 회원의 사용자 이름은 가입 시 등록한 이메일 주소를 사용하면 된다.

![image19](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image19.png)

- 터미널에서 다운로드한 파일을 확인하고 <b>unzip oracle\*</b> 명령을 입력해 압축을 풀자. 압축을 푼 다음에는 다시 Disk1 디렉터리로 이동한 후 rpm 파일이 존재하는지 확인한다.

![image20](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image20.png)

#### step 2

Oracle Database Express 11g를 설치한다.

- <b>dnf-y install oracle</b> 명령을 입력해 Oracle Database Express 11g를 설치하자.

![image21](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image21.png)

- 설치가 완료되면 <b>service oracle-xe configure</b> 명령을 입력해 환경 설정을 시작한다. 대부분 [Enter] 누르면 되며, 비밀번호 입력 부분에서만 비밀번호를 지정하면 된다(편의를 위해 password로 입력한다). 완료되는데 시간이 좀 걸린다.

```
Specify the HTTP --- Application Express [8080]: [Enter]     -> 웹 접속 포트 번호
Specify the port  --- database listener [1521] : [Enter]    -> SQL*Plus 접속 포트 번호
Specify password -- initial configuration: 암호 입력 후 [Enter]
      -> SYS 및 SYSTEM 사용자의 비밀번호를 지정하는 것이며, 입력되는 글자가 보이지 않는다.
confirm password: 한 번 더 입력 후 [Enter]
Do you want --- boot (y/n) [y]: [Enter]
     -> 자동으로 시작되도록 설정(몇 분간 시간이 걸림)
```

![image22](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image22.png)

- <b>systemctl restart/enable/status oracle-xe</b> 명령을 입력해 서비스 시작/상시 가동/상태 확인을 하자.

![image23](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image23.png)

- Oracle 환경을 설정하는 스크립트를 실행하자.

```
. /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh     -> 제일 앞에 '.'과 공백이 있다.
```

![image24](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image24.png)

- gedit으로 /etc/bashrc 파일을 열고 재부팅한 후에도 계속 설정이 적용되도록 제일 아래에 . /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh' 를 추가로 입력한 후 저장하고 닫는다.

![image25](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image25.png)

#### step 3

- Oracle을 사용하기 위한 포트를 열자.
- 다음 명령으로 Oracle과 관련된 8080 및 1521 포트를 열어주자.

```
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --permanent --add-port=1521/tcp
firewall-cmd --reload
```

![image26](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image26.png)

#### step 4

- 웹에서 Oracle에 접속해보자.
- 웹 브라우저에서 http://10.0.2.100:8080/apex 또는 http://127.0.0.1:8080/apex라는 주소를 입력해 접속하자. [Workspace]에는 internal을, [Username]에는 admin을, [Password]에는 설치 시 지정한 비밀번호를 입력하고 \<Login\>을 클릭하자.

![image27](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image27.png)

- ADMIN 사용자의 비밀번호를 바꾸라는 메시지가 나오면 [Enter Current Password]에는 기존 비밀번호를 넣고, [Enter New Password]와 [Confirm New Password]에는 새로 설정할 비밀번호를 넣은다음 \<Apply Changes\>를 클릭하자 (굳이 바꾸지 않아도 되므로 모두 password로 입력했다).

- 비밀번호가 바뀌었다는 메시지 화면이 나오면 \<Return\>을 클릭하고 다시 접속 화면이 나오면 'internal/ADMIN/비밀번호'를 차례로 입력한 후 \<Login\>을 클릭하자. 
- Oracle 관리 화면이 나온다. 이 화면에서 Oracle의 대부분을 관리할 수 있다.

![image28](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image28.png)

- 설치와 가동을 확인했으니 웹 브라우저를 닫는다.

##  Oracle에서 데이터베이스 구축
- 지난 실습에서 MariaDB에서 데이터베이스를 구축해보았다. 이번에는 Oracle에서 동일한 데이터베이스를 구축해보자. 일부 과정을 제외하고는 MariaDB와 별 차이가 없음을 느낄것이다.

> 최신 버전의 Oracle은 웹 환경을 잘 지원하지만, 이전 버전의 Oracle을 사용할 때는 대부분 텍스트 환경에서만 사용했다. 또 Oracle 개발자들도 텍스트 환경에서의 사용을 더 선호하는 경향이 있다. 텍스트 환경의 Oracle 클라이언트는SQL\*Plus를 주로 사용한다.

### 실습 5

Oracle에 쇼핑몰에서 사용할 데이터베이스를 구축하자.

#### step 0

\<실습 4\>에 이어서 진행한다.

#### step 1

- 이제는 Oracle 클라이언트 프로그램인 SQL\*Plus로 Oracle 서버에 접속해서  동일한 데이터베이스를 구축하자.
- \<실습 3\>에서 mysql을 이용해 구축했던 과정과 비교해보자. 상당히 유사할 것이다.
- 먼저 데이터 파일을 저장할 /oradata 디렉터리를 만들고, 누구나 읽기/쓰기가 가능하게 설정하자.

![image29](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image29.png)

#### step 2

- 터미널에서 <b>sqlplus</b> 명령을 입력하고, system 사용자(필비밀번호를 password로 설정했다)로 접속하자. 그러면 프롬프트가 SQL\>로 변경될 것이다(이것은 MariaDB의 [MariaDB [none]\>] 프롬프트와 동일한 상태다)

- <b>CREATE TABLESPACE shopping_db DATAFILE '/oradata/shop.dbf' SIZE 5M;</b> 구문을 입력해 쇼핑몰의 데이터베이스인 shopping_db를 생성하고, <b>SELECT tablespace_name FROM DBA_DATA_FILES;</b> 구문을 입력해 데이터베이스가 잘 생성되었는지 확인한다(Oracle의 테이블스페이스(tablespace)는 MariaDB의 데이터베이스와 비슷한 개념이라고 보면 된다).

![image30](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image30.png)

- 다음 SQL문을 입력해 테이블을 생성하자.

```SQL
CREATE TABLE customer (
	id  VARCHAR(10)  NOT  NULL   PRIMARY   KEY,
	name  NCHAR(5),
	age  INT,
	address  NCHAR(5) )  TABLESPACE   shopping_db;
	
CREATE TABLE purchase (
	no  INT  NOT  NULL   PRIMARY   KEY,
	cust_id  VARCHAR(10),
	mdate  CHAR(8),
	product  NCHAR(5) ) TABLESPACE   shopping_db;
```

#### MariaDB와 Oracle의 차이점은 다음과 같다.

- 테이블 생성 구문 뒤에 테이블이 생성될 테이블스페이스를 지정한다.
- 한글이 들어갈 문자형은 NCHAR를 사용한다.
- purchase 테이블의 date 열 이름은 예약어로 인식되지
- AUTO_INCREMENT는 인식하지 않으므로 생략했다.

![image31](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image31.png)

![image32](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image32.png)

- <b>DESC customer;</b> 구문과 <b>DESC purchase;</b> 구문을 차례로 입력해 정의한 두 테이블의 구조를 확인해보자.

![image33](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/6~7%EC%9D%BC%EC%B0%A8(6h)%20-%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%EC%84%9C%EB%B2%84/images/image33.png)

- <b>INSERT INTO customer VALUES ('hong', '홍길동', 22, '경기' );</b> 구문과 <b>INSERT INTO purchase VALUES (1, 'hong', '20160122', 'TV');</b> 구분을 차례로 입력해 customer 테이블과 purchase 테이블에 데이터를 입력하자. MariaDB와 달리 purchase 테이블의 no 일에는 직접 숫자를 입력한다.

> 터미널에서 한글 깨짐 등의 문제로 입력이 잘 안 된다면 gedit을 실행해서 SQL문을 입력하고 터미널에 복사/붙여넣기 방식을 사용해보자.

- <b>SELECT \* FROM customer;</b> 구문과 <b>SELECT FROM purchase;</b> 구문을 입력하여 테이블에 삽입한 데이터를 확인한다.

