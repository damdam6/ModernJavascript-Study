### 1. "렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값을 결정한다."

### 2.

```javascript
const multiply = (x1, x2) => {
  if (x2) {
    return x1 * x2;
  }
  return (n) => {
    return x1 * n;
  };
};
```

### 3.

```javascript
const increase = (function () {
  let num = 0;

  // 클로저
  return function () {
    return ++num;
  };
})();
```

### 4.

1. 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.

### 5.

```javascript
class Person {
  // private 필드 정의
  #name = '';

  Constructor(name) {
    // private 필드 참조
    this.#name = name;
  }
}

// 인스턴스 생성
const me = new Person('hunteac');
```
