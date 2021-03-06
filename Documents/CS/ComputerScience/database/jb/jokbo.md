1.	다음을 간단히 설명하시오


(가)	Manual navigation vs automatic navigation (05, 07)



A.	Automatic navigation이란 navigation process가 사용자 요청을 만족하기 위해 저장된 데이터에 대해 자동적으로 수행된다는 것을 말하는 것이다. 이와 반대로, manual navigation이란, navigation process가 사용자가 명시한 모든 절차에 의해 이루어진다는 것이다. 예를 들어 relation system에서 사용자는 간단한 SQL문을 사용하여 원하는 데이터를 찾아낼 수 있지만, nonrelation system에서 사용자는 복잡한 프로그래밍 등을 통해 원하는 데이터를 찾아야 한다.



(나)	Serializability (05)



A.	동시에 수행되는(concurrent execution) 트랜잭션들은 그 트랜잭션들이 어떠한 순서대로 한번에 하나씩 수행된 결과와 같은 결과를 내도록 보장되어야 한다. 이렇게 직렬적으로 수행되는 결과와 같은 결과를 내는 것을 serializability라고 한다.



(다)	Total vs partial constraints(ERD) (05)



A.	Completeness constraint란, higher-level entity set에 있는 entity가 generalization하에서 적어도 하나 이상의 lower-level entity set에 존재하는지 안하는지를 명시하는 것이다.\

B.	Total constraints : 한 entity는 lower-level entity set중 하나에 반드시 속해야 한다.

C.	Partial constraints : 한 entity는 lower-level entity set중 하나에 속할 필요는 없다.



(라)	RESTRICT vs CASCADE (DROP TABLE) (05)



A.	
테이블을 삭제하는 sql문은 DROP이며, 사용법은 다음과 같다.


~~~

DROP TABLE <base table name> <behavior>;

~~~

여기에서 <behavior>는 RESTRICT 혹은 CASCADE가 될 수 있다.
RESTRICT는 현재 그 table이 사용 중이라면, DROP이 취소되는 것을 의미한다.
CASCADE는 DROP명령이 항상 성공적으로 수행되고, 해당 table을 사용 중인 모든 것들도 DROP됨을 의미한다.



(마) logical data independence vs. physical data independence (06, 08)



A.  logical data independence - 새로운 entity, attribute, relationship들의 추가나 삭제와 같은 conceptual schema에서의 수정이 있더라도 external schema와 application progtram의 수정을 필요로 하지 않음을 의미 한다.
    Physical data independence - 다른 파일 편성(file organization)이나 파일 구조(file structure)를 사용하거나, 다른 저장 장치를 사용하는 경우, 그리고 index나 hash 알고리즘을 수정하는 경우와 같은 internal schema의 수정을 할 때 conceptual schema나 external schema의 수정이 필요 없음을 의미한다.



(바) ODBC (06)


A.  Open Database Cnnnecxtivity
    application program과 DBMS를 연결하는 표준 API(Application Program Interface)
    ODBC는 operating system, database system에 대해 독립적이다. 즉, ODBC에 의해 작성된 application은 ODBC driver만 바꾸는 작업만으로 다른 operating system이나 database system을 넘나들 수 있다.


(사) total participation of ERD (06)


A.  entity set에 있는 모든 entity들이 임의의 relationship set의 적어도 하나 이상의 relationship에 가담(participate)하는 경우를 말한다. 이것은 ERD에서 두 줄(double line)로 표현한다.
    예를 들어, 아래의 ERD의 경우 entity set 'loan'의 모든 entity들을 'customer'와 'borrower' 라는 relationship을 가져야 한다. 이때 'borrower'와 'loan'은 total participation 관계이다.
    
    
    
![dbjokbo2006_no1_3rd](https://user-images.githubusercontent.com/14533484/56468879-3f6f9180-646d-11e9-8bb0-118f736819d9.png)




(아) primary key of weak entity (06)


A. weak entity set에는 primary key가 없다. 때문에 weak entity가 종속된 strong entity의 primary key와 weak entity set의 discriminators(partial key)의 결합으로 대신한다. 



(자) downsizing (06)


A.  client/server computing에서 platform에 맞게 새롭게 application을 설계해야 한다.
    host-based application의 경우 더 작은 환경이나 LAN기반의 환경에 재설계 될 경우 downsizing이 필요하다.


(차) type vs relation (07, 08)

A. 

- 타입은 우리가 이야기 하고자 하는 것이고, 관계는 우리가 이야기 하고자 하는 것에 관한 것에 관해 말하는 것이다.
- 타입은 고용인 번호와 이름, 부서 번호 그리고 봉급. 관계는 "특정 고용인 번호를 가진 고용인은 특정 이름을 가지고 특정 부서에서 일하며, 특정 봉급을 벌어들인다."라는 형태의 사실적인 표현.
- 타입과 관계는 둘 다 필요하다. / 타입과 관계는 필요할 뿐 아니라, 충분하다 / 타입과 관계는 같은 것이 아니다.



(카) disjoint vs overlapping constraints (07)

A.  Disjoint : ERD에서 entity가 단 하나의 lower - level entity set에만 포함될 수 있는 것.
    Overlapping : ERD에서 entity가 여러 lower - level entity set에 포함될 수 있는 것.ㅓ


(타) foreign key (08)

A1. 어떠한 relvar R2의 속성들의 value가 또 다른 relvar R1의 후보키들의 value와 match가 될 때, 이를 foreign key라 부른다.

A2. EMP table의 DEPT# value는 모든 employee가 department에 할당되어 있음을 보이기 위하여, table DEPTa안에 DEPT#의 값이 반드시 존재하여야 한다. 이렇게, table DEPT의 primary키를 참조(reference)한, table EMP안의 column DEPT#를 foreign key라고 한다.


(파) bill - of - material relationship (08)

A. 다이어그램에서는, 한 종류의 entity type만을 포함하는 relationship이 존재한다. bill-of-material relationship은 어떠한 entity type이 다른 entity type을 구성요소로서 포함하고 있는 관계이며 일종의 unary relationship관계 혹은 특별한 경우의 binary relationship이다.









---




2.	DBA의 주요 역할을 5가지만 설명하라.(05)



    - 데이터베이스의 개념 스키마를 정의
    - 내부 스키마 정의
    - 사용자와의 연락
    - 보안 검사와 무결성 검사 정의
    - 덤프(dump, 메모리의 내용을 복사하는 것)와 재 적재(reload)정책 정의
    - 변화하는 요구에 대한 적응과 성능 향상에 대한 감시.




2-1. 데이터베이스에서 데이터에 대한 3단계 뷰를 유지하는 근본적인 목적을 설명하고, 이것에 기초하여 특정 레코드의 검색과정을 단계별로 기술하라. (06)

A.  

(1) 3단계 뷰를 유지하는 목적 - 3단계 뷰를 유지하는 근본적인 목적은 data의 독립성을 유지하기 위한 것이다. conceptual scheme를 효율성과 응용 데이터 요구사항에 관계없이 상대적으로 안정된 것으로 유지함으로써 사용자가 보는 view와 data가 저장되는 방법 간의 flexibility와 adaptablity를 높인다. 검색 과정은 다음과 같다.


(2) 레코드 검색과정 - 우선 사용자가 external level에서 특정 레코드를 검색하기 위해 질의를 하면 External/Conceptual mapping을 통해 conceptual level의 질의로 변형되고, 다시 Conceptual / Internal mapping을 통해 internal level의 질의로 변형되게 된다. internal level에소ㅓ는 질의에 대한 정보를 찾게 되고 이 정보를 다시 Conceptual/ Internal mapping을 통해 conceptual level에서의 scheme로 변경하게 되고 conceptual level에서는 이 정보를 External/Conceptual mapping을 통해 External level의 형태로 변경하여 사용자에게 질의에 대한 결과가 보여지게 된다.


---



3. 카타로그가 자술적(self-describing)이란 것은 무엇을 의미하는가? 다음의 질의는 무엇을 의미하는가? (06)


![dbjokbo2006_no3_1](https://user-images.githubusercontent.com/14533484/56469014-ec96d980-646e-11e9-8ab4-8850121088ef.png)



A.  카탈로그 릴레이션 변수 자체를 기술하는 엔트리를 포함하는 것. 즉, 카탈로그 안에 카탈로그 자신에 대한 정보도 포함됨을 의미한다.
    위의 질의는 TABLES와 COLUMS를 JOIN한 후 COLCOUNT의 값이 3 미만인 table record를 가져와 그 중에 TABNAME과 COLNAME을 출력하라는 질의이다.




3-1. 뷰와 기본 릴레이션의 차이점을 기술하고, 뷰에 대한 질의처리 과정을 설명하라. (08)

A. 

(1) 기본 릴레이션은 각기 **고유명**이 있고, DB에 **독립적**으로 존재한다. 뷰는 **기본 릴레이션에서 유도된** 또 하나의 릴레이션이다. 뷰는 독립적으로 존재하는 것이 아니고 **가상**으로 존재한다.

(2) 뷰의 질의 처리 과정

- 뷰의 정의 sql이 시스템 카탈로그에 저장된다.
- 실체적 질의 sql문에서 참조된 뷰명은 시스템에서 시스템 카탈로그에 저장된 정의로 치환된다.
- 최적화 과정을 거쳐서 변환된다.

ex)

i) s라는 기본 릴레이션이 있을 때 아래와 같이 GOOD_SUPPLIER라는 뷰를 정의할 수 있다.

~~~
CREATE VIEW GOOD_SUPPLIER AS
SELeCT S#, STSTUS, CITY FROM S WHERE STSTUS >20;
~~~

아래와 같은 표현식은 시스템이 다음과 같이 수정한다.

~~~
SELECT S# STSTUS FROM GOOD_SUPPLIER WHERE CITY = "SEOUL";
~~~

ii) 수정

~~~
(SELECT S#, STSTUS FROM (SELECT S#, STSTUS, CITY FROM S WHERE STSTUS>20) WHERE CITY = "SEOUL";)

~~~

iii) 이것은 다시 다음과 같이 최적화(단순화)되어 처리된다.

(SELECT S#, STATUS FROM S WHeRE STATUS > 20 AND CITY = "SEOUL";)




---



4.	Aggregation 개념을 정의하고 이 개념이 유용한 예를 두 가지만 설명하라.(05)




(1) Aggregation의 개념

관계들 간의 관계를 표현하기 위해 관계를 사위 개채로 취급하는 추상화 기법이다.

(2) Aggregation이 유용한 예

"어떤 직원이 어떤 지사에서 수행한 일을 관리하는 관리자를 기록하고자 한다"면 다음과 같은 4항 관계를 생각할 수 있다.



![dbjokbo2005_no4_1](https://user-images.githubusercontent.com/14533484/56466765-d7ab4d80-6450-11e9-8cca-4d0b6e94b828.png)



그러나 i) 관계 manages에 있는 모든 개체 employee, branch, job 조합은 관계 works-on에도 있으므로 위의 ERD는 과다한 정보가 들어있다. 또한 ii) 관계 works-on 과 manages는 하나의 관계 집합으로 결합될 수 있는 것처럼 보이지만 employee, branch, job 조합은 관리자를 갖지 않기 때문에 두 관계를 결합될 수 없다.

따라서 aggregation을 적용하면 위의 두가지 단점을 해결할 수 있다. 다음 그림은 aggregation을 적용한 ERD를 나타낸다.


![dbjokbo2005_no4_2](https://user-images.githubusercontent.com/14533484/56466768-e134b580-6450-11e9-8713-c4358f819af1.png)



---



5. 다음의 내용을 반영한 어떤 회사(company)의 데이터베이스를 위한 ERD를 작성하시오. 회사 데이터베이스는 고용인(employer), 부서(department)와 프로젝트(project)에 대한 내용만을 포함한다. (05, 06, 08)


(가) 회사는 여러 부서(department)들로 구성되어 있고, 각 부서는 유일한 이름(name)과 번호(number), 그리고 위치를 가지며 부서를 관리하는 한 고용인이 있다. 이 고용인이 부서를 관리하기 시작했을 때(start data)에 대한 정보를 유지한다.

(나) 한 부서는 여러개의 프로젝트(project)를 제어(control)하며, 각각의 프로젝트는 유일한 이름, 번호와 위치(location)을 가진다.

(다) 각 고용인(employee)의 이름, 주민등록번호, 주소, 봉급(salary), 성별과 생일에 대한 정보를 유지한다. 고용인은 하나의 부서에 속하지만 같은 부서에서 의해서 제어되지 않은 여러개의 프로젝트에서 일할 수 있다. 각 고용인의 직속 상사(direct supervisor)정보를 유지한다.

(라) 보험 목적을 위하여 각 고용인의 부양가족(dependent)에 대한 정보를 유지한다. 각 부양가족의 이름, 성별, 출생일과 고용인과의 관계(relationship)를 유지한다




![dbjokbo2005_no5_1](https://user-images.githubusercontent.com/14533484/56466974-0d9e0100-6454-11e9-8f0a-89dceb5278e0.png)


5-1. 데이터 모델의 구성요소를 설명하고, 다음 4가지 모델을 비교 설명하여라. (06)

가) 관계형 모델
나) 계층적 모델
다) 네트워크 모델
라) 개체 / 관계성 (Entity / Relationship) 모델

A. 데이터 모델의 구성요소는 구조(structure), 조작(manipulation), 무결성(Integrity)이다. 구조는 데이터가 표현되는 형태를 말하고, 조작은 해당 모델에서 어떠한 연산자들을 통해 데이터가 관리되는가에 대한 것이다. 마지막으로 무결성은 해당 모델에 의해 표현된 데이터들이 어떻게 무결성 제약을 포함하는가에 대한 것이다.

가) 관계형 모델
    a) 구조적 관점 : 데이터베이스에서 데이터는 사용자에게 테이블의 형태로 인식된다.
    b) 조작적 관점 : 사용자 수준의 연산자는 주어진 예전의 테이블로부터 새로운 테이블을 유도하는 연산자들로써 최소한 SELECT(RESTRICT), PROJECT, JOIN 연산자를 제공한다.
    c) 무결성 관점 : 테이블들은 참조 무결성 등의 무결성 제약을 포함한다.
    
나) 계층적 모델
    a) 구조적 관점 : 데이터들은 사용자에게 트리의 형태(세그먼트, 링크)의 계층 구조로 인식된다.
    b) 조작적 관점 : 최소한 데이터의 탐색에 필요한 연산자를 제공한다.
    c) 무결성 관점 : 데이터들은 부모 / 자식 관계가 링크에 의해 명시적으로 표현되므로 부모 / 자식간의 무결성 제약을 포함한다.

다) 네트워크 모델
    a) 구조적 관점 : 데이터들은 사용자에게 그래프 기반의 네트워크 형태로 인식된다.
    b) 조작적 관점 : 최소한의 데이터 검색에 대한 연산자를 제공한다.
    c) 무결성 관점 : 명시적 링크를 이용하여 오너(Owner) / 멤버(Member)관계를 표현하기 때문에 오너와 멤버 사이의 무결성 제약을 포함한다.

라) 개체 / 관계성 (Entity / Relationship) 모델
    a) 구조적 관점 : 데이터는 유형, 무형의 객체(object)로써의 개체와 개체 집합고ㅓㅏ 개체 집합 간의 여러 유형의 관계를 나타내는 관계성(relationship)으로 인식된다.
    b) 조작적 관점 : 검색 / 갱신에 대한 연산자를 제공한다.
    c) 무결성 관점 : 개체 간의 관계성을 통해 개체 간에 지켜져야 할 무결성 제약이 포함된다.
    
    


---


6. 클라이언트-데이터베이스 서버 구조를 설명하고 이것이 갖는 장점을 기술하시오. 일반적인 Two-tier 클라이언트 / 서버 구조에서 발생하는 문제점을 기술하고, Three - tier 구조에서 이러한 문제들의 처리과정을 설명하라. 특히 웹 환경에 적합한 구조를 기술하고 그 이유를 설명하라. (05, 06, 07)


(1) client-database server architecture 설명 : 사용자와 상호작용하고, 데이터에 대한 요청을 생성하는 Client application단과 그 요청을 처리하고 답장하고, 컨트롤하고, 보안과 권한 조정을 제공하고, 저장공간을 제공하는 서버단을 합쳐 Client-database server architecture라 합니다.

(2) client - database server architecture 장점 기술 : 


- 훨씬 효과적인 일의 분담을 제공한다
- job에 대한 horizontal, vertical scaling을 제공한다 (작업의 효율적인 분할 가능)
- application은 일반적으로 smaller client computer configuration으로 좋은 performance를 제공한다.
- user들은 자신의 client에서 사용해왔던 tool을 그대로 사용할 수 있다.
- client는 더 많은 data에 접근 가능하다
- valuable data의 손실이나 부적절한 access로부터 보호를 해준다.


(3) client - database server architecture 문제점 기술:

- 동시에 다수의 client가 server에 접속을 할 경우 서버에 부하가 생기며 시스템 전체에 정체 현상을 유발시킨다.
- fat client 문제 발생
- server로 사용되는  mainframe의 설치, 유지, 보수 비용이 크다.
- 개별 user의 독립성과 개인적인 system 사용이 어렵다
- security cost가 높아진다.


(4) Three - tier architecture에서 client - database server architecture의 문제점 처리과정 기술:

- application server를 여러개 배치하여 server의 load balancing이 쉬워진다.
- fat client의 임무를 application server에 두어 client를 가볍게 한다.
- application server의 설치, 유지, 보수 비용은 mainframe보다 저렴하기 때문에 incremental scale이 가능하다.
- application server의 적절한 변경을 통해 user의 요구 충족 기간이 2-tier보다 짧아진다.
- security를 위한 server를 따로 두어 관리한다.

(5) web환경에 적합한 구조 기술

- Tier 1(client) : user interface, perhaps performing some simple logic processing (e.g. input validation)
- Tier 2(application server) : business logic, data processing logic
- Tier 3(database server) : data validation, database access

(6) web환경에 적합한 구조의 이유 설명 :

- web환경에서 user는 헤아릴 수 없을 정도로 많기 때문에 기존의 2-tier 방식은 server에 상당한 부하를 주고 있다. 이에 비해 위에서 제안한 구조는 다음과 같은 장점이 있다.
- server의 기능이 대폭 줄어 비용감소 및 관리가 쉬워진다
- 많은 user에 대한 business logic을 하나의 application server에 중앙 집중화 함으로서 application의 중앙집중화를 유도한다. (S/W 분산에 대한 문제 제거)
- 하나의 tier가 다른 tier에 영향을 끼치지 않으면서 대체되거나 수정될 수 있다.
- core business를 database function으로부터 분리시킴으로써 load balancing을 구현하기 쉽다.
- 위의 장점들은 3 - tier가 web환경에 적합하다는 근거이다.


6-1. ERD에 적합한 릴레이션 스킴들을 만드는 경우를 고려한다. 다음 경우에 적합한 스킴들의 축소를 위한 방법을 기술하라. (07, 08)

![dbjokbo2007_no6_1](https://user-images.githubusercontent.com/14533484/56469932-f0c8f400-647a-11e9-8bcb-828acec3e1df.png)


A. 

- 개체 집합 A에서 개체 집합 B로 가는 다대 일 관계 집합 AB를 생각해 보자. 앞에서 소개된 테이블 생성 방안을 이용하면 A, B, BA의 3개의 테이블을 얻을 수 있다.  A는 관계 AB에 전체적으로 참가 한다고 가정하자. 즉 개체 집합 A의 모든 개체 a는 관계 AB에 참가해야 한다. 그러면 테이블 A와 테이블 AB를 조합하여 두 테이블의 열들의 합집합으로 구성되는 하나의 테이블을 만들 수 있다.
- 예를 들어 그림의 개체 - 관계 다이어그램을 생각해 보자. 개체 - 관계 다이어그램의 2중선은 account_branch에 account가 전체적으로 참가한다는 것을 가리킨다. 그러므로 어떤 계좌도 특정 지사와의 연관 없이 존재할 수 없다. 게다가 관계 집합 account_branch는 account로부터 branch로 다대일의 관계를 가진다. 그러므로 account_branch를 위한 테이블을 account를 위한 테이블과 결합시켜 다음의 2개의 테이블만 만들면 된다.


    ~~~
    account = (account_number, balance, branch_name)
    branch = (branch_name, branch_city, assets)    
    ~~~

6-2  weak entity set은 identifying entity set의 주 키 속성을 추가함으로써 strong entity set으로 만드는 것이 가능하다. 만약 그렇게 한다면 어떤 종류의 중복이 생기는지를 설명하라.

Ans.

Identifying entity set의 primary key가 explicit 하게 저장되면, weak - entity set을 strong entity set으로 만들 수 있다. 그런데 이 때 identifying relation의 attribute가 strong entity set의 attribute의 중복이 된다. 예제에서 loan_number가 payment에 저장되면 entity set payment schema에는 4개의 속성(loan_number, payment_number, payment_date, payment_amount)가 저장되는데, 이 때 loan_payment schema에 저장된 단 두가지 속성인 (loan_number, payment_number) attribute가 중복된다.


---


7. 온라인 서점을 모델링하는 ERD를 다음과 같이 가정한다.

![dbjokbo2007_no7_1](https://user-images.githubusercontent.com/14533484/56469928-e7d82280-647a-11e9-8bb7-eb798d988be6.png)


가) 개체 집합(entity set)들과 이들의 주 키(Primary key)들을 기술하라.
나) 서점이 음악 카세트들과 CD들을 취급 품목(collection)에 추가한다고 가정한다. 같은 음악을 카세트 또는 CD로 서로 다른 가격으로 표현할 수 있다. 이러한 추가사항을 모델링 하기 위해서 기존 ERD를 확장하라.(단 shopping basket(시장바구니)에 대한 효과는 무시한다.)
다) shopping basket이 책들, music cassette들, 또는 compact disk들의 임의의 결합을 포함할 수 있도록 하는 경우를 모델링 하기 위해서 generalization을 사용하여 ERD를 확장하라.


A. 온라인 서점을 모델링하는 ERD를 다음과 같이 가정한다.

가) 개체 집합(entity set) 들과 이들의 주 키(primary key)들을 기술하라.


![dbjokbo2007_no7_2](https://user-images.githubusercontent.com/14533484/56469925-e7d82280-647a-11e9-9b5f-f8907c1d0f70.png)

나) 서점이 음악 카세트들과 CD들을 취급 품목(collection)에 추가한다고 가정한다. 같은 음악(music item)을 cassette 또는 CD로 서로 다른 가격으로 표현할 ㅜㅅ 있다. 이러한 추가사항을 모델링 하기 위해서 기존 ERD를 확장하라.



![dbjokbo2007_no7_3](https://user-images.githubusercontent.com/14533484/56469926-e7d82280-647a-11e9-83b6-12b8e657451a.png)


다) shopping basket이 책들, music cassette들, 또는 compact disk들의 임의의 결합을 포함할 수 있도록 하는 경우를 모델링 하기 위해서 generalization을 사용하여 ERD를 확장하라.


![dbjokbo2007_no7_4](https://user-images.githubusercontent.com/14533484/56469927-e7d82280-647a-11e9-9f0f-89a293106453.png)





7-1. 다음의 관계형 스킴을 사용하여 답하라. 밑줄은 기본 키 속성을 의미한다 (06, 07)

~~~
    S(S#, SNAME, STATUS, CITY)
    P(P#, PNAME, COLOR, WEIGHT, CITY)
    SP(S#, P#, QTY)

~~~

가) 기본 릴레이션과 뷰의 차이점을 설명하시오 : 기본 릴레이션은 각기 고유명이 있고, DB에 독립적으로 존재한다. 뷰는 기본 릴레이션에서 유도된 또 하나의 릴레이션이다. 뷰는 독립적으로 존재하는 것이 아니고 가상으로 존재한다.

나) 다음의 뷰 정의를 가정한다

~~~
    CREATE VIEW GOOD_SUPPLIER AS
        SELECT S#, STATUS, CITY FROM S WHERE STATUS>20;
        
~~~

다음의 질의를 고려하자

~~~
SELECT S#, STATUS FROM GOOD_SUPPLIER WHERE CITY = "SEOUL"
~~~

이 질의가 원하는 것이 무엇인가? 이 질의를 DBMS가 처리하는 과정을 설명하라.

- 질의 : S 릴레이션에서 STATUS > 20 인 조건을 만족하는 S#, STATUS, CITY 속성들로 이루어진 뷰 GOOD_SUPPLIER 으로부터 CITY 명이 SEOUL 인 튜플들을 선택하여 속성값 S#과 STATUS로 이루어진 릴레이션을 구성한다.

- 처리과정 :

(1) 뷰의 정의 sql이 시스템 카탈로그에 저장된다.
(2) 실제적 질의 sql문에서 참조된 뷰명은 시스템에서 시스템 카탈로그에 저장된 정의로 치환된다.

~~~
    (SELECT S#, STATUS
     FROM ( SELECT S#, STATUS, CITY
            FROM S
            WHERE STATUS > 20)
    WHERE CITY = "SEOUL";)
~~~

(3) 최적화 과정을 거쳐서

~~~
    (SELECT S#, STATUS
     FROM S
     WHERE STATUS > 20 AND CITY = "SEOUL";)
~~~
    
    
    
와 같이 변환된다.








9. 다음 ERD 기호에 대한 적절한 설명을 기술하고 UML Class diagram notation으로 표시하라(05)



![dbjokbo2005_no9_1](https://user-images.githubusercontent.com/14533484/56467989-0cbf9c00-6461-11e9-9cb1-d7ddb7aa6462.png)

- 타원 : 속성

- 타원 안의 밑줄 : 주 키

- 사각형 : 개체 집합

- 마름모 : 관계 집합

- 이중선 : 개체 집합이 관계 집합에 전체적으로 참가함을 표시(즉, 개체 집합의 각 개체는 그 관계 집합의 적어도 한 관계에 나타난다)



ERD의 설명 : loan 개체는  borrower 관계 집합의 적어도 한 관계에 나타난다.



![dbjokbo2005_no9_2](https://user-images.githubusercontent.com/14533484/56467990-0d583280-6461-11e9-9a4d-d3a911a2d0ca.png)



