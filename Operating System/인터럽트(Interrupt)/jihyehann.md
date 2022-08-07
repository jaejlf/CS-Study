## 💡 정의

프로그램을 실행하는 도중에 예기치 않은 상황이 발생할 경우 현재 실행 중인 작업을 즉시 중단하고, 발생된 상황에 대한 우선 처리가 필요함을 CPU에게 알리는 것을 말한다.

<br/>

### 하드웨어 인터럽트

CPU 외부로부터의 인터럽트 요구 신호에 의해 발생되는 인터럽트를 말한다.

#### 종류

- 입출력 인터럽트 (I/O interrupt): 입출력 작업의 종료나 입출력 오류에 의해 CPU의 기능이 요청된다.
- 정전,전원 이상 인터럽트(Power fail interrupt): 전원 공급의 이상
- 기계 착오 인터럽트(Machine check interrupt): CPU의 기능적인 오류
- 외부 신호 인터럽트(External interrupt): I/O 장치가 아닌 오퍼레이터나 타이머에 의해 의도적으로 프로그램이 중단된 경우

<br/>

### 소프트웨어 인터럽트

CPU 내부에서 실행한 명령이나 CPU의 명령 실행에 관련된 모듈이 변화하는 경우에 발생하는 인터럽트를 말하며, 프로그램의 오류에 의해 생기는 인터럽트이다.

`trap` 또는 `exception` 이라고도 한다.

#### 종류

- 프로그램 검사 인터럽트 (Program check interrupt)
    - 0으로 나누는 경우
    - OverFlow/UnderFlow
    - 페이지 부재
    - 부당한 기억장소의 참조 등
- SVC (Supervisor Call: 감시프로그램 호출) 인터럽트
    - 사용자가 프로그램을 실행시키거나 supervisior을 호출하는 동작을 수행하는 경우
    - 프로그래머에 의해 코드로 짜인 감시 프로그램을 호출하는 방식

<br/><br/>

## 💡 우선순위

일반적으로 하드웨어 인터럽트가 소프트웨어 인터럽트보다 우선순위가 높다.

1. 전원 이상(Power fail)
2. 기계 착오(Machine Check)
3. 외부 신호(External)
4. 입출력(I/O)
5. 명령어 잘못
6. 프로그램 검사(Program Check)
7. SVC(SuperVisor Call)

<br/><br/>

## 💡 과정

1. 인터럽트 발생 시, CPU는 현재 진행 중인 기계어 코드를 완료한다.
2. 현재까지 수행중이었던 상태를 해당 process의 `PCB`**(Process Control Block)** 에 저장한다. (수행 중이던 MEMORY 주소, 레지스터 값, 하드웨어 상태 등)
3. PC(Program Counter)에 다음에 실행할 명령의 주소를 저장한다.
4. 인터럽트 벡터를 읽고 ISR 주소값을 얻어 `ISR`**(Interrupt Service Routine)** 로 점프하여 루틴을 실행한다.
5. 해당 코드를 실행한다.
6. 해당 작업을 다 처리하면, PCB에 보관해두었던 PC와 레지스터를 복원한다.
7. 중단되었던 곳에서부터 이어서 수행한다.

<br/><br/>

## 📌 참고

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Operating System/Interrupt.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Interrupt.md)
- [https://doh-an.tistory.com/31](https://doh-an.tistory.com/31)
- [https://raisonde.tistory.com/entry/인터럽트Interrupt의-개념과-종류](https://raisonde.tistory.com/entry/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8Interrupt%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%A2%85%EB%A5%98)

<br/>
