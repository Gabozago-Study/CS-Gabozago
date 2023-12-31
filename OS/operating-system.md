# Operating System
<br>

### 운영체제 정의
#
* 하드웨어(CPU, 메모리, 디스크 등) 관리
* 응용 프로그램과 하드웨어 사이에서 인터페이스 역할을 하는 시스템 소프트웨어
  
  <br>

### 프로세스 vs 스레드
#
<img src="https://gmlwjd9405.github.io/images/os-process-and-thread/process.png" alt="process" width="100%">
<img src="https://gmlwjd9405.github.io/images/os-process-and-thread/thread.png" alt="process" width="100%">

프로세스
* 실행중인 프로그램으로 OS로부터 주소 공간, 파일, 메모리 등을 할당받아 실행, 코드/데이터/스택/힙 메모리 영역을 가짐

스레드
* 프로세스의 독립적인 실행 단위로 프로세스로부터 자원을 할당받아 실행, 프로세스의 코드/데이터/힙 메모리 영역을 공유하고 개별적인 스택을 가짐
* cf. Java-Thread: JVM에 의해 스케쥴되는 실행 단위 코드 블럭

> 스레드가 개별적인 스택을 가지는 이유?
> * 스택에는 함수 호출 시의 전달인자, 지역 변수, 되돌아갈 주소 등을 저장
> * 독립적인 스택을 갖는 것은 독립적인 함수 호출이 가능하고 독립적인 실행 흐름을 추가할 수 있다는 것을 의미

> 스레드가 PC 레지스터를 가지는 이유?
> * 스레드는 CPU를 할당/반납하고를 반복
> * 이전까지의 수행 내역을 기억하기 위해 독립적인 PC 사용

  <br>

### 프로세스 생성 과정
#
1. 프로세스 관리 정보를 갖는 PCB를 생성하고 프로그램의 코드를 읽어 들여 코드 영역을 메모리에 할당
2. 초기화된 전역 변수 및 static 변수인 데이터 영역을 메모리에 할당
3. 힙과 스택의 초기 메모리 주소를 초기화
4. Queue에서 프로세스가 등록되고 운영체제가 CPU를 할당하기를 대기

  <br>

### 프로세스 제어 블록(Process Control Block, PCB)
#
* 프로세스 관리 정보를 저장하는 커널의 자료구조 (Data 영역에 존재)
* 운영체제는 프로세스를 관리하기 위해 프로세스의 생성과 동시에 고유한 PCB 를 생성 
* Process 상태, PC(다음에 수행할 명령어의 주소), CPU 레지스터, CPU 스케줄링 정보, 메모리 관리 정보 등을 저장
* 문맥 교환 시에 진행 사항을 PCB에 저장하고 CPU 반환 -> CPU를 할당받으면 PCB에 저장되어 있는 내용을 불러와 이전에 종료되었던 시점부터 다시 수행
 
  <br>

### 문맥 교환 (Context Switching)
#
과정
  1. 실행 중이던 프로세스의 상태(문맥)를 PCB에 보관
  2. 새로운 프로세스의 PCB에서 문맥을 복원해 `레지스터`에 적재
  3. 새로운 프로세스 실행
* 프로세스 사이에서 CPU 제어권이 이동되는 것
* 실행 중이던 프로세스를 중단하고 다른 프로세스를 실행할 때 발생
* Context: CPU에서 프로세스 실행시 필요한 프로세스의 정보(각 프로세스의 PCB에 저장)
* 멀티 스레드에서는 문맥 교환 시 스택 영역을 제외한 모든 영역을 공유하기 때문에 문맥 교환 비용이 훨씬 적음
> 레지스터 (register) 
> * CPU 에서 처리할 명령어나 연산의 중간 결과값 등을 일시적으로 기억하는 임시 기억 장소
> * CPU 기억 장치들 중에서 속도가 가장 빨라 연산 속도를 향상하기 위해서 사용
> * 레지스터에 새로운 데이터가 전송되면, 기존에 있던 내용은 지워지고 새로운 내용만 기억

<br>

### 멀티 스레드 vs 멀티 프로세스
#
멀티 스레드
* 하나의 프로세스에 여러 스레드가 자원을 공유하며 작업을 나누어 하는 것
* 안전성 낮음: 하나의 스레드의 비정상적인 활동은 전체 스레드에 영향을 끼칠 수 있음
* 통신 비용 적음
    * 코드/데이터/힙 영역을 공유해 메모리를 적게 차지하고 공유 메모리가 없어도 통신 가능
* 문맥 교환 비용 적음
* 프로세스를 생성하여 자원을 할당하는 시스템 콜이 감소함으로서 자원을 효율적으로 관리
  
멀티 프로세스
* 여러 프로세서(CPU)가 여러 작업(Task)을 동시에 처리하는 것 (병렬 처리)
* 안전성: 하나의 프로세스가 죽더라도 다른 프로세스에는 영향을 끼치지 않고 정상적으로 수행
* 통신 비용/문맥 교환 비용이 큼
    * CPU는 한 번에 하나의 프로세스만 실행 가능 -> 여러 프로세스를 돌아가면서 실행
        * IPC (Inter Process Communication): 프로세스 간의 통신을 하는 것
            * 파일 공유, 커널 영역 이용(메시지 큐, 공유 메모리, 소켓 등)
* 많은 메모리 공간을 차지
 
  <br>

> ### 그래서 멀티 스레드 vs 멀티 프로세스 무엇이 더 나은가?
> * 멀티 스레드는 멀티 프로세스보다 적은 메모리 공간을 차지하고 문맥 전환이 빠르다는 장점이 있지만, 오류로 인해 하나의 스레드가 종료되면 전체 스레드가 종료될 수 있다는 점과 동기화 문제를 안고 있다. 
> * 반면 멀티 프로세스 방식은 하나의 프로세스가 죽더라도 다른 프로세스에는 영향을 끼치지 않고 정상적으로 수행된다는 장점이 있지만, 멀티 스레드보다 많은 메모리 공간과 CPU 시간을 차지한다는 단점이 존재한다. 
> 
> 이 두 가지는 동시에 여러 작업을 수행한다는 점에서 같지만 적용해야 하는 시스템에 따라 적합/부적합이 구분된다. 따라서 대상 시스템의 특징에 따라 적합한 동작 방식을 선택하고 적용해야 한다.

<br>

### 인터럽트
#
프로그램을 실행하는 도중에 예기치 않은 상황이 발생할 경우 현재 실행 중인 작업을 즉시 중단하고, 발생된 상황을 우선 처리한 후 실행 중이던 작업으로 복귀하여 계속 처리하는 것

<br>

### 병렬성과 동시성의 차이
#
* 병렬성: 멀티 코어에서의 멀티 스레드, 각 코어들의 스레드가 동시에 실행
* 동시성: 싱글 코어에서의 멀티 스레드, 여러 개의 스레드가 번갈아가며 실행

<br>

### Critical Section(공유 자원, 임계 영역)
#
* 동일한 자원에 동시에 접근하는 경우가 발생하는 코드 영역
* 접근 순서에 따라 실행 결과가 달라지는 구역

<br>

### 교착 상태 (Deadlock)
#
둘 이상의 프로세스/스레드가 자원을 점유한 상태에서 서로 다른 프로세스/스레드가 점유하고 있는 자원을 요구하며 무한정 기다리는 현상

발생 조건 -> 4가지 조건을 모두 만족해야 됨
* 상호 배제: 하나의 프로세스/스레드가 자원에 접근할 수 있음
* 비선점: 다른 프로세스/스레드의 자원을 뺏을 수 없음
* 점유와 대기: 자원을 가진 상태에서 다른 자원을 기다림
* 순환 대기: 순환 형태로 자원을 대기

해결 방법
* 모든 프로세스가 lock을 잡는 순서를 동일하게 코딩
* trylock을 활용하여 lock을 선점한 프로세스/스레드가 없을 때만 락을 얻으려고 시도하는 방법
* 예방: 4가지 조건 중 1개 이상이 만족하지 않도록 함
    * 상호 배제 부정: 여러 프로세스가 공유 자원을 사용하도록 함
    * 점유와 대기 부정: 프로세스가 실행되기 전 필요한 모든 자원을 할당
    * 비선점 부정: 자원을 점유 중인 프로세스가 다른 자원을 요구할 때, 점유 중인 자원을 반납하고 대기
    * 순환 대기 부정: 자원에 고유한 번호를 할당하고, 번호 순서대로 자원을 요구하도록 함
* 회피: 교착상태가 발생하지 않도록 알고리즘 작성
    * 은행원 알고리즘: 어떤 자원을 할당하기 전에 할당 후에도 안정 상태로 있을 수 있는지 검사 후 할당
* 회복: 교착 상태 발생 후, 해당 프로세스를 종료하거나 할당된 자원을 해제 또는 선점하여 해결
    * 선점할 경우, 기아 상태가 발생하지 않도록 해야 함
* 무시: 그냥 무시

<br>

### 기아 상태 (Starvation)
#
여러 프로세스가 부족한 자원을 점유하기 위해 경쟁할 때, 특정 프로세스에 영원히 자원 할당이 되지 않는 경우

해결 방법
* 프로세스의 우선 순위 변경
* 요청을 순서대로 처리하는 요청 큐 사용

<br>

### 가상 메모리
#
프로세스 전체가 메모리 내에 올라오지 않더라도 실행이 가능하도록 하는 기법
* 프로그램이 물리 메모리보다 커도 된다
* 실제 프로그램 전체를 적재하여 사용하지 않고 일부분만 적재하기 때문에 메모리 제약을 극복
* 메모리의 실제 주소를 사용하지 않으므로 보안 상의 장점이 존재

<br>

### Fragmentation(단편화)
#
프로세스들이 메모리에 적재되고 제거되는 일이 반복되다보면, 프로세스들이 차지하는 메모리 틈 사이에 사용 하지 못할 만큼의 작은 자유공간들이 늘어나게 되는데, 이것이 `단편화` 이다.
* 외부 단편화: 메모리 공간 중 사용하지 못하게 되는 일부분. 물리 메모리(RAM)에서 사이사이 남는 공간들을 모두 합치면 충분한 공간이 되는 부분들이 분산되어 있을때 발생한다고 볼 수 있다.
* 내부 단편화: 프로세스가 사용하는 메모리 공간 에 포함된 남는 부분. 예를들어 메모리 분할 자유 공간이 10,000B 있고 Process A 가 9,998B 사용하게되면 2B 라는 차이 가 존재하고, 이 현상을 내부 단편화라 칭한다.

<br>

### Paging(페이징)
#
메모리에 불연속적으로 할당하는 방법 중 하나로 프로세스를 일정 크기인 `페이지`로 잘라서 가상 메모리에 적재하고 페이지 테이블을 이용하여 `프레임`으로 변환하여 가상 메모리를 관리하는 기법
현대 운영체제에서 사용되는 메모리 할당 기법
* 내부 단편화가 발생할 수 있음
> 페이지: 가상 메모리를 최소 단위로 쪼개어 만든 일정한 크기의 블럭

> 프레임: 물리 메모리에 페이지 크기와 같은 블럭으로 나눈 블럭


<br>

### Segmentation(세그멘테이션)
#
메모리에 불연속적으로 할당하는 방법 중 하나로 프로세스를 서로 다른 크기의 논리적 단위인 `세그먼트`로 나누어 메모리에 배치하는 것
* 메모리를 세그먼트로 나누고 세그먼트 테이블에 각 세그먼트의 시작(base) 주소와 크기(limit) 정보를 운용하여 가상 메모리를 관리하는 기법
* 외부 단편화가 발생할 수 있음

<br>
<br>

## 페이지 교체 알고리즘
### FIFO 페이지 교체
#
가장 간단한 페이지 교체 알고리즘으로 FIFO(first-in first-out)의 흐름을 가진다.
* 먼저 물리 메모리에 들어온 페이지 순서대로 페이지 교체 시점에 먼저 나가게 된다는 것이다.
* 오래된 페이지도 필요한 정보를 포함하고 있을 수 있기 때문에 오래된 페이지라는 이유 만으로 필요한 정보가 쉽게 사라지는 부작용을 초래할 수 있다.(초기 변수 등)
* 처음부터 활발하게 사용되는 페이지를 교체해서 페이지 부재율을 높이는 부작용을 초래할 수 있다.
> Belady의 모순: 페이지를 저장할 수 있는 페이지 프레임의 갯수를 늘려도 되려 페이지 부재가 더 많이 발생하는 모순이 존재한다.

<br>
<br>


### 최적 페이지 교체(Optimal Page Replacement)
#
가장 오랫동안 사용되지 않을 페이지를 찾아 교체하는 것이다.
* 주로 비교 연구 목적을 위해 사용한다.
* 알고리즘 중 가장 낮은 페이지 부재율을 보장한다.
* 구현의 어려움이 있다. 모든 프로세스의 메모리 참조의 계획을 미리 파악할 방법이 없기 때문이다.
  
<br>
<br>


### LRU 페이지 교체(LRU Page Replacement)
#
LRU: Least-Recently-Used
* 최적 알고리즘의 근사 알고리즘으로, 가장 오랫동안 사용되지 않은 페이지를 선택하여 교체한다.

<br>
<br>


### LFU 페이지 교체(LFU Page Replacement)
#
LFU: Least Frequently Used
* 참조 횟수가 가장 적은 페이지를 교체하는 방법이다. 
* 활발하게 사용되는 페이지는 참조 횟수가 많아질 거라는 가정에서 만들어진 알고리즘이다.
* 어떤 프로세스가 특정 페이지를 집중적으로 사용하다, 다른 기능을 사용하게되면 더 이상 사용하지 않아도 계속 메모리에 머물게 되어 초기 가정에 어긋나는 시점이 발생할 수 있다

<br>
<br>


### MFU 페이지 교체(MFU Page Replacement)
#
MFU: Most Frequently Used
* 참조 회수가 가장 작은 페이지가 최근에 메모리에 올라왔고, 앞으로 계속 사용될 것이라는 가정에 기반한다.

