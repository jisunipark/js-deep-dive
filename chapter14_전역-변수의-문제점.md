# 14장 전역 변수의 문제점

## 변수의 생성 주기

### 지역 변수의 생명 주기

- 변수는 자신이 선언된 위치에서 생성되고 소멸한다.
- 변수 선언은 런타임 이전 단계에서 자바스크립트 엔진에 의해 먼저 실행된다.
  _→ 전역 변수에 한정_
- **지역 변수의 생명 주기는 함수의 생명 주기와 일치한다.**
- 하지만 누군가가 스코프를 참조하고 있다면 스코프는 해제되지 않고 생존하게 된다.
- **호이스팅은 스코프를 단위로 동작한다.**
  - 호이스팅은 변수 선언이 스코프의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징
  ```jsx
  var x = 'global';

  function foo() {
    console.log(x); // ① undefined
    var x = 'local';
  }

  foo();
  console.log(x); // global
  ```

### 전역 변수의 생명 주기

- **전역 변수의 생명 주기는 전역 객체의 생명 주기와 일치한다.**
  - 브라우저 환경에서 전역 객체는 `window`
    → 브라우저 환경에서 `var` 키워드로 선언한 전역 변수는 전역 객체 `window`의 프로퍼티

## 전역 변수의 문제점

1. 암묵적 결합
   - 모든 코드가 전역 변수를 참조하고 변경할 수 있음
   - 가독성은 나빠지고 의도치 않게 상태가 변경될 수 있는 위험성도 높아진다.
2. 긴 생명 주기
   - 메모리 리소스를 오랜 기간 소비한다.
   - 변수 이름이 중복되면 의도치 않은 재할당이 이뤄진다.
3. 스코프 체인 상에서 종점에 존재
   - 전역 변수의 검색 속도가 가장 느리다
4. 네임 스페이스 오염
   - 파일이 분리되어 있어도 하나의 전역 스코프를 공유
     - 다른 파일 내에서 동일한 이름으로 명명된 전역 변수나 전역 함수가 같은 스코프 내에 존재할 경우 예상치 못한 결과를 가져올 수 있다.

## 전역 변수의 사용을 억제하는 법

- **변수의 스코프는 좁을수록 좋다.**

### 즉시 실행 함수

```jsx
(function () {
  var foo = 10; // 즉시 실행 함수의 지역 변수
  // ...
})();

console.log(foo); // ReferenceError: foo is not defined
```

### 네임 스페이스 객체

```jsx
var MYAPP = {}; // 전역 네임스페이스 객체

MYAPP.name = 'Lee';

console.log(MYAPP.name); // Lee
```

```jsx
var MYAPP = {}; // 전역 네임스페이스 객체

MYAPP.person = {
  name: 'Lee',
  address: 'Seoul',
};

console.log(MYAPP.person.name); // Lee
```

### 모듈 패턴

```jsx
var Counter = (function () {
  // private 변수
  var num = 0;

  // 외부로 공개할 데이터나 메서드를 프로퍼티로 추가한 객체를 반환한다.
  return {
    increase() {
      return ++num;
    },
    decrease() {
      return --num;
    },
  };
})();

// private 변수는 외부로 노출되지 않는다.
console.log(Counter.num); // undefined

console.log(Counter.increase()); // 1
console.log(Counter.increase()); // 2
console.log(Counter.decrease()); // 1
console.log(Counter.decrease()); // 0
```

### ES6 모듈

파일 자체의 독자적인 모듈 스코프를 제공

```html
<script type="module" src="lib.mjs"></script>
<script type="module" src="app.mjs"></script>
```
