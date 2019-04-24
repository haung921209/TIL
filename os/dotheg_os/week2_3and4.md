# 프로세스 생명 주기 요점 정리

---



## 1. 프로세스란?



`process is a program in execution`




![pcb](https://user-images.githubusercontent.com/14533484/56672022-a355bc80-66f0-11e9-96cc-d753efac4108.png)


(1) state와 flag의 특징



<img width="609" alt="스크린샷 2019-04-25 오전 8 31 09" src="https://user-images.githubusercontent.com/14533484/56700302-86db7380-6734-11e9-9eac-f75c13bc8a6e.png">


state의 경우, volatile long 자료형으로 선언된 변수입니다. 이 volatile의 경우에는, 이 선언된 변수는 최적화에서 제외하여 항상 메모리에 접근하도록 하는 자료형입니다.

예를 들면


~~~c
while (i < 10)
    i++;
~~~

와 같이 표현한 것을 컴파일러는

~~~c
int i=10;
~~~

과 같이 최적화 해버립니다.(i에 그냥 10을 할당해버림.)

volatile로 선언한다는 이야기는, 반복할 때마다 항상 i의 메모리에 접근해야 하므로, 컴파일러가 while 반복문을 없애지 않는다는 이야기와도 같습니다. 메모리 관리 등을 위해서라도 state에 대한 정확한 정보는 중요하기 때문에, volatile로 선언하여 안정성을 챙기는 것입니다.



<img width="621" alt="스크린샷 2019-04-25 오전 8 31 14" src="https://user-images.githubusercontent.com/14533484/56700301-86db7380-6734-11e9-8d7e-47b70a2f870b.png">

0보다 큰 process의 state에 대해서도 다음과 같이 정리해두었습니다. 이는 우리가 흔히 아는 프로세스 상태도에서 각 상태간의 번호에 대해서 이야기 해주고 있습니다. 즉 PCB에서는 프로세스가 어떤 상태인지 효과적으로 알려주기 위해서 위와 같이 일정 변수의 값을 이용하여 보여주는 방식으로 사용하고 있습니다.








<img width="612" alt="스크린샷 2019-04-25 오전 8 42 37" src="https://user-images.githubusercontent.com/14533484/56700609-26e5cc80-6736-11e9-9df6-1247dc8e2ee3.png">


<img width="627" alt="스크린샷 2019-04-25 오전 8 42 46" src="https://user-images.githubusercontent.com/14533484/56700613-29482680-6736-11e9-9add-6e8fffce8484.png">
