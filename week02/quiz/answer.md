# answer

1. string, number, boolean, undefined, symbol, object, function
2. break foo;
3. false, undefined, null, 0, -0, NaN, ‘’
4. 좌항 피연산자가 null이나 undefined면 우항 피연산자 반환하고, 아니면 좌항 피연산자 반환한다. 좌항이 falsy라도 null이나 undefined아니면 좌항을 반환해서 변수에 기본값 설정할 때 유용하다.