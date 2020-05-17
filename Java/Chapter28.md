# 28. Number

### 1. Number 생성자 함수

- 표준 빌트인 객체인 Number 객체는 생성자 함수 객체이다. 따라서 new 연산자와 함께 호출하여 Number 인스턴스를 생성할 수 있다.
- Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.
- Number 생성자 함수에 숫자를 인수로 전달하면 [[NumberData]] 내부 슬롯에 인수로 전달받은 숫자를 할당한 Number 래퍼 객체를 생성한다.
- Number 생성자 함수에 숫자가 아닌 값을 인수로 전달하면 전달받은 인수를 숫자로 강제 변환한 후, [[NumberData]] 내부 슬롯에 변환된 숫자를 할당한 Number 래퍼 객체를 생성한다. 전달받은 인수를 숫자로 변환할 수 없다면 NaN을 [[NumberData]] 내부 슬롯에 할당한 Number 래퍼 객체를 생성한다.
-  new 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 Number 인스턴스가 아닌 숫자를 반환한다. 

### 2. Number 프로퍼티

### 2.1 Number.EPSILON

- 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다.

```javascript
function isEqual(a, b){
  // Math.abs는 절댓값을 반환한다.
  // a와 b의 차이가 Number.EPSILON보다 작으면 같은 수로 인정한다.
  return Math.abs(a - b) < Number.EPSILON;
}

console.log(isEqual(0.1 + 0.2, 0.3)); // true
```

### 2.2 Number.MAX_VALUE

- 자바스크립트에서 표현할 수 있는 가장 큰 양수 값(1.7976931348623157 x 10308)이다. Number.MAX_VALUE보다 큰 숫자는 Infinity이다.

### 2.3 Number.MAX_SAFE_INTEGER

- 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수 값(9007199254740991)이다.

### 2.4 Number.MIN_VALUE

- 자바스크립트에서 표현할 수 있는 가장 작은 양수 값(5 x 10-324)이다. Number.MIN_VALUE보다 작은 숫자는 0이다.

### 2.5 Number.MIN_SAFE_INTEGER

-  자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수 값( -9007199254740991)이다.

### 2.6 Number.POSITIVE_INFINITY

- 양의 무한대를 나타내는 숫자값 Infinity와 같다.

### 2.7 Number.NEGATIVE_INFINITY

- 음의 무한대를 나타내는 숫자값 -Infinity와 같다.

### 2.8 Number.NaN

- 숫자가 아님(Not-a-Number)을 나타내는 숫자값이다. Number.NaN은 window.NaN과 같다.

### 3. Number 메소드

### 3.1 Number.isFinite

- 인수로 전달된 숫자값이 정상적인 유한수, 즉 Infinity 또는 -Infinity가 아닌지 검사하여 그 결과를 불리언 값으로 반환한다.

```javascript
// 인수가 유한수이면 true를 반환한다.
Number.isFinite(0);                // -> true
Number.isFinite(Number.MAX_VALUE); // -> true
Number.isFinite(Number.MIN_VALUE); // -> true

// 인수가 무한수이면 false를 반환한다.
Number.isFinite(Infinity);  // -> false
Number.isFinite(-Infinity); // -> false
```

### 3.2 Number.isInteger

- 인수로 전달된 값이 정수(Integer)인지 검사하여 그 결과를 불리언 값으로 반환한다. 검사전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

```javascript
// 인수가 정수이면 true를 반환한다.
Number.isInteger(0)     // -> true
Number.isInteger(123)   // -> true
Number.isInteger(-123)  // -> true

// 0.5는 정수가 아니다.
Number.isInteger(0.5)   // -> false
// '123'을 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger('123') // -> false
// false를 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger(false) // -> false
// Infinity/-Infinity는 정수가 아니다.
Number.isInteger(Infinity)  // -> false
Number.isInteger(-Infinity) // -> false
```

### 3.3 Number.isNaN

- 인수로 전달된 값이 NaN인지 검사하여 그 결과를 불리언 값으로 반환한다.
- 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다. 따라서 숫자가 아닌 인수가 주어졌을 때 반환값은 언제나 false가 된다.

### 3.4 Number.isSafeInteger

- 인수로 전달된 값이 안전한(safe) 정수값인지 검사하여 검사하여 그 결과를 불리언 값으로 반환한다. 검사전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

### 3.5 Number.prototype.toExponential

- 전달받는 인수를 지수 표기법으로 변환하여 문자열로 반환한다.

### 3.6 Number.prototype.toFixed

- 대상 숫자를 반올림하여 문자열로 반환한다.

### 3.7 Number.prototype.toPrecision

- 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다. 

### 3.8 Number.prototype.toString

-  숫자를 문자열로 변환하여 반환한다.

