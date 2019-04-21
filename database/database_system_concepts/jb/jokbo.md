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


4.	Aggregation 개념을 정의하고 이 개념이 유용한 예를 두 가지만 설명하라.


![figure1](img/db/dbjokbo2005_no4_1.png)


![figure2](./img/db/dbjokbo2005_no4_2.png)



