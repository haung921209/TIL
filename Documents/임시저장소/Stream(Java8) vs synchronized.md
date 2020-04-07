멀티코어 CPU의 각 코어는 별도의 캐시를 포함하고 있다. 락을 사용하면 이러한 캐시가 동기화 되어야하므로 속도가 느린 캐시일관성 프로토콜 인터코어 통신(cache-coherency-protocol intercore communication)이 이루어진다. 따라서 synchronized의 속도가 더 느리게 된다.

