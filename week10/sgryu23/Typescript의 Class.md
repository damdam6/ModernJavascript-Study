- Typescript가 지원하는 클래스는 ECMAScript 6의 클래스과 유사하지만 몇 가지 Typescript의 고유한 확장 기능이 있다.

### 1. 클래스 정의(Class Definition)
- ES6 클래스는 클래스 몸체 내에 메소드만을 포함할 수 있다.
- 클래스 몸체에 클래스 프로퍼티를 선언할 수 없고 반드시 생성자 내부에서 클래스 프로퍼티를 선언하고 초기화한다.

```js
// person.js
class Person {
  constructor(name) {
    // 클래스 프로퍼티의 선언과 초기화
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

const person = new Person(Pangpang_e)
person.walk()  // pangpang_e is walking.
```

- 위 코드를 실행하면 ES6에서는 문제 없이 실행이 되지만 확장자를 ts로 바꾸어 컴파일하면 아래와 같은 에러 메시지가 뜬다.
```
person.ts(4, 10): error TS2339: Property 'name' does not exist on type 'Person'.
person.ts(8, 25): error TS2339: Property 'name' does not exist on type 'Person'.
```

- Typescript 클래스는 클래스 몸체에 프로퍼티를 아래와 같이 사전 선언해야 한다.
```ts
// person.ts
class Person {
  // 클래스 프로퍼티를 사전 선언해야 한다.
  name: string;

  constructor(name: string) {
    // 클래스 프로퍼티에 값을 할당
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

const person = new Person('Pangpang_e')
person.walk();  // Pangpang_e is walking.
```

### 2. 접근 제한자
- Typescript 클래스는 클래스 기반 객체 지향 언어가 지원하는 접근 제한자(Access modifier) public, private, protected를 지원하며 의미 또한 기본적으로 동일하다.
- 단, 접근 제한자를 **명시하지 않았을 때** 다른 클래스 기반의 언어는 암묵적으로 protected가 지정되어 패키지 레벨로 공개되지만, <b style="color:orange">Typescript의 경우 접근 제한자를 생략한 클래스 프로퍼티와 메소드는 암묵적으로 <a style="background:yellow">public</a>이 선언</b>된다.
- 따라서 public으로 지정하고자 하는 멤버 변수와 메서드는 접근 제한자를 생략한다.

[접근 제한자를 선언한 프로퍼티와 메서드에 대한 접근 가능성(in Typescript)]
|  접근 가능성  |  public  |  protected  | private  |
|--------------|----------|-------------|----------|
|  클래스 내부  |    O     |      O      |     O    |
|자식 클래스 내부|   O      |     O      |     X    |
| 클래스 인스턴스|   O     |      X      |     X    |

- 접근 제한자가 선언된 프로퍼티로의 접근 가능성 예시
```ts
class Foo {
  public x: string;
  protected y: string;
  private z: string;

  constructor(x: string, y: string, z: string) {
    // public, protected, private 접근 제한자 모두 클래스 내부에서 참조 가능
    this.x = x;
    this.y = y;
    this.z = z;
  }
}

const foo = new Foo('x', 'y', 'z');

// public 접근 제한자는 클래스 인스턴스를 통해 클래스 외부에서 참조 가능하다.
console.log(foo.x);

// protected 접근 제한자는 클래스 인스턴스를 통해 클래스 외부에서 참조할 수 없다.
console.log(foo.y);
// error TS2445: Property 'y' is protected and only accessible within class 'Foo' and its subclasses.

// private 접근 제한자는 클래스 인스턴스를 통해 클래스 외부에서 참조할 수 없다.
console.log(foo.z);
// error TS2341: Property 'z' is private and only accessible within class 'Foo'.

class Bar extends Foo {
  constructor(x: string, y: string, z: string) {
    super(x, y, z);

    // public 접근 제한자는 자식 클래스 내부에서 참조 가능하다.
    console.log(this.x);

    // protected 접근 제한자는 자식 클래스 내부에서 참조 가능하다.
    console.log(this.y);

    // private 접근 제한자는 자식 클래스 내부에서 참조할 수 없다.
    console.log(this.z);
    // error TS2341: Property 'z' is private and only accessible within class 'Foo'.
  }
}
```

### 3. 생성자 파라미터에 접근 제한자 선언
- 접근 제한자는 생성자 파라미터에도 선언할 수 있다.
- 접근 제한자가 생성된 파라미터는 암묵적으로 클래스 프로퍼티로 선언되고 생성자 내부에서 별도의 초기화가 없어도 암묵적으로 초기화가 수행된다.
- 이때 private 접근 제한자가 사용되면 클래스 내부에서만 참조가 가능하고 public 접근 제한자가 사용되면 클래스 외부에서도 참조가 가능하다.

```ts
class Foo {
  /*
  접근 제한자가 선언된 생성자 파라미터 x는 클래스 프로퍼티로 선언되고 지동으로 초기화된다.
  public이 선언되었으므로 x는 클래스 외부에서도 참조가 가능하다.
  */
  constructor(public x: string) { }
}

const foo = new Foo('Hello');
console.log(foo);   // Foo { x: 'Hello' }
console.log(foo.x); // Hello

class Bar {
  /*
  접근 제한자가 선언된 생성자 파라미터 x는 멤버 변수로 선언되고 자동으로 초기화된다.
  private이 선언되었으므로 x는 클래스 내부에서만 참조 가능하다.
  */
  constructor(private x: string) { }
}

const bar = new Bar('Hello');

console.log(bar); // Bar { x: 'Hello' }

// private이 선언된 bar.x는 클래스 내부에서만 참조 가능하다
console.log(bar.x); // Property 'x' is private and only accessible within class 'Bar'.
```

### 4. static 키워드
- ES6 클래스에서 static 키워드는 클래스의 정적(static) 메서드를 정의함
- 정적 메서드는 클래스의 인스턴스가 아닌 클래스 이름으로 호출함 -> 클래스의 인스턴스를 생성하지 않고도 호출이 가능하다.

```js
class Foo {
  constructor(prop) {
    this.prop = prop;
  }

  static staticMethod() {
    /*
    정적 메소드는 this를 사용할 수 없다.
    정적 메소드 내부에서 this는 클래스의 인스턴스가 아닌 클래스 자신을 가리킨다.
    */
    return 'staticMethod';
  }

  prototypeMethod() {
    return this.prop;
  }
}

// 정적 메소드는 클래스 이름으로 호출한다.
console.log(Foo.staticMethod());

const foo = new Foo(123);
// 정적 메소드는 인스턴스로 호출할 수 없다.
console.log(foo.staticMethod()); // Uncaught TypeError: foo.staticMethod is not a function
```

- Typescript에서는 static 키워드를 클래스 프로퍼티에도 사용할 수 있다.
- 정적 메서드와 마찬가지로 정적 클래스 프로퍼티는 인스턴스가 아닌 클래스 이름으로 호출하며 클래스의 인스턴스를 생성하지 않아도 호출이 가능하다.

```ts
class Foo {
  // 생성된 인스턴스의 갯수
  static instanceCounter = 0;
  constructor() {
    // 생성자가 호출될 때마다 카운터를 1씩 증가시킨다.
    Foo.instanceCounter++;
  }
}

var foo1 = new Foo();
var foo2 = new Foo();

console.log(Foo.instanceCounter);  // 2
console.log(foo2.instanceCounter); // error TS2339: Property 'instanceCounter' does not exist on type 'Foo'.
```

[참고 자료]
1. https://poiemaweb.com/typescript-class
2. https://www.typescriptlang.org/docs/handbook/2/classes.html