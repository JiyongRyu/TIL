# 20. strict mode

### 1. strict mode란?

- strict mode는 자바스크립트 언어의 문법을 보다 엄격히 적용하여 기존에는 무시되던 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.

### 2. strict mode의 적용

- strict mode를 적용하려면 전역의 선두 또는 함수 몸체의 선두에 `'use strict';`를 추가한다. 전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

```
'use strict';

function foo() {
  x = 10; // ReferenceError: x is not defined
}
foo();
```

### 3. 전역에 strict mode를 적용하는 것은 피하자

- 전역에 적용한 strict mode는 스크립트 단위로 적용된다.

### 4. 함수 단위로 strict mode를 적용하는 것도 피하자

-  strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.

### 5. strict mode가 발생시키는 에러

### 5.1 암묵적 전역

- 선언하지 않은 변수를 참조하면 ReferenceError가 발생한다.

### 5.2 변수, 함수, 매개변수의 삭제

- delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.

### 5.3 매개변수 이름의 중복

- 중복된 함수 매개변수 이름을 사용하면 SyntaxError가 발생한다.

### 5.4 with 문의 사용

- with 문을 사용하면 SyntaxError가 발생한다.

### 6.  strict mode 적용에 의한 변화

### 6.1 일반 함수의 this

- strict mode 에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩된다

### 6.2 arguments 객체

- strict mode 에서는 매개변수에 전달된 인수를 재할당하여 변경하여도 arguments 객체에 반영되지 않는다.