### 1. "함수의 상위 스코프를 결정한다."를 렉시컬 환경의 관점으로 설명하세요.

### 2. 다음 'multiply' 함수를 구현하세요.

```javascript
multiply(2, 4); // 8
multiply(3, 5); // 15

const double = multiply(2);
double(2); // 2
double(8); // 16

const hexa = multiply(6);
hexa(6); // 36
hexa(10); // 60
```

### 3. 아래의 코드는 잘 동작하지만 오류를 발생시킬 가능성이 있다. 클로저를 활용해서 안전한 코드를 작성하세요.

```javascript
let num = 0;

const increase = function () {
  return ++num;
};

console.log(increase());
console.log(increase());
console.log(increase());
```

### 4. 클래스 내부에 정의된 정적 메서드와 프로토타입 메서드의 차이를 설명하세요.

### 5. 아래의 코드에 존재하는 name을 private 필드로 변경하세요.

```javascript
class Person {
  name = '';
}

// 인스턴스 생성
const me = new Person();
```
