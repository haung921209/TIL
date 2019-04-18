#Chap 2

###시스템 콜이란 무엇입니까?

시스템 콜이란 프로그래밍 언어에서 지원하지 않는 기능에 대하여 운영체제의 루틴을 호출하여 이용하는 것을 말합니다. 대개 모든 운영체제는 여러가지 low level의 연산을 수행하기 위한 루틴들의 모음을 가지고 있습니다. 예를 들어 모든 운영체제는 디렉토리를 만드는 루틴이라든가, 특정한 디렉토리에 있는 파일들의 목록을 읽어내는 루틴 등을 가지고 있습니다. 만약 응용프로그램에서 운영체제에 있는 루틴을 실행시켜 어떠한 결과를 얻기 원한다면, 시스템 호출을 이용하면 됩니다.

시스템 콜의 예시는 다음과 같습니다.

1. 프로세스 제어(Process Control)

- fork()
- exit()
- wait()

2. 파일 조작(File Manipulation)

- open()
- read()
- write()
- close()

3. 장치 조작(Device Manipulation)

- ioctl()
- read()
- write()

4. 정보 유지(Information Maintenance)

- getpid()
- alarm()
- sleep()

5. 통신(Communication)

- pipe()
- shm_open()
- mmap()

6. 보호(Protection)

- chmod()
- umask()
- chown()


인터럽트란 무엇입니까?
