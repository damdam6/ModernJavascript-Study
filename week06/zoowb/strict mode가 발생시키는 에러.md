# strict mode가 발생시키는 에러

> strict mode를 적용했을 때 발생하는 에러에 대해 알아보자.

### 암묵적 전역

- 선언하지 않은 변수를 참조했을 때 **ReferenceError** 발생
  - 변수 선언이 없을 때 strict를 사용하지 않았다면 에러 발생 없이 x 변수가 전역 변수로 동적으로 생성되었겠지만, strict mode를 적용하여 에러가 발생했다.
- 꼭 var, let, const를 사용해 변수를 선언하자.

```jsx
(function () {
  "use strict";

  x = 1; //ReferenceError: x is not defined
  console.log(x);
})();

// strict mode 사용 안했을 때
(function () {
  x = 1;
  console.log(x); // 1
})();
```

### 변수, 함수, 매개변수의 삭제

- delete 연산자로 변수, 함수, 매개변수를 삭제하면 **SyntaxError**가 발생한다.
  - delete 연산자는 오직 객체의 속성을 삭제할 수 있기 때문에.
  - delete 연산자는 메모리 해제와 직접적인 연관이 없다.
  - strict mode가 아니라면 false만 반환.
- 변수의 내용을 삭제하려면 null을 할당하자. (이후 가비지 컬렉터에 의해 메모리에서 해제됨.)

```jsx
(function () {
  "use strict";

  var x = 1;
  delete x; // Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.

  function foo(a) {
    delete a; // Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.
  }
  delete foo; // Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.
})();
```

### 삭제할 수 없는 프로퍼티를 삭제하려 할 때도 예외 발생.

- Object의 prototype 프로퍼티를 삭제하려 하면 **TypeError** 발생
- Object의 prototype 프로퍼티는 삭제할 수 없다.

```jsx
(function () {
  "use strict";
  delete Object.prototype; // Uncaught TypeError: Cannot delete property 'prototype' of function Object() { [native code] }
})();
```

### 할당할 수 없는 프로퍼티에 할당 시도

- 할당할 수 없는 프로퍼티에 할당을 시도하면 **TypeError** 발생

1. 사용할 수 없는 프로퍼티에 할당 시도
2. 쓸 수 없는(writable: false) 프로퍼티에 할당 시도
3. getter-only 프로퍼티에 할당 시도
4. 확장 불가 객체에 새로운 프로퍼티 할당 시도

```jsx
"use strict";

// 1. 사용할 수 없는 프로퍼티에 할당 시도

var undefined = 5; // Uncaught TypeError: Cannot assign to read only property 'undefined' of object '#<Window>'
var Infinity = 5; // Uancaught TypeError: Cannot assign to read only property 'undefined' of object '#<Window>'

// 2. 쓸 수 없는(writable: false) 프로퍼티에 할당 시도

var obj1 = {};
Object.defineProperty(obj1, "x", { value: 42, writable: false });
obj1.x = 9; // Uncaught TypeError: Cannot assign to read only property 'x' of object '#<Object>'

// 3. getter-only 프로퍼티에 할당 시도

var obj2 = {
  get x() {
    return 17;
  },
};
obj2.x = 5; // Uncaught TypeError: Cannot set property x of #<Object> which has only a getter

// 4. 확장 불가 객체에 새로운 프로퍼티 할당 시도

var fixed = {};
Object.preventExtensions(fixed);
fixed.newProp = "ohai"; // Uncaught TypeError: Cannot add property newProp, object is not extensible
```

### 함수 파라미터 이름의 중복

- 함수 파라미터에 중복된 이름이 있다면 **SyntaxError** 발생.
  - strict mode가 아니라면 return 코드가 실행된다.

```jsx
// strict mode 적용

(function sum(a, a, c) {
  // Uncaught SyntaxError: Duplicate parameter name not allowed in this context
  "use strict";
  return a + b + c;
})();

// strict mode 적용 하지 않음 1

(function sum(a, a, c) {
  return a + b + c;
})();

sum(1, 2, 3); // Uncaught ReferenceError: b is not defined
// return 코드가 실행된다.

// strict mode 적용 하지 않음 2

(function sum(a, a, c) {
  return a + c;
})();

sum(1, 2, 3); // 5 -> 마지막으로 중복된 인수가 선택됨.
// return 코드가 실행된다.
```

### with문의 사용

- with문을 사용하면 **SyntaxError**가 발생한다.
  - with문은 전달된 객체를 스코프 체인에 추가하는 역할을 한다.
  - 동일한 객체의 프로퍼티를 반복해서 사용할 때 객체 이름을 생략할 수 있어 코드가 간단해지지만, 성능과 가독성이 나빠진다.
- with문을 사용하지 말자.
```jsx
(function () { // Uncaught SyntaxError: Strict mode code may not include a with statement
  "use strict";
  
	with({ x: 1}) {
		console.log(x);
	}
}());
```