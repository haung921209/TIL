# 프로세스 생명 주기 요점 정리

---



## 1. 프로세스란?



`process is a program in execution`




![pcb](https://user-images.githubusercontent.com/14533484/56672022-a355bc80-66f0-11e9-96cc-d753efac4108.png)


(1) state와 flag의 특징



<img width="609" alt="스크린샷 2019-04-25 오전 8 31 09" src="https://user-images.githubusercontent.com/14533484/56700302-86db7380-6734-11e9-9eac-f75c13bc8a6e.png">


<img width="621" alt="스크린샷 2019-04-25 오전 8 31 14" src="https://user-images.githubusercontent.com/14533484/56700301-86db7380-6734-11e9-8d7e-47b70a2f870b.png">


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

volatile로 선언한다는 이야기는, 반복할 때마다 항상 i의 메모리에 접근해야 하므로, 컴파일러가 while 반복문을 없애지 않는다는 이야기와도 같습니다.