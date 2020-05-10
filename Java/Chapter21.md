# 21. 빌트인 객체

### 1. 자바스크립트 객체의 분류

- 표준 빌트인 객체

  표준 빌트인 객체(standard built-in objects / native objects / global objects)는 ECMAScript 사양에 정의된 객체를 말하며 애플리케이션 전역의 공통 기능을 제공한다. 표준 빌트인 객체는 ECMAScript 사양에 정의된 객체이므로 자바스크립트 실행 환경(브라우저 또는 Node.js 환경)과 관계없이 언제나 사용할 수 있다. 표준 빌트인 객체는 전역 객체의 프로퍼티로서 제공된다. 따라서 별도의 선언없이 전역 변수처럼 언제나 참조할 수 있다.

- 호스트 객체

  호스트 객체(host objects)는 ECMAScript 사양에 정의되어 있지 않지만 자바스크립트 실행 환경에서 추가적으로 제공하는 객체를 말한다. 

- 사용자 정의 객체

  사용자 정의 객체(user-defined objects)는 표준 빌트인 객체와 호스트 객체처럼 기본 제공되는 객체가 아닌 사용자가 직접 정의한 객체를 말한다.

### 2. 표준 빌트인 객체

- 자바스크립트는 Object, String, Number, Boolean, Symbol, Date, Math, RegExp, Array, Map/Set, WeakMap/WeakSet, Function, Promise, Reflect, Proxy, JSON, Error 등 40여개의 표준 빌트인 객체를 제공한다.
- Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체이다.
- 표준 빌트인 객체는 정적 메소드만을 제공한다.
- 표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체는 다양한 기능의 메소드를 제공한다. 또한 인스턴스 없이도 호출 가능한 정적 메소드도 제공한다.
- 표준 빌트인 객체인 Number는 인스턴스 없이 정적으로 호출할 수 있는 정적 메소드도 제공한다.

### 3. 원시 값과 래퍼 객체

```
const str = 'hello';

// 원시 타입인 문자열이 프로퍼티와 메소드를 갖고 있다.
console.log(str.length); // 5
console.log(str.toUpperCase()); // HELLO
```

- 원시 값을 객체처럼 사용하면 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성하고 생성된 객체로 프로퍼티에 접근하거나 메소드를 호출하고 다시 원시 값으로 되돌린다.
- 문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체를 레퍼 객체(wrapper object)라 한다.

```
const str = 'hi';

// 원시 타입인 문자열이 레퍼 객체인 String 인스턴스로 변환된다.
console.log(str.length); // 2
console.log(str.toUpperCase()); // HI

// 레퍼 객체로 프로퍼티 접근이나 메소드 호출한 후, 다시 원시값으로 되돌린다.
console.log(typeof str); // string
```

![21-1](https://poiemaweb.com/assets/fs-images/21-1.png)

### 4. 전역 객체

- 전역 객체(global object)는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이며 어떤 객체에도 속하지 않은 최상위 객체이다.
- 전역 객체는 개발자가 의도적으로 생성할 수 없다. 즉, 전역 객체를 생성할 수 있는 생성자 함수가 제공되지 않는다.
- 전역 객체의 프로퍼티를 참조할 때 window(또는 global)를 생략할 수 있다.
- 전역 객체는 Object, String, Number, Boolean, Function, Array, RegExp, Date, Math, Promise와 같은 모든 표준 빌트인 객체를 프로퍼티로 가지고 있다.
- 자바스크립트 실행 환경에  따라 추가적으로 프로퍼티와 메소드를 갖는다.
- var 키워드로 선언한 전역 변수와 선언하지 않은 변수에 값을 할당한 암묵적 전역 그리고 전역 함수는 전역 객체의 프로퍼티가 된다.
- let이나 const 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 
- 브라우저 환경의 모든 자바스크립트 코드는 하나의 전역 객체 window를 공유한다.

### 4.1 빌트인 전역 프로퍼티

- 빌트인 전역 프로퍼티(built-in global property)는 전역 객체의 프로퍼티를 의미한다. 주로 애플리케이션 전역에서 사용하는 값을 제공한다.

### 4.1.1 Infinity

- Infinity 프로퍼티는 양/음의 무한대를 나타내는 숫자값 Infinity를 갖는다.

### 4.1.2 NaN

- NaN 프로퍼티는 숫자가 아님(Not-a-Number)을 나타내는 숫자값 NaN을 갖는다. NaN 프로퍼티는 Number.NaN 프로퍼티와 같다.

### 4.1.3 undefined

- undefined 프로퍼티는 원시 타입 undefined를 값으로 갖는다.

### 4.2 빌트인 전역 함수

- 빌트인 전역 함수(built-in global function)는 애플리케이션 전역에서 호출할 수 있는 빌트인 함수로서 전역 객체의 메소드이다.

### 4.2.1 eval

- 문자열 형태로 매개변수에 전달된 코드를 런타임에 동적으로 평가하고 실행하여 결과값을 반환한다. 전달된 문자열 코드가 여러 개의 문으로 이루어져 있다면 모든 문을 실행 후 마지막 결과값을 반환한다.

### 4.2.2 isFinite

- 매개 변수에 전달된 값이 정상적인 유한수인지 검사하여 그 결과를 불리언 타입으로 반환한다. 매개변수에 전달된 값이 숫자가 아닌 경우, 숫자로 타입을 변환한 후 검사를 수행한다.

### 4.2.3 isNaN

- 매개변수에 전달된 값이 NaN인지 검사하여 그 결과를 불리언 타입으로 반환한다. 매개변수에 전달된 값이 숫자가 아닌 경우, 숫자로 타입을 변환한 후 검사를 수행한다.

### 4.2.4  parseFloat

- 매개변수에 전달된 문자열을 부동소수점 숫자(floating point number)로 변환하여 반환한다.

### 4.2.5 parseInt

- 매개변수에 전달된 문자열을 정수형 숫자(Integer)로 해석(parsing)하여 반환한다. 반환값은 언제나 10진수이다.

### 4.2.6 encodeURI / decodeURI

- encodeURI 함수는 매개변수로 전달된 URI(Uniform Resource Identifier)를 인코딩한다. URI는 인터넷에 있는 자원을 나타내는 유일한 주소를 말한다. URI의 하위개념으로 URL, URN이 있다.

### 4.2.7 encodeURIComponent / decodeURIComponent

- encodeURIComponent 함수는 매개변수로 전달된 URI(Uniform Resource Identifier) 구성 요소(component)를 인코딩한다. 

### 4.3 암묵적 전역

```
var x = 10; // 전역 변수

function foo () {
  y = 20; // 선언하지 않은 식별자에 값을 할당
}
foo();

// 선언하지 않은 식별자 y를 전역에서 참조할 수 있다.
console.log(x + y); // 30
```

- y는 전역 객체의 프로퍼티가 되어 마치 전역 변수처럼 동작한다. 이러한 현상을 암묵적 전역이라 한다.

