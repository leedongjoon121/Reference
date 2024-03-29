# Context Switching

멀티프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할때, 기존의 프로세스의 상태 또는 레지스터 값(Context)을 저장하고 CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터 값(Context)를 교체하는 작업

- 멀티프로세싱을 하기 위해 CPU를 나눠서 써야할때, Context를 교체하는 것이다.

### Context Swich를 하는 주체 = OS 

### Context
사용자와 다른 사용자, 사용자와 시스템 or 디바이스간의 상호작용에 영향을 미치는 사람, 장소, 개체 등의 현재 상황(상태)을 규정하는 정보

CPU가 해당 프로세스를 실행하기 위한 해당 프로세스의 정보들 이며, 이 Context는 프로세스의 PCB(Process Control Block)에 저장됨

그래서 Context Switching때 PCB의 정보를 읽어(적재) CPU가 프로세스가 이전에 하던 일을 이어서 수행하는 것이 가능

### PCB (Process Control Block) 저장 정보
- 프로세스 상태 : 생성, 준비, 수행, 대기, 중지
- 프로그램 카운터 : 프로세스가 다음에 실행할 명령어 주소
- 레지스터 : 누산기, 스택, 색인 레지스터
- 프로세스 번호

### 참고사항 : Context Switching때 해당 CPU는 아무런 일을 하지 못한다. 따라서 컨텍스트 스위칭이 잦아지면 오히려 오버헤드가 발생해 효율(성능)이 떨어짐


### 인터럽트 (Interrupt)
인터럽트는 CPU가 프로그램을 실행하고 있을 때 실행중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우 CPU에게 알려 예외 사항을 처리할 수 있도록 하는 것

대표적인 인터럽트에 의한 Context Switching
1. I/O request (입출력 요청시)
2. Time slice expired (CPU 사용 시간이 만료)
3. Fork a child (자식 프로세스를 만들 때)
4. Wait for an intterupt (인터럽트 처리를 기다릴 때)

... 생략 

### 우선순위는 해당 OS의 스케줄러가 우선순위 알고리즘에 의해 정해지고 수행하게 되어있다.
- 라운드 로빈 스케줄링은 시분할 시스템을 위해 설계된 선점형 스케줄링


