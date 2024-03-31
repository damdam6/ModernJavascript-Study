### 일반적인 javaScript 함수의 this 바인딩
  - 함수 호출 시 함수 내부의 this는 지정되지 않는다. (지정되지 않은 this는 전역을 가르키게 된다.)
  ```js
  const dog = {
    name: 'bowwow'
    foo1: function() {
      const foo2 = function() {
        console.log(this.name);
      }
    }
  }

  dog.foo1();  // undefined
  ```
  - 왜 위의 함수에서 `dog.foo1()` 메서드를 호출할 때 this.name은  undefined가 될까?
  - 함수를 호출하면 this가 전역 객체를 가르키게 되고, 전역 객체에서 name은 정의되지 않았기 때문에 undefined가 뜬다.

### 화살표 함수의 this 바인딩
  ```js
  const dog = {
    name: 'bowwow',
    foo1: function() {
      const foo2 = () => {
        console.log(this.name);
      }
      foo2();
    }
  }

  dog.foo1();  // bowwow
  ```
  - 화살표 함수는 선언될 때 this가 없다.
  - 따라서 위의 코드에서 this는 상위 스코프에서 값을 참조한다.
  - 이를 **lexical this**라고 한다.

### 화살표 함수의 this를 사용하면 안 되는 경우
#### 1. 메서드
  ```js
  const dog = {
    name: 'bowwow';
    callName: () => console.log(this.name);
  }

  dog.callName();  // undefined
  ```
  - 위의 예시에서 this 는 dog의 선언 시점의 상위 스코프를 가리키기 때문에 전역에서 'name'을 찾는다. 그래서 undefined가 찍힌다.
  
#### 2. 생성자 함수
  ```js
  const Person(name){
    this.name = name;
  }

  Person.prototype.sayHi = () => console.log(`Hi ${this.name}`);

  const person = new Person('Lee');
  person.sayHi();  // Hi
  ```
  - 화살표 함수를 생성자 함수로 사용하면 위에서 전역 객체에서 name을 참조하므로 undefined가 생략된 값이 출력된다.
  - 화살표 함수는 생성자 함수로 사용할 수 없게 만들어 졌기 때문이다.
  - 동적 추가를 위해서는 객체 리터럴을 바인딩하고 프로토타입의 constructor 프로퍼티와 생성자 함수 간의 연결을 재설정해준다.
  ```js
  // 생성자 함수로 constructor 프로퍼티 연결 설정
  const Person(name) {
    this.name = name;
  };

  Person.prototype.sayHi = function () { console.log(`Hi ${this.name}`);}
  
  const person = new Person('Lee');
  person.sayHi();  // Hi Lee
  ```

#### 3. addEventListener()의 콜백함수
  ```js
  const button = document.getElementById('myButton');

  button.addEveneListener('click', () => {
    console.log(this);   // Window
    this.innerHTML = 'clicked';
  });

  button.addEventListener('click', function() {
    console.log(this);  // button 엘리먼트
    this.innerHTML = 'clicked';
  })
  ```
  - `addEventListener` 의 콜백함수에서는 this에 이미 해당 이벤트 리스너가 호출된 엘리먼트가 바인딩되도록 지정이 되어있다.
  - 이처럼 이미 값이 정해진 콜백함수의 경우 화살표 함수를 사용하면 기존 바인딩 값이 아니라 화살표 함수의 바인딩 값, 즉 상위 스코프로 대체되므로 의도했던 대로 동작이 되지 않을 수 있다.
  - 이런 속성을 알고 의도적으로 사용할 수는 있다. 다만 이런 경우처럼 this 가 미리 지정된 경우에 화살표 함수를 사용하는 것을 주의해야 한다.