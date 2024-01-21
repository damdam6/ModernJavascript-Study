# Object.is와 일치비교연산자(===) 비교

Date: January 21, 2024

## [Object.is](http://Object.is) 와 === 비교

### 자바스크립트의 비교 연산

- `[===` (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality) - 엄격한 동등 (삼중 등호)
- `[==](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Equality)` - 느슨한 동등 (이중 등호)
- `[Object.is()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/is)`

| x                 | y                 | ==       | ===      | Object.is | SameValueZero |
| ----------------- | ----------------- | -------- | -------- | --------- | ------------- |
| undefined         | undefined         | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| null              | null              | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| true              | true              | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| false             | false             | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| 'foo'             | 'foo'             | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| 0                 | 0                 | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| +0                | -0                | ✅ true  | ✅ true  | ❌ false  | ✅ true       |
| +0                | 0                 | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| -0                | 0                 | ✅ true  | ✅ true  | ❌ false  | ✅ true       |
| 0n                | -0n               | ✅ true  | ✅ true  | ✅ true   | ✅ true       |
| 0                 | false             | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| ""                | false             | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| ""                | 0                 | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| '0'               | 0                 | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| '17'              | 17                | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| [1, 2]            | '1,2'             | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| new String('foo') | 'foo'             | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| null              | undefined         | ✅ true  | ❌ false | ❌ false  | ❌ false      |
| null              | false             | ❌ false | ❌ false | ❌ false  | ❌ false      |
| undefined         | false             | ❌ false | ❌ false | ❌ false  | ❌ false      |
| { foo: 'bar' }    | { foo: 'bar' }    | ❌ false | ❌ false | ❌ false  | ❌ false      |
| new String('foo') | new String('foo') | ❌ false | ❌ false | ❌ false  | ❌ false      |
| 0                 | null              | ❌ false | ❌ false | ❌ false  | ❌ false      |
| 0                 | NaN               | ❌ false | ❌ false | ❌ false  | ❌ false      |
| 'foo'             | NaN               | ❌ false | ❌ false | ❌ false  | ❌ false      |
| NaN               | NaN               | ❌ false | ❌ false | ✅ true   | ✅ true       |

### IsLooselyEqual(x,y) 알고리즘( == )

느슨한 비교를 입력해볼 수 있는 사이트 [https://felix-kling.de/js-loose-comparison/](https://felix-kling.de/js-loose-comparison/)

⇒ 각각의 단계에 대한 흐름을 살펴볼 수 있다.

![Untitled](./Object.is와%20연산자%20비교/isLooselyEqual.png)

### IsStrictlyEqual(x,y) 알고리즘 (===)

![Untitled](./Object.is와%20연산자%20비교/isStrictlyEqual.png)

![Untitled](./Object.is와%20연산자%20비교/Number-equal.png)

⇒ `===` 외에도 엄격한 동등은

`[Array.prototype.indexOf()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)`,  `[Array.prototype.lastIndexOf()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)`,  `[TypedArray.prototype.indexOf()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/indexOf)`,  `[TypedArray.prototype.lastIndexOf()` (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/lastIndexOf), 그리고 `[case` (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch) 일치를 포함한 인덱스 검색 메서드에서 사용된다.

### SameValue(x,y) 알고리즘 Object.is

![Untitled](./Object.is와%20연산자%20비교/SameValue.png)

![Untitled](./Object.is와%20연산자%20비교/Number-sameValue.png)

### Object.is의 폴리필 코드 살펴보기

```sql
0 === -0 // true
Object.is(0, -0); // false

NaN === 0/0 // false
Object.is(NaN, 0/0); // true

NaN === NaN // false
Object.is(NaN, NaN); // true
```

→ 가장 큰 차이 점 : Nan 비교와 +0,-0 비교가 가능해졌다.

```sql
if (!Object.is) {
  Object.is = function(x, y) {
    if (x === y) {
      return x !== 0 || 1 / x === 1 / y;
   } else {
     return x !== x && y !== y;
   }
  };
}
```

→ 폴리필 코드에서도 해당 부분만 예외처리를 통해 처리하고 있다.
<br>

Q. 선후관계에 대한 의문이 여전히 있다. 왜 Object.is와 ===은 다르게 구성했을까. 이후 등장한 Object.is의 필요성 때문일 것 같은데, 무엇을 위해 등장했나?

<br>

### 참고자료 및 출처

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Equality_comparisons_and_sameness](https://developer.mozilla.org/ko/docs/Web/JavaScript/Equality_comparisons_and_sameness)

[https://tc39.es/ecma262/multipage/abstract-operations.html#sec-islooselyequal](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-islooselyequal)

[https://tc39.es/ecma262/multipage/abstract-operations.html#sec-isstrictlyequal](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-isstrictlyequal)

[https://tc39.es/ecma262/multipage/abstract-operations.html#sec-samevalue](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-samevalue)

[https://medium.com/jung-han/js-2탄-그리고-object-is-e58b72e90443](https://medium.com/jung-han/js-2%ED%83%84-%EA%B7%B8%EB%A6%AC%EA%B3%A0-object-is-e58b72e90443)
