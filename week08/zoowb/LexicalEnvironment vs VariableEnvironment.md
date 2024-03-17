# **LexicalEnvironment vs VariableEnvironment**

### 렉시컬 환경이란?

- 렉시컬 환경(Lexical Environment)은 식별자, 식별자에 바인딩된 값, 상위 스코프에 대한 참조를 기록하는 자료구조.
- 실행 컨텍스트를 구성하는 컴포넌트
- 스코프와 식별자를 관리한다.

### 렉시컬 환경의 구성요소

- 환경 레코즈
  - 현재 실행중인 코드 환경의 this값과 선언된 모든 변수와 함수가 저장되는 곳
  - 함수의 실행블록 또는 코드블록에 있는 모든 데이터
- 외부 렉시컬 환경
  - 렉시컬 환경의 부모 렉시컬 환경
  - 부모 렉시컬 환경 또한 환경 레코즈와 외부 렉시컬 환경을 가지며 root에 있는 전역 렉시컬 환경은 외부 렉시컬 환경으로 null값을 가짐.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7fe93563-b680-4a21-8a23-42c5ad3b7a81/d18a46ed-4493-4195-b9c5-32f70d9b076b/Untitled.png)

```jsx
<script>
  console.log(ex1) // Cannot access 'ex1' before initialization
	console.log(ex2) // Cannot access 'ex2' before initialization
	console.log(ex3) // undefined

  const ex1 = 'const';
  let ex2 = 'let'
  var ex3 = 'var';

  function f(){
      const name = 'sejin';
      console.log(`${name} ${ex1} ${ex2} ${ex3}`);
  }

  f();

 </script>
```

위 코드에는 두개의 렉시컬 환경이 존재한다.

- 전역 렉시컬 환경
- f()가 가지는 렉시컬 환경

### Lexical Environment와 Variable Environment

- 생성 초기에 둘은 동일한 렉시컬 환경을 참조하지만, 몇 가지 상황을 만나면 Variable Environment 컴포넌트를 위한 새로운 렉시컬 환경을 생성한다.
- 이 때 어떠한 상황을 만나야 Variable Environment 컴포넌트를 위한 새로운 렉시컬 환경을 생성할까?

### var, let, const

- var로 선언된 변수는 `함수 스코프`를 따른다.

```jsx
function foo() {
  if (true) {
    var a = "Hello";
  }
  console.log(a);
}
```

위 코드에서 변수를 if문 안에서 생성했으나, 함수 스코프를 따르기 때문에 함수 스코프에 변수가 저장되었다.

Hello가 출력된다.

- let, const로 선언된 변수는 `블록 스코프`를 따른다.

```jsx
function foo() {
  if (true) {
    const a = "Hello";
  }
  console.log(a);
}
```

위 코드에서 if문을 나오는 순간 블록 스코프가 종료되기 때문에 바깥의 함수 스코프에는 a 변수가 저장되어 있지 않다.

ReferenceError 발생.

### Variable Environment의 필요성

- 위에서 본 것과 같이 var와 let, const의 스코프는 다르다.
- 따라서 한 함수 안에 여러개의 블록 스코프가 존재하다면 각 블록 스코프별로 렉시컬 환경과 컴포넌트를 생성할 필요가 있다.
- 반변 함수 스코프를 따르는 var는 처음 실행 컨텍스트가 생성될 때 Variable Environment에 저장되어 사용된다.

### 참고 자료

http://dmitrysoshnikov.com/ecmascript/es5-chapter-3-2-lexical-environments-ecmascript-implementation/
https://velog.io/@cjkangme/JS-LexicalEnvironment-vs-VariableEnvironment
