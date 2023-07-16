# CPU 스케줄러와 스케줄링 알고리즘


### CPU 스케줄러
#
장기스케줄러(Long-term scheduler or job scheduler)
* 메모리와 디스크 사이의 스케줄링을 담당.
* 프로세스에 memory(및 각종 리소스)를 할당(admit)
* degree of Multiprogramming 제어
(실행중인 프로세스의 수 제어)
* 프로세스의 상태
  * new -> ready(in memory)


단기스케줄러(Short-term scheduler or CPU scheduler)
* CPU 와 메모리 사이의 스케줄링을 담당.
* Ready Queue 에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.
* 프로세스에 CPU 를 할당(scheduler dispatch)
* 프로세스의 상태
  * ready -> running -> waiting -> ready

중기스케줄러(Medium-term scheduler or Swapper)
* 여유 공간 마련을 위해 프로세스를 메모리에서 디스크로 쫓아냄 (swapping)
* 프로세스에게서 memory 를 deallocate(할당 해제)
* degree of Multiprogramming 제어
* 현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러
* 프로세스의 상태
  * ready -> suspended

> 스와핑(swapping): 메모리의 관리를 위해 사용되는 기법. 표준 Swapping 방식으로는 round-robin 과 같은 스케줄링의 다중 프로그래밍 환경에서 CPU 할당 시간이 끝난 프로세스의 메모리를 보조 기억장치(e.g. 하드디스크)로 내보내고 다른 프로세스의 메모리를 불러 들일 수 있다.

<br>

## CPU 스케줄링 알고리즘
#

### FCFS(First Come First Served)
#
먼저 온 순서대로 처리
* 비선점형(Non-Preemptive) 스케줄링

문제점
* `convoy effect` (호위 효과)
  * 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생

<br>
<br>


### SJF(Shortest - Job - First)
#
다른 프로세스가 먼저 도착했어도 CPU burst time 이 짧은 프로세스에게 선 할당
* 비선점형(Non-Preemptive) 스케줄링

문제점
* `starvation`
  * 이 스케줄링은 극단적으로 CPU 사용이 짧은 job 을 선호한다. 그래서 사용 시간이 긴 프로세스는 거의 영원히 CPU 를 할당받을 수 없다.

<br>
<br>


### SRTF(Shortest Remaining Time First)
#
새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
* 선점형 (Preemptive) 스케줄링
* 현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.

문제점
* `starvation`(기아 상태)
* 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.

<br>
<br>


### Priority Scheduling
#
우선순위가 가장 높은 프로세스에게 CPU 를 할당하는 스케줄링이다. 우선순위란 정수로 표현하게 되고 작은 숫자가 우선순위가 높다.
* 선점형 스케줄링(Preemptive) 방식
  * 더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.
* 비선점형 스케줄링(Non-Preemptive) 방식
  * 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.

문제점
* `starvation`(기아 상태)
* 무기한 봉쇄(Indefinite blocking)
  * 실행 준비는 되어있으나 CPU 를 사용못하는 프로세스를 CPU 가 무기한 대기하는 상태

해결책
* `aging`
  * 아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여주자.

<br>
<br>

### Round Robin (라운드 로빈)
#
현대적인 CPU 스케줄링, 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 갖게 된다.
* 할당 시간이 지나면 프로세스는 선점당하고 ready queue 의 제일 뒤에 가서 다시 줄을 선다.
* RR은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적
RR이 가능한 이유는 프로세스의 context 를 save 할 수 있기 때문이다.

장점
* Response time이 빨라진다.
n 개의 프로세스가 ready queue 에 있고 할당시간이 q(time quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n 을 얻는다. 즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
* 프로세스가 기다리는 시간이 CPU 를 사용할 만큼 증가한다.
* 공정한 스케줄링이라고 할 수 있다.

주의할 점
* 설정한 time quantum이 너무 커지면 FCFS와 같아진다. 
* 또 너무 작아지면 스케줄링 알고리즘의 목적에는 이상적이지만 잦은 `문맥 교환(context switch)` 로 overhead 가 발생한다. 
* 그렇기 때문에 적당한 time quantum을 설정하는 것이 중요하다.
