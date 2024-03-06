# 09장 타입 변환과 단축 평가

### 알아두자

- 단축평가
- 옵셔널 체이닝 연산자 **?.**

```jsx
var elem = null;

// elem이 null 또는 undefined이면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // undefined
```

- null 병합 연산자 **??**

```jsx
// 좌항의 피연산자가 null 또는 undefined이면 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
var foo = null ?? 'default string';
console.log(foo); // "default string"
```

### 헷갈리는 것

- (p. 121) 함수 매개변수에 기본값을 설정할 때