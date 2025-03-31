# recent-java

## 레벨 1: 기초 다지기 - 쓰레드 & 동기화 기본 개념 이해 
### 프로세스 (Process) vs. 쓰레드 (Thread) 개념 명확히 이해
> * 프로세스와 쓰레드의 정의, 차이점 (자원 공유 방식 등)
> * 자바에서 쓰레드를 생성하고 실행하는 기본적인 방법 (Thread 클래스 상속, Runnable 인터페이스 구현)
> * 쓰레드 생명 주기 (Life Cycle: NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED)

### 동시성 (Concurrency) vs. 병렬성 (Parallelism) 개념 구분
> * 동시성과 병렬성의 정의, 차이점 (논리적 동시 실행 vs. 물리적 동시 실행)
> * 멀티 코어 프로세서 환경에서의 동시성/병렬성

### 공유 자원 (Shared Resource) 문제점 인식
> * 여러 쓰레드가 공유 자원에 동시에 접근할 때 발생할 수 있는 문제점 (경쟁 상태 Race Condition, 데이터 불일치 등)
> * 임계 영역 (Critical Section) 개념 이해

### 동기화 (Synchronization) 기본
> * synchronized 키워드: 메서드 동기화, 블록 동기화 사용법 및 원리
> * volatile 키워드: 가시성 (Visibility) 문제 해결, 원자성 (Atomicity) 보장 X
> * wait(), notify(), notifyAll(): 쓰레드 간 협력 (wait-notify 메커니즘), Object 클래스 메서드

---

## 레벨 2: 중급 - java.util.concurrent 패키지 활용
### Executor Framework (ExecutorService, Executors)
> * ExecutorService 인터페이스 역할 및 주요 메서드 (submit(), shutdown(), awaitTermination())
> * Executors 팩토리 클래스: newFixedThreadPool(), newCachedThreadPool(), newSingleThreadExecutor(), newScheduledThreadPool() 등 다양한 쓰레드 풀 생성 및 특징 이해
> * 쓰레드 풀의 장점 (쓰레드 재사용, 효율적인 자원 관리)

### Callable & Future
> * Runnable 과의 차이점 (결과 반환 O, 예외 던지기 O)
> * Future 인터페이스: 비동기 작업 결과 얻기 (get()), 작업 상태 확인 (isDone(), isCancelled()), 작업 취소 (cancel())
> * Future.get() 메서드의 블로킹 동작 및 타임아웃 설정

### 동기화 도구 (Synchronization Utilities):
> * Locks (ReentrantLock, ReadWriteLock): synchronized 보다 유연한 락 제어 (tryLock, 인터럽트 가능한 락, 공정성 설정, 읽기/쓰기 락 분리)
> * Condition: Lock 과 함께 사용하는 쓰레드 간 협력 도구 (await(), signal(), signalAll()), wait/notify 와 비교
> * Semaphore: 공유 자원에 대한 동시 접근 쓰레드 수 제어
> * CountDownLatch: 특정 수의 이벤트가 완료될 때까지 대기
> * CyclicBarrier: 여러 쓰레드가 특정 지점에서 모두 만날 때까지 대기
> * Phaser: CountDownLatch 와 CyclicBarrier 의 기능을 합친 유연한 동기화 도구

### 동시성 컬렉션 (Concurrent Collections):
> * ConcurrentHashMap: 쓰레드 안전한 고성능 해시 맵
> * CopyOnWriteArrayList, CopyOnWriteArraySet: 읽기 작업은 빠르고, 쓰기 작업 시 복사본을 생성하여 동기화하는 리스트/셋
> * BlockingQueue (ArrayBlockingQueue, LinkedBlockingQueue, SynchronousQueue 등): 생산자-소비자 패턴 구현에 유용한 쓰레드 안전 큐

---

## 레벨 3: 고급 - 동시성 문제 심층 이해 & 고급 기법
### 데드락 (Deadlock) & 라이브락 (Livelock) & 기아 상태 (Starvation)
> * 각 문제의 발생 조건, 원인, 예방 및 해결 방법
> * 쓰레드 덤프 (Thread Dump) 분석을 통한 데드락 진단

### 메모리 모델 (Java Memory Model, JMM)
> * happens-before 관계 이해: 메모리 가시성 보장 원리
> * volatile, final, synchronized 키워드가 JMM 에 미치는 영향

### 원자성 변수 (Atomic Variables - java.util.concurrent.atomic)
> * AtomicInteger, AtomicLong, AtomicBoolean, AtomicReference 등
> * CAS (Compare-And-Swap) 알고리즘 기반의 락 없는 (Lock-free) 동시성 처리
> * synchronized 와 비교 시 성능 이점

### Fork/Join Framework (자바 7)
> * 분할 정복 (Divide and Conquer) 알고리즘 병렬 처리
> * ForkJoinPool, RecursiveTask, RecursiveAction
> * 작업 훔치기 (Work Stealing) 알고리즘

### CompletableFuture (자바 8)
> * Future 의 한계를 개선한 비동기 프로그래밍 API
> * 논블로킹 방식의 비동기 작업 조합 (chaining), 예외 처리, 콜백 등록
> * 함수형 프로그래밍 스타일 접목

### Reactive Streams & Reactive Programming (Project Reactor, RxJava)
> * Non-blocking, Asynchronous, Backpressure 기반의 데이터 스트림 처리 패러다임
> * 고성능, 고응답성, 탄력적인 시스템 구축
> * (심화 내용이지만, 현대적인 동시성 프로그래밍 트렌드를 이해하는 데 중요)

---

## 레벨 4: 실전 & 최신 기술 - 가상 스레드 & 성능 튜닝
### 가상 스레드 (Virtual Threads - 자바 21)
> * 경량 쓰레드 개념, 플랫폼 쓰레드와의 차이점
> * 블로킹 I/O 작업의 효율적인 처리
> * 기존 동기 코드 스타일 유지하면서 높은 동시성 달성
> * ExecutorService 와의 관계 및 활용법

### 동시성 프로그래밍 성능 튜닝 (Performance Tuning)
> * 프로파일링 도구 (JProfiler, YourKit 등) 사용법
> * 쓰레드 덤프, 힙 덤프 분석
> * GC (Garbage Collection) 튜닝과 동시성
> * 락 경합 (Lock Contention) 분석 및 최적화
> * 동시성 디자인 패턴 (Concurrency Design Patterns) 활용

---