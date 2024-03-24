### 자바스크립트와 타입스크립트 접근제어자 문법 차이 (feat. class)

- 객체 지향 설계란?
    - 각 객체가 어떤 역할을 맡고 어떻게 협력할지 구성하는게 중요
    - 그러나 초기 자바스크립트 → 객체지향 프로그래밍에 최적화 되지 못했다.
        
        ⇒ 현재도 캡슐화를 완전히 지원하지 못한다.
        

- 자바스크립트의 Class
    - ES6에 class문이 생겼다
    - ES6 이전 → 생성자 함수 사용해 class와 유사한 느낌의 객체를 만들어서 사용함.
        - class와는 다른 객체였다.
    - 객체지향프로그래밍을 지원하기 위해 Class기능이 생겼다고 보면 된다.
    
- private이 없다고?
    - JavaScript = 기본적으로 프로퍼티와 메서드는 모두 public 상태가 된다.
    - private이라는 개념이 없(었)다.
    
    ```jsx
    class testClass{
    _count=0;
    }
    ```
    
    ⇒ 이런식으로 실제로는 public이나 개발자 간 암묵적인 룰을 기반으로 ( _ )가 붙으면 외부에서 접근하지 못하는 프로퍼티를 표현했다고 보았다.
    
- private은 추가 되었다!
    - ES2019에 prefix #을 추가했다.
    
    ```jsx
    class testClass{
    	#privateField
    	}
    ```
    
    ⇒ 이 클래스에서만 해당 값 직접 접근 가능
    
    - 단, protected와 다르게 클래스를 상속한 자식 클래스에서도 접근이 불가능하다.
    

- TypeScript에서는 Class관리법을 명시적으로 제공한다.
    - public
        - 명시도 가능 / 명시하지 않아도 기본으로 설정
    - protected
        - 클래스와 상속된 클래스에서만 접근 가능하다!
        - 단, 상속된 클래스에서 protected를 걸어주지 않으면 public으로 선언된다.
    - private
        - 클래스 외부로부터의 접근을 모두 막을 수 있다.

- TypeScript 한계
    - 타입 체킹만 가능하다!
    - 런타임에는 작동한다. (Javascript는 막지 못하므로..)

- TypeScript Class에서 사용할 수 있는 다른 도구들
    - readonly
        - protected가 아니라, readonly만 표기하면, 값이 바뀌지 않는 프로퍼티 생성 가능
    - static
        - 싱글턴 패턴
        - instance → static으로 선언하기
            - constructor를 private으로 선언하면 됨.
        

참고자료

[https://medium.com/hcleedev/web-typescript의-public-protected-private-알아보기-31e16bc11d32](https://medium.com/hcleedev/web-typescript%EC%9D%98-public-protected-private-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-31e16bc11d32)

https://cpro95.tistory.com/677