### 1. 다음 코드 실행 시 1, 2번의 출력값은 무엇이고, 출력값이 다른 이유는 무엇인가요?

```jsx
function test(x, y, ...z) {
  console.log(arguments.length); // 1번 출력값
}

test(1, 2, 3, 4, 5);

console.log(test.length); // 2번 출력값
```

### 2. 자바스크립트에서 함수가 정의될 때 발생하는 일을 말해보세요.

### 3. `__proto__` 접근자 프로퍼티와 `prototype` 프로퍼티는 동일한 프로토타입을 가리킨다? (O/X)

### 4. 다음 코드의 출력값을 예측해보고, 해당 출력값이 나오는 이유를 말해보세요.

```jsx
function Person() {}

Person.prototype.eyes = 2;
Person.prototype.nose = 1;

var kim = new Person();
var park = new Person();

console.log(kim.eyes); // 출력값은?
```

### 5. `__proto__` 속성을 통해 상위 프로토타입과 연결되어 있는 형태를 무엇이라고 하나요?
