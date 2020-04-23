# 6. 데이터 타입

- 데이터 타입은 값으 종류를 말함

- 7개의 데이터 타입을 제공하며 원시타입과 객체타입으로 분류

  원시 타입(primitive type)

  ​    숫자(number) 타입: 숫자. 정수와 실수 구분없이 하나의 숫자 타입만 존재

  ​    문자열(string) 타입: 문자열

  ​    불리언(boolean) 타입: 논리적 참(true)과 거짓(false)

  ​    undefined 타입: var 키워드로 선언된 변수에 암묵적으로 할당되는 값

  ​    null 타입: 값이 없다는 것을 의도적으로 명시할 때 사용하는 값

  ​    Symbol 타입: ES6에서 새롭게 추가된 7번째 타입

  객체 타입 (object/reference type): 객체, 함수, 배열 등

### 1. 숫자타입

- 64비트 부동소수점 형식을 따름

```
// 모두 숫자 타입이다.
var integer = 10;    // 정수
var double = 10.12;  // 실수
var negative = -20;  // 음의 정수

var binary = 0b01000001; // 2진수
var octal = 0o101;       // 8진수
var hex = 0x41;          // 16진수

// 표기법만 다를 뿐 모두 같은 값이다.
console.log(binary); // 65
console.log(octal);  // 65
console.log(hex);    // 65
console.log(binary === octal); // true
console.log(octal === hex);    // true

// 숫자 타입은 모두 실수로 처리된다.
console.log(1 === 1.0); // true
console.log(4 / 2);     // 2
console.log(3 / 2);     // 1.5

// 숫자 타입의 3가지 특별한 값
console.log(10 / 0);       // Infinity
console.log(10 / -0);      // -Infinity
console.log(1 * 'String'); // NaN
```

### 2. 문자열 타입

- 텍스트 데이터를 나타내는데 사용
- 0개 이상의 16bit 유니코드 문자들의 집합
- 작은 따옴표(‘’), 큰 따옴표(“”) 또는 백틱(``)으로 텍스트를 감쌈

```
// 문자열 타입
var string;
string = '문자열'; // 작은 따옴표
string = "문자열"; // 큰 따옴표
string = `문자열`; // 백틱 (ES6)

string = '작은 따옴표로 감싼 문자열 내의 "큰 따옴표"는 문자열로 인식된다.';
string = "큰 따옴표로 감싼 문자열 내의 '작은 따옴표'는 문자열로 인식된다.";

// 따옴표로 감싸지 않은 hello를 식별자로 인식한다.
var string = hello; // ReferenceError: hello is not defined
```

### 3. 템플릿 리터럴

```
var template = `Template literal`;
console.log(template); // Template literal
```

### 3.1 멀티라인 문자열

- 일반 문자열 내에서 줄바꿈은 허용되지 않음

| 이스케이프 시퀀스 | 의미                                                         |
| :---------------- | :----------------------------------------------------------- |
| \0                | Null                                                         |
| \b                | 백스페이스                                                   |
| \f                | 폼 피드(Form Feed): 프린트 출력시 다음 페이지의 시작으로 이동한다. |
| \n                | 개행(LF, Line Feed): 다음 행으로 이동                        |
| \r                | 개행(CR, Carriage Return): 커서를 처음으로 이동              |
| \t                | 탭(수평)                                                     |
| \v                | 탭(수직)                                                     |
| \uXXXX            | 유니코드. 예를 들어 ‘\u0041’은 ‘A’, ‘\uD55C’는 ‘한’, ‘\u{1F600}’는 😀이다. |
| \’                | 작은 따옴표                                                  |
| \”                | 큰 따옴표                                                    |
| \\                | 백슬래시                                                     |

### 3.2 표현식 삽입

- 문자열은 문자열 연산자 + 를 이용해 연결할수 있음
- 템플릿 리터럴 내에서는 표현식 삽입을 통해 문자열 삽입할수 있음
- 표현식 삽입은 반드시 템플릿 리터럴 내에서 사용해야함

```
var first = 'Ung-mo';
var last = 'Lee';

// ES5: 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');
// My name is Ung-mo Lee.

var first = 'Ung-mo';
var last = 'Lee';

// ES6: 표현식 삽입
console.log(`My name is ${first} ${last}.`);
// My name is Ung-mo Lee.

console.log(`1 + 2 = ${1 + 2}`); // 1 + 2 = 3
console.log('1 + 2 = ${1 + 2}'); // 1 + 2 = ${1 + 2}
```

### 4. 불리언 타입

- 논리적 참, 거짓을 나타내는 true와 false 뿐

### 5. Undefined 타입

- undefined 타입의 값은 undefined가 유일
- 변수에 값이 없다는 것을 명시하고 싶은 경우 null을 할당함

### 6. Null 타입

- null 타입의 값은 null
- 변수에 null을 할당하는 것은 변수가 이전에 참조하던 값을 더이상 참조 하지 않겠다는 의미

### 7. Symbol 타입

- 주로 이름의 충돌 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용

### 8. 데이터 타입의 필요성

### 8.1 데이터 타입에 의한 메모리 공간의 확보와 참조

- 자바엔진은 데이터 타입, 즉 값의 종류에 따라 정해진 크기의 메모리 공간을 확보
- 숫자 타입의 값을 생성할 때 배정밀도 64비트 부동소수점 포맷을 사용

### 9.2 데이터 타입에 의한 값의 해석

- 모든 값은 데이터 타입을 가지며 메모리에 2진수, 즉 비트의 나열로 저장
- 데이터 타입이 필요한 이유
  - 값을 저장할 때 확보해야 하는 **메모리 공간의 크기**를 결정하기 위해
  - 값을 참조할 때 한번에 읽어 들여야 할 **메모리 공간의 크기**를 결정하기 위해
  - 메모리에서 읽어 들인 **2진수를 어떻게 해석**할 지를 결정하기 위해

### 10. 동적 타이핑

10.1 동적 타입 언어와 정적타입 언어

- 명시적 타입선언 : C 나 Java와 같은 정적타입 언어는 변수를 선언할 때 변수에 할당할 수 있는 값의 종류, 즉 데이터 타입을 사전에 선언해야 하는데 이를 명시적 타입선언이라함
- 자바스크립트는 정적 타입 언어와는 다르게 변수를 선언할 때 타입을 선언하지 않음

```
var foo;
console.log(typeof foo);  // undefined

foo = 3;
console.log(typeof foo);  // number

foo = 'Hello';
console.log(typeof foo);  // string

foo = true;
console.log(typeof foo);  // boolean

foo = null;
console.log(typeof foo);  // object

foo = Symbol(); // 심볼
console.log(typeof foo);  // symbol

foo = {}; // 객체
console.log(typeof foo);  // object

foo = []; // 배열
console.log(typeof foo);  // object

foo = function () {}; // 함수
console.log(typeof foo);  // function
```

- 자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정되며 재할당에 의해 변수의 타입은 언제든지 동적으로 변할수 있음. 이러한 특징을 동적 타이핑이라 하고 정적타입 언어와 구별하기 위해 동적 타입 언어라 부름
- 변수는 타입을 갖지 않으며 값은 타입을 갖는다

### 10.2 동적 타입 언어와 변수

- 동적 타입 언어는 변수에 어떤 데이터 타입의 값이라도 자유롭게 할당 가능함
- 동적 타입 언어의 단점
  - 값이 언제든지 변결될 수 있기 때문에 복잡한 프로그램에서는 변화하는 변수 값을 추적하기 어려울수 있음
  - 값의 변경에 의해 타입도 언제든지 변경가능하므로 값을 확인하기 전에는 타입을 확신할 수 없음
  - 유연성은 높지만 신뢰성은 떨어짐
- 변수를 사용할때 주의점
  - 변수는 꼭 필요한 경우에 한해 제한적으로 사용해야함. 변수값은 재할당에 의해 언제든지 변경될 수 있으므로 이로 인해 동적 타입 언어인 자바스크립트는 타입을 잘못 예측해 오류가 발생할 가능성이 크기 때문
  - 변수의 유효 범위(스코프)는 최대한 좁게 만들어 변수의 부작용을 억제해야 함
  - 전역 변수는 최대한 사용하지 않도록 한다. 어디서든지 참조/변경 가능한 전역 변수는 의도치 않게 값이 변경될 가능성이 높고 다른 코드에 영향을 줄 가능성도 높음
  - 변수보다는 상수를 사용해 값의 변경을 억제해야 함
  - 변수 이름은 변수의 목적이나 의미를 파악할 수 있도록 네이밍해야함 