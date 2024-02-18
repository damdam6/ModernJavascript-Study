### 1. 다음 코드 실행 시 1, 2번의 출력값은 무엇이고, 출력값이 다른 이유는 무엇인가요?

```jsx
function test(x, y, ...z) {
  console.log(arguments.length); // 1번 출력값
}

test(1, 2, 3, 4, 5);

console.log(test.length); // 2번 출력값
```

    [정답]

    1번 출력값: 5
    2번 출력값: 2

- **1번**에서는 arguments.length를 호출했기 때문에 실제 함수 호출 시 전달된 인수의 수를 출력한다.

- **2번**은 함수 객체 자체의 매개변수 갯수를 나타낸다. 이 때 rest 파라미터의 갯수는 제외되기 때문에 x, y만 매개변수의 수로 인정되어 출력한다.

### 2. 자바스크립트에서 함수가 정의될 때 발생하는 일을 말해보세요.

    [정답]

    1. 해당 함수에 Constructor(생성자) 자격이 부여된다.
    - new를 통해 객체를 만들 수 있다.

    2. 해당 함수에 Prototype Object가 생성되고 연결된다.
    - 함수를 생성하면 함수 + Prototype Object도 생성된다.

### 3. `__proto__` 접근자 프로퍼티와 `prototype` 프로퍼티는 동일한 프로토타입을 가리킨다? (O/X)

    [정답] O

- 모든 객체가 가지고 있는 `__proto__` 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다.

- 하지만 프로퍼티를 사용하는 주체가 다르다.

⭐⭐⭐ `__proto__` 접근자 프로퍼티와 함수 객체의 `prototype` 프로퍼티 정리
| 구분 | 소유 | 값 | 사용 주체 | 사용 목적 |
| :-------------------------: | :---------: | :---------------: | :---------: | :--------------------------------------------------------------------------: |
| `__proto__` 접근자 프로퍼티 | 모든 객체 | 프로토타입의 참조 | 모든 객체 | 객체가 지신의 프로토타입에 접근 또는 교체하기 위해 사용 |
| prototype 프로퍼티 | constructor | 프로토타입의 참조 | 생성자 함수 | 생성자 함수가 자신이 생성할 객체(인스턴스)의 프로토타입을 할당하기 위해 사용 |

### 4. 다음 코드의 출력값을 예측해보고, 해당 출력값이 나오는 이유를 말해보세요.

```jsx
function Person() {}

Person.prototype.eyes = 2;
Person.prototype.nose = 1;

var kim = new Person();
var park = new Person();

console.log(kim.eyes); // 출력값은?
```

    [정답] 2

- kim에는 eyes라는 속성이 없는데도 kim.eyes를 실행하면 2라는 값을 출력한다.
- Prototype Object에 존재하는 eyes 속성을 어떻게 해서 참조한 것일까?
- kim이 가지고 있는 딱 하나의 속성 `__proto__`가 그것을 가능하게 해준다.
- prototype 속성은 함수만 가지고 있는 것과 달리 `__proto__` 속성은 모든 객체가 빠짐없이 가지고 있는 속성이다.
- `__proto__`는 객체가 생성될 때 조상이었던 함수의 Prototype Object를 가리킨다.
- kim 객체는 Person 함수로부터 생성되었으니 Person 함수의 Prototype Object를 가리키고 있다.
- `__proto__`는 Person 함수의 Prototype Object를 가리키고 있다.

### 5. `__proto__` 속성을 통해 상위 프로토타입과 연결되어 있는 형태를 무엇이라고 하나요?

    [정답] Prototype Chain(프로토타입 체인)

![prototype_chain](../sgryu23/image/prototype_chain.webp)

- 위와 같은 프로토타입 체인 구조 때문에 모든 객체는 Object의 자식이라 불리고 Object Prototype Object에 있는 모든 속성을 사용할 수 있다.
