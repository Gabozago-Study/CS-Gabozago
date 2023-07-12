# 운영체제

### OS 정의
: 응용 프로그램과 하드웨어 간의 인터페이스로써 사용자가 컴퓨터를 편리하고 효과적으로 사용할 수 있도록 환경을 제공하는 시스템 소프트웨어

### Program & Process & Thread
1. Program
    - 어떤 작업을 위해 실행될 수 있는 파일
2. Process
<img src="https://gmlwjd9405.github.io/images/os-process-and-thread/process.png" alt="process" width="100%">
    - 실행중인 프로그램
    - 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당
    - 최소 1개의 Thread(Main Thread 포함)를 보유
3. Thread
<img src="https://gmlwjd9405.github.io/images/os-process-and-thread/thread.png" alt="process" width="100%">
    - 프로세스 안에서 실행되는 여러 흐름 단위
    - 프로세스 내에서 각각 Stack만 따로 할당받고 Code, Data, Heap 영역은 공유
    - cf. Java-Thread: JVM에 의해 스케쥴되는 실행 단위 코드 블럭

### Multi-process & Multi-thread
1. Multi-process
    - 하나의 응용 프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리하도록 하는 것
    - 자원이 서로 다르게 할당되므로 작업이 독립적으로 수행되어 안정적이나
    - 작업량 많을수록 오버헤드 및 Context Switching으로 인한 성능 저하 우려
        - Context Switching: 멀티프로세스 환경에서 CPU가 어떤 프로세스를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때 Context(CPU가 해당 프로세스를 실행하기 위한 해당 프로세스의 정보들)를 교체하는 작업
    - 한 프로세스가 다른 프로세스와 통신하기 위해 IPC(Inter-process communication) 사용해야하므로 통신이 복잡함
2. Multi-thread
    - 하나의 응용 프로그램을 여러 개의 스레드로 구성하여 각 스레드가 하나의 작업을 처리하도록 하는 것
    - 자원이 Stack만 따로 할당받으므로 시스템의 자원과 처리 비용 감소하며,
    - 실행속도와 Context Switching이 빠름
    - 스레드 간의 자원(Code, Data, Heap)을 공유하고 있기 때문에 통신의 부담이 적어 응답 시간이 빠름
    - 자원을 공유하고 있으므로 동기화 문제가 발생할 수 있으며, 하나의 스레드의 오류로 전체 프로세스에 문제 발생

### 동기 & 비동기
1. 동기
    - 설계가 간단하고 직관적
    - 결과가 주어질 때까지 다른 작업을 수행하지 못함
2. 비동기
    - 동기보다 복잡
    - 어떤 작업이 진행 중일 때, 그 시간 동안 다른 작업을 할 수 있으므로 자원을 효율적으로 사용할 수 있음

### 멀티 쓰레드 환경에서의 주의사항
1. 동시성 문제
: 2 이상의 스레드가 동시에 같은 인스턴스의 필드 값을 변경하면서 발생하는 문제
2. 교착 상태
: 둘 이상의 프로세스들이 자원을 점유한 상태에서 서로 다른 프로세스가 점유하고 있는 자원을 요구하며 무한정 기다리는 상황
3. 해결방법
    - 상호 배제(Mutual Exclusion): Locking과 UnLocking를 통해 구현
    - 세마포어(Semaphore): 최대 허용치만큼 접근 요청을 가능하게 설정하여 0이 되면 대기하도록 설정
    - Monitor: synchronized를 통해 구현 

### 페이지 교체 알고리즘
: 운영체제에서 필요한 페이지가 주기억장치에 적재되지 않았을 시(= 페이징 부재) 어떤 페이지 프레임을 선택해 교체할 것인지 결정하는 방법

1. FIFO(first in first out)
: 가장 간단한 알고리즘, 메모리에 올라온 지 가장 오래된 페이지를 교체
2. 최적(Optimal)
: 앞으로 가장 오랫동안 사용되지 않을 페이지를 교체 - 구현 불가능
3. LRU(least-recently-used)
: 가장 오래 사용되지 않은 페이지를 교체
4. LFU(least-frequently-used)
: 참조 횟수가 가장 작은 페이지를 교체
5. MFU(most-frequently-used)
: 참조 횟수가 가장 많은 페이지를 교체
