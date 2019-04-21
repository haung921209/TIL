1.	다음을 간단히 설명하시오


(가)	Manual navigation vs automatic navigation(05)



A.	Automatic navigation이란 navigation process가 사용자 요청을 만족하기 위해 저장된 데이터에 대해 자동적으로 수행된다는 것을 말하는 것이다. 이와 반대로, manual navigation이란, navigation process가 사용자가 명시한 모든 절차에 의해 이루어진다는 것이다. 예를 들어 relation system에서 사용자는 간단한 SQL문을 사용하여 원하는 데이터를 찾아낼 수 있지만, nonrelation system에서 사용자는 복잡한 프로그래밍 등을 통해 원하는 데이터를 찾아야 한다.



(나)	Serializability (05)



A.	동시에 수행되는(concurrent execution) 트랜잭션들은 그 트랜잭션들이 어떠한 순서대로 한번에 하나씩 수행된 결과와 같은 결과를 내도록 보장되어야 한다. 이렇게 직렬적으로 수행되는 결과와 같은 결과를 내는 것을 serializability라고 한다.



(다)	Total vs partial constraints(ERD) (05)



A.	Completeness constraint란, higher-level entity set에 있는 entity가 generalization하에서 적어도 하나 이상의 lower-level entity set에 존재하는지 안하는지를 명시하는 것이다.\

B.	Total constraints : 한 entity는 lower-level entity set중 하나에 반드시 속해야 한다.

C.	Partial constraints : 한 entity는 lower-level entity set중 하나에 속할 필요는 없다.



(라)	RESTRICT vs CASCADE (DROP TABLE) (05)



A.	테이블을 삭제하는 sql문은 DROP이며, 사용법은 다음과 같다.
    DROP TABLE <base table name> <behavior>;
    여기에서 <behavior>는 RESTRICT 혹은 CASCADE가 될 수 있다.
    RESTRICT는 현재 그 table이 사용 중이라면, DROP이 취소되는 것을 의미한다.
    CASCADE는 DROP명령이 항상 성공적으로 수행되고, 해당 table을 사용 중인 모든 것들도 DROP됨을 의미한다.



(마) logical data independence vs. physical data independence (06)



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



3. 카타로그가 자술적(self-describing)이란 것은 무엇을 의미하는가? 다음의 질의는 무엇을 의미하는가? (06)


![dbjokbo2006_no3_1](https://user-images.githubusercontent.com/14533484/56469014-ec96d980-646e-11e9-8ab4-8850121088ef.png)



A.  카탈로그 릴레이션 변수 자체를 기술하는 엔트리를 포함하는 것. 즉, 카탈로그 안에 카탈로그 자신에 대한 정보도 포함됨을 의미한다.
    위의 질의는 TABLES와 COLUMS를 JOIN한 후 COLCOUNT의 값이 3 미만인 table record를 가져와 그 중에 TABNAME과 COLNAME을 출력하라는 질의이다.




4.	Aggregation 개념을 정의하고 이 개념이 유용한 예를 두 가지만 설명하라.(05)




(1) Aggregation의 개념

관계들 간의 관계를 표현하기 위해 관계를 사위 개채로 취급하는 추상화 기법이다.

(2) Aggregation이 유용한 예

"어떤 직원이 어떤 지사에서 수행한 일을 관리하는 관리자를 기록하고자 한다"면 다음과 같은 4항 관계를 생각할 수 있다.



![dbjokbo2005_no4_1](https://user-images.githubusercontent.com/14533484/56466765-d7ab4d80-6450-11e9-8cca-4d0b6e94b828.png)



그러나 i) 관계 manages에 있는 모든 개체 employee, branch, job 조합은 관계 works-on에도 있으므로 위의 ERD는 과다한 정보가 들어있다. 또한 ii) 관계 works-on 과 manages는 하나의 관계 집합으로 결합될 수 있는 것처럼 보이지만 employee, branch, job 조합은 관리자를 갖지 않기 때문에 두 관계를 결합될 수 없다.

따라서 aggregation을 적용하면 위의 두가지 단점을 해결할 수 있다. 다음 그림은 aggregation을 적용한 ERD를 나타낸다.


![dbjokbo2005_no4_2](https://user-images.githubusercontent.com/14533484/56466768-e134b580-6450-11e9-8713-c4358f819af1.png)







5. 다음의 내용을 반영한 어떤 회사(company)의 데이터베이스를 위한 ERD를 작성하시오. 회사 데이터베이스는 고용인(employer), 부서(department)와 프로젝트(project)에 대한 내용만을 포함한다. (05, 06)


(가) 회사는 여러 부서(department)들로 구성되어 있고, 각 부서는 유일한 이름(name)과 번호(number), 그리고 위치를 가지며 부서를 관리하는 한 고용인이 있다. 이 고용인이 부서를 관리하기 시작했을 때(start data)에 대한 정보를 유지한다.

(나) 한 부서는 여러개의 프로젝트(project)를 제어(control)하며, 각각의 프로젝트는 유일한 이름, 번호와 위치(location)을 가진다.

(다) 각 고용인(employee)의 이름, 주민등록번호, 주소, 봉급(salary), 성별과 생일에 대한 정보를 유지한다. 고용인은 하나의 부서에 속하지만 같은 부서에서 의해서 제어되지 않은 여러개의 프로젝트에서 일할 수 있다. 각 고용인의 직속 상사(direct supervisor)정보를 유지한다.

(라) 보험 목적을 위하여 각 고용인의 부양가족(dependent)에 대한 정보를 유지한다. 각 부양가족의 이름, 성별, 출생일과 고용인과의 관계(relationship)를 유지한다




![dbjokbo2005_no5_1](https://user-images.githubusercontent.com/14533484/56466974-0d9e0100-6454-11e9-8f0a-89dceb5278e0.png)





6. 클라이언트-데이터베이스 서버 구조를 설명하고 이것이 갖는 장점을 기술하시오. 일반적인 Two-tier 클라이언트 / 서버 구조에서 발생하는 문제점을 기술하고, Three - tier 구조에서 이러한 문제들의 처리과정을 설명하라. 특히 웹 환경에 적합한 구조를 기술하고 그 이유를 설명하라. (05)


(1) client-database server architecture 설명

(2) client - database server architecture 장점 기술

(3) client - database server architecture 문제점 기술

(4) Three - tier architecture에서 client - database server architecture의 문제점 처리과정 기술

(5) web환경에 적합한 구조 기술

(6) web환경에 적합한 구조의 이유 설명






9. 다음 ERD 기호에 대한 적절한 설명을 기술하고 UML Class diagram notation으로 표시하라(05)



![dbjokbo2005_no9_1](https://user-images.githubusercontent.com/14533484/56467989-0cbf9c00-6461-11e9-9cb1-d7ddb7aa6462.png)

- 타원 : 속성

- 타원 안의 밑줄 : 주 키

- 사각형 : 개체 집합

- 마름모 : 관계 집합

- 이중선 : 개체 집합이 관계 집합에 전체적으로 참가함을 표시(즉, 개체 집합의 각 개체는 그 관계 집합의 적어도 한 관계에 나타난다)



ERD의 설명 : loan 개체는  borrower 관계 집합의 적어도 한 관계에 나타난다.




![dbjokbo2005_no9_2](https://user-images.githubusercontent.com/14533484/56467990-0d583280-6461-11e9-
9a4d-d3a911a2d0ca.png)








