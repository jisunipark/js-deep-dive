# 08장 제어문

### 알아두자

- break 문은 레이블 문, 반복문, switch 문의 코드 블록에서 탈출하는 역할
- continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
- switch문에서 여러 개의 case 문을 하나의 조건으로 사용할 수도 있다.
- for 문은 반복 횟수가 명확할 때 주로 사용하고 while 문은 반복 횟수가 불명확할 때 주로 사용한다.

### 무엇을 배웠나

- 블록문
- 조건문
  - if … else 문
  - switch 문
- 반복문
  - for 문
  - while 문
  - do … while 문: 코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서 코드 블록은 무조건 한 번 이상 실행된다.
    ```jsx
    var count = 0;

    // count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다,
    do {
      console.log(count);
      count++;
    } while (count < 3);
    ```
- break 문
- continue 문
