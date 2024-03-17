### 함수 선언식 Function Declarations

```jsx
function 함수명() {
  구현 로직
}
```

### 함수 표현식 Function Expressions

```jsx
var 함수명 = function () {
  구현 로직
};
```

- 두 함수의 차이점
  - 함수 호이스팅
    : 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르다
    ⇒ 함수 호이스팅
    ⇒ 함수 선언문이 코드의 선두로 끌어올려진 것처럼 동작
  - 함수 표현식 → 클로져로 사용
    ```jsx
    function tabsHandler(index) {
      return function tabClickEvent(event) {
        console.log(index);
      };
    }
    ```
  - 함수 표현식 → 콜백으로 사용
    - 콜백 함수 : 다른 함수의 인자로 전달된 함수 (js의 특징)
    ```jsx
    var arr = ["a", "b", "c"];
    arr.forEach(function () {
      // ...
    });
    ```

### Airbnb 스타일은 어떤 함수를 선택하고 있는가?

- airbnb는 함수 표현식을 사용을 권장한다.
    <aside>
     `💡 [7.1]Use named function expressions instead of function declarations. `
    
    > `Why? Function declarations are hoisted, which means that it’s easy - too easy - to reference the function before it is defined in the file.`
    > 
    </aside>
    
    ⇒ 이유는 함수 호이스팅으로 인해 함수를 명확히 알아보기 어렵다는 점
    
    ```jsx
    // good
    // lexical name distinguished from the variable-referenced invocation(s)
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```
    
    ⇒ 특히 참조 변수와 구분되는 자세한 이름을 작성하여 가독성이 좋도록 함수를 선언하는 것이 권장된다.


### 그 외 함수에 관한 airbnb 코드 컨벤션

- 함수 생성자를 사용하지 말 것
    <aside>
    💡 `Never use the Function constructor to create a new function.
    Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.`
    
    </aside>
    
    ⇒ 자바스크립트에서 **`Function`** 생성자나 **`eval()`**을 사용하면, 문자열로 된 코드를 실행한다. 이는 보안문제, 디버깅 어려움, 성능 문제가 있기 때문에 권장되지 않는다.
    
    - eval()이란?
        
        **`eval()`** 함수는 자바스크립트에서 문자열로 된 코드를 실행할 수 있게 해주는 함수
        
        ```jsx
        const code = '2 + 2';
        const result = eval(code); // 4
        ```
        
        → **`eval()`**을 사용하면, 외부로부터 주입된 코드를 실행할 위험이 있다. 만약 사용자 입력을 **`eval()`**에 그대로 전달한다면, 악의적인 코드가 실행될 수 있다.
        
        → 오류가 발생했을 때, 그 오류가 어디서 발생했는지 추적하기가 힘들다
        
        → **`eval()`**은 최적화되지 않은 코드 실행 경로를 사용한다. 일반적인 코드보다 느릴 가능성이 있다.
        

- 가변 인자 함수 호출 시 전개 구문 사용하기
    <aside>
    💡 `Prefer the use of the spread syntax ... to call variadic functions. eslint: [prefer-spread](https://eslint.org/docs/rules/prefer-spread)`
    
    > `Why? It’s cleaner, you don’t need to supply a context, and you can not easily compose new with apply.`
    > 
    </aside>
    
    ```jsx
    // bad
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);
    
    // good
    const x = [1, 2, 3, 4, 5];
    console.log(...x);
    
    // bad
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));
    
    // good
    new Date(...[2016, 8, 5]);
    ```


### 출처 및 참고자료

https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/

https://github.com/airbnb/javascript?tab=readme-ov-file#functions
