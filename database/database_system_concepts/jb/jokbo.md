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


2.	DBA의 주요 역할을 5가지만 설명하라.(05)

    - 데이터베이스의 개념 스키마를 정의
    - 내부 스키마 정의
    - 사용자와의 연락
    - 보안 검사와 무결성 검사 정의
    - 덤프(dump, 메모리의 내용을 복사하는 것)와 재 적재(reload)정책 정의
    - 변화하는 요구에 대한 적응과 성능 향상에 대한 감시.





3.	ㅇㅇㅇ


4.	Aggregation 개념을 정의하고 이 개념이 유용한 예를 두 가지만 설명하라.(05)


(1) Aggregation의 개념

관계들 간의 관계를 표현하기 위해 관계를 사위 개채로 취급하는 추상화 기법이다.

(2) Aggregation이 유용한 예

"어떤 직원이 어떤 지사에서 수행한 일을 관리하는 관리자를 기록하고자 한다"면 다음과 같은 4항 관계를 생각할 수 있다.



![dbjokbo2005_no4_1](https://user-images.githubusercontent.com/14533484/56466765-d7ab4d80-6450-11e9-8cca-4d0b6e94b828.png)

그러나 i) 관계 manages에 있는 모든 개체 employee, branch, job 조합은 관계 works-on에도 있으므로 위의 ERD는 과다한 정보가 들어있다. 또한 ii) 관계 works-on 과 manages는 하나의 관계 집합으로 결합될 수 있는 것처럼 보이지만 employee, branch, job 조합은 관리자를 갖지 않기 때문에 두 관계를 결합될 수 없다.

따라서 aggregation을 적용하면 위의 두가지 단점을 해결할 수 있다. 다음 그림은 aggregation을 적용한 ERD를 나타낸다.


![dbjokbo2005_no4_2](https://user-images.githubusercontent.com/14533484/56466768-e134b580-6450-11e9-8713-c4358f819af1.png)







5. 다음의 내용을 반영한 어떤 회사(company)의 데이터베이스를 위한 ERD를 작성하시오. 회사 데이터베이스는 고용인(employer), 부서(department)와 프로젝트(project)에 대한 내용만을 포함한다. (05)

(가) 회사는 여러 부서(department)들로 구성되어 있고, 각 부서는 유일한 이름(name)과 번호(number), 그리고 위치를 가지며 부서를 관리하는 한 고용인이 있다. 이 고용인이 부서를 관리하기 시작했을 때(start data)에 대한 정보를 유지한다.
(나) 한 부서는 여러개의 프로젝트(project)를 제어(control)하며, 각각의 프로젝트는 유일한 이름, 번호와 위치(location)을 가진다.
(다) 각 고용인(employee)의 이름, 주민등록번호, 주소, 봉급(salary), 성별과 생일에 대한 정보를 유지한다. 고용인은 하나의 부서에 속하지만 같은 부서에서 의해서 제어되지 않은 여러개의 프로젝트에서 일할 수 있다. 각 고용인의 직속 상사(direct supervisor)정보를 유지한다.
(라) 보험 목적을 위하여 각 고용인의 부양가족(dependent)에 대한 정보를 유지한다. 각 부양가족의 이름, 성별, 출생일과 고용인과의 관계(relationship)를 유지한다


![dbjokbo2005_no5_1](https://user-images.githubusercontent.com/14533484/56466974-0d9e0100-6454-11e9-8f0a-89dceb5278e0.png)

6. 





