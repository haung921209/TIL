3.1 short-term, medium-term, 그리고 long-term 스케쥴링의 차이점에 대해서 묘사하시오


- - -

3.2 프로세스 간의 context-switch시에 커널의 역할에 대해서 설명하시오


- - -

3.3 RPC 메커니즘을 고려합니다. "At most once"나 "Exactly once" 의미론을 시행하지 않을 때 발생할 수 있는 바람직하지 않은 상황을 기술합니다. 이러한 guarantee들 중 어느 것도 없는 메커니즘에 대해 가능한 사용을 설명하세요.

- - -

3.4 Figure 3.24에 있는 프로그램을 이용하여, Line A에 무엇이 output이 될지 설명하시오.

- - -

3.5 다음 각 항목의 장점과 단점은 무엇입니까? 시스템과 프로그래머 수준을 모두 고려해서 답변해주세요.

a. 대칭 및 비대칭 통신(Symmetric and asymmetric communication)
b. 자동 및 명시적 버퍼링(Automatic and explicit buffering)
c. 사본으로 보내기와 참조로 보내기(Send by copy and send by reference)
d. 고정크기 및 가변 크기 메세지

- - -

3.6 피보나치 순서는 숫자 0, 1, 1, 2, 3, 5, 8........의 수열이다. 형식적으로는 이렇게 표현될 수 있다 : 

```

fib0 = 0
fib1 = 1
fibn = fibn-1 + fibn-2

```

자식 프로세스에서 Fibonacci sequence를 생성하는 fork() system call을 사용하여 C 프로그램을 작성하시오. 시퀀스의 숫자는 command line에서 제공될 것입니다. 예를 들어, 만약 5가 주어졌다면, fibonacci sequence의 첫 다섯 숫자들이 자식 프로세스에 의해 결과물로 제출될 것입니다. 왜냐하면 부모와 자식 프로세스는 그들의 각각의 데이터의 복사본을 가지고 있기 때문이고, 자식 프로세스가 시퀸스를 출력할 필요가 있습니다. 프로그램을 종료하기 전에 부모가 wait() call을 호출하여 자식 프로세스가 완료될 때까지 기다리도록 하십시오. 필요한 error checking을 수행하여 명령줄에 음수가 아닌 숫자가 전달되는지 확인하십시오.


- - -

3.7 Win32 API의 CreateProcess()를 사용하여 이전 연습을 반복하십시오. 이 경우 CreateProcess()에서 호출할 별도의 프로그램을 지정하여야 합니다. 이는 분리된 프로그램인, 피보나치 수열을 출력하기 위한 child process로서 실행될 것입니다. 필요한 오류 검사를 수행하여 command line에 음수가 나오지 않도록 합니다.

- - -

3.8 그림 3.19에 표시된 날짜 서버를 현재 날짜가 아닌 임의의 한 줄의 운세를 전달하도록 수정합니다. 운세가 여러 줄 있게 합니다. 그림 3.20에 표시된 날짜 클라이언트는 운세 서버가 반환하는 다중 행 운세를 읽는 데 사용할 수 있다.

- - -

3.9 **echo server**란 client로부터 무언가를 받았을 때, 되받아 반응하는 서버입니다. 예를 들어, client가 _Hello there!_를 보냈을 때, 그 서버는 client로부터 받은 그것을 그대로 반응할 것입니다 - 그것은 바로, _Hello there!_

- - -

3.10 

- - -

