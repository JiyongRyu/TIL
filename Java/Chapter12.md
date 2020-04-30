# 12. 함수

### 1. 함수란?

```
// f(x, y) = x + y
function add(x, y) {
  return x + y;
}

// f(2, 5) = 7
add(2, 5); // 7
```

- 프로그래밍 언어의 **함수는 일련의 과정을 문(statement)들로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것이다.**
- 프로그래밍 언어의 함수도 입력을 받아서 출력을 내보낸다. 이때 함수 내부로 입력을 전달받는 변수를 **매개변수(parameter)**, 입력을 **인수(argument)**, 출력을 **반환값(return value)**이라 한다.

![12-2](https://poiemaweb.com/assets/fs-images/12-2.png)

- 인수(argument)를 매개변수를 통해 함수에게 전달하면서 함수의 실행을 명시적으로 지시해야 하고 이를 **함수 호출(function call/invoke)**이라 한다.

```
// 함수 호출
var result = add(2, 5);

// 함수 add에 인수 2, 5를 전달하면서 호출하면 반환값 7을 반환한다.
console.log(result); // 7
```

- 함수는 필요할 때 여러번 호출할 수 있다. 즉, 실행 시점을 개발자가 결정할 수 있고 몇 번이든 재사용이 가능하다. 코드의 재사용이라는 측면에서 매수 유용하다.
- 코드의 중복을 억제하고 재사용성을 높이는 **함수는 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높이는 효과가 있다.**

### 3. 함수 리터럴

```
// 변수에 함수 리터럴을 할당
var add = function add(x, y) {
  return x + y;
};
```

- 함수 이름
  - 함수 이름은 식별자이다. 따라서 식별자 네이밍 규칙을 준수해야 한다.
  - 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자다.
  - 함수 이름은 생략할 수 있다. 이름이 있는 함수를 기명 함수(named function), 이름이 없는 함수를 익명 함수(anonymous function)라 한다.
- 매개변수 목록
  - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분한다.
  - 매개변수에는 함수 호출문의 인수가 순서대로 할당된다. 즉, 매개변수 목록은 순서에 의미가 있다.
  - 매개변수는 함수 몸체 내에서 변수와 동일하게 취급된다. 따라서 매개변수도 변수와 마찬가지로 식별자 네이밍 규칙을 준수해야 한다.
- 함수 몸체
  - 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행 단위로 정의한 코드 블록이다.
  - 함수 몸체는 함수 호출에 의해 실행된다.



- 함수는 객체다. 특이점이라면 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.

#### 4. 함수 정의

- 함수 선언문

```
function add(x, y) {
  return x + y;
}
```

- 함수 표현식

```
var add = function (x, y) {
  return x + y;
};
```

- Function 생성자 함수

```
var add = new Function('x', 'y', 'return x + y');
```

- 화살표 함수 : ES6

```
var add = (x, y) => x + y;
```

### 4.1 함수 선언문

```
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
// console.dir은 console.log와는 달리 함수 객체의 프로퍼티까지 출력한다.
// 단, Node.js 환경에서는 console.log와 같은 결과가 출력된다.
console.dir(add); // ƒ add(x, y)

// 함수 호출
console.log(add(2, 5)); // 7
```

- 함수 선언문은 함수 이름을 생략할수 없다
- 함수 선언문은 표현식이 아닌 문이다

![12-4](https://poiemaweb.com/assets/fs-images/12-4.png)

```
// 이름이 있는 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석한다.
// 함수 선언문은 함수 이름을 생략할 수 없다.
function foo() { console.log('foo'); }
foo(); // foo

// 함수 리터럴을 피연산자로 사용하면 함수 선언문이 아니라 함수 리터럴 표현식로 해석한다.
// 함수 리터럴은 함수 이름을 생략할 수 있다.
(function bar() { console.log('bar'); });
bar(); // ReferenceError: bar is not defined
```

- **자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고 생성된 함수 객체를 할당한다.**
- **함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.**![12-7](https://poiemaweb.com/assets/fs-images/12-7.png)

- 자바스크립트 엔진은 함수 선언문을 함수 표현식으로 변환하여 함수 객체를 생성한다고 생각할 수 있다. 단, 함수 선언문과 함수 표현식이 정확히 동일하게 동작하는 것은 아니다.

### 4.2 함수 표현식

```
// 함수 표현식
var add = function (x, y) {
  return x + y;
};

console.log(add(2, 5)); // 7
```

- 함수 리터럴의 함수 이름은 생략할 수 있다. 이러한 함수를 익명 함수(anonymous function)이라 한다. 함수 표현식의 함수 리터럴은 함수 이름을 생략하는 것이 일반적이다.

```
// 기명 함수 표현식
var add = function foo (x, y) {
  return x + y;
};

// 함수 객체를 가리키는 식별자로 호출
console.log(add(2, 5)); // 7

// 함수 이름으로 호출하면 ReferenceError가 발생한다.
// 함수 이름은 함수 몸체 내부에서만 유효한 식별자이다.
console.log(foo(2, 5)); // ReferenceError: foo is not defined
```

### 4.3 함수 생성 시점과 함수 호이스팅

```
// 함수 참조
console.dir(add); // ƒ add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

-  함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있다. 그러나 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없다. 이는 **함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문이다.**

-  var 키워드로 사용한 변수 선언문 이전에 변수를 참조하면 변수 호이스팅에 의해 undefined로 평가되지만 함수 선언문으로 정의한 함수를 함수 선언문 이전에 호출하면 함수 호이스팅에 의해 호출이 가능하다.

- **변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 된다.**

  따라서 **함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.**

### 4.4 Function 생성자 함수 

- 생성자 함수는 개체를 생성하는 함수를 말한다

```
var add = new Function('x', 'y', 'return x + y');

console.log(add(2, 5)); // 7
```

### 4.5 화살표 함수

```
// 화살표 함수
const add = (x, y) => x + y;

console.log(add(2, 5)); // 7
```

### 5. 함수 호출

- 함수는 함수를 가리키는 식별자와 한 쌍의 소괄호인 함수 호출 연산자로 호출한다. 함수 호출 연산자 내에는 0개 이상의 인수(argument)를 쉼표로 구분하여 나열한다. 함수를 호출하면 현재의 실행 흐름을 중단하고 호출된 함수로 컨트롤을 넘긴다. 이때 매개변수에 인수가 순서대로 할당되고 함수 몸체의 문들이 실행되기 시작한다.

### 5.1 매개변수와 인수

```
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 호출
// 인수 1과 2는 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행된다.
var result = add(1, 2);
```

![12-9](https://poiemaweb.com/assets/fs-images/12-9.png)

```
function add(x, y) {
  return x + y;
}

console.log(add(2)); // NaN , y가 없으므로 2 + undefined = NaN 호출

function add(x, y) {
  return x + y;
}

console.log(add(2, 5, 10)); // 7 초과된 인수는 무시된다
```

### 5.2 인수 확인

```
function add(x, y) {
  return x + y;
}

console.log(add(2));        // NaN
console.log(add('a', 'b')); // 'ab'
```

1. 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않는다.
2. 자바스크립트 함수는 매개변수의 타입을 사전에 지정할 수 없다.

- 함수를 정의할 때 적절한 인수가 전달되었는지 확인이 필요하다

### 5.3 매개변수의 최대 개수

- ECMAScript 사양에서는 매개변수의 최대 개수에 대해 명시적으로 제한하고 있지 않다. 
- 함수의 매개변수는 코드 이해에 방해가 되는 요소이므로 이상적인 매개변수 개수는 0개이며 적을 수록 좋다.

### 5.4 반환문

```
function multiply(x, y) {
  return x * y; // 값의 반환
}

// 함수는 반환값으로 평가된다.
var result = multiply(3, 5);

console.log(result); // 15
```

- 함수는 return 키워드와 반환값으로 이루어진 반환문을 사용하여 실행 결과를 함수 외부로 반환(return)할 수 있다.
- 반환문은 두가지 역할을 한다. 첫번째, 반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나간다. 따라서 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.

- 반환문은 생략할수 있다
- 반환문은 함수 몸체 내부에서만 사용할 수 있다.

```
function foo () {
  // return 키워드 뒤에 반환값을 명시적으로 지정하지 않으면 undefined가 반환된다.
  return;
}

console.log(foo()); // undefined

function multiply(x, y) {
  // return 키워드와 반환값 사이에 줄바꿈이 있으면
  return // 세미콜론 자동 삽입 기능(ASI)에 의해 세미콜론이 추가된다.
  x * y; // 무시된다.
}

console.log(multiply(3, 5)); // undefined
```

### 6. 참조에 의한 전달과 외부상태의 변경

```
// 매개변수 primitive는 원시값을 전달받고, 매개변수 obj는 객체를 전달받는다.
function changeVal(primitive, obj) {
  primitive += 100;
  obj.name = 'Kim';
}

// 외부 상태
var num = 100;
var person = { name: 'Lee' };

console.log(num); // 100
console.log(person); // {name: "Lee"}

// 원시값은 값 자체가 복사되어 전달되고 객체는 참조값이 복사되어 전달된다.
changeVal(num, person);

// 원시 값은 원본이 훼손되지 않는다.
console.log(num); // 100

// 객체는 원본이 훼손된다.
console.log(person); // {name: "Kim"}
```

![12-10](https://poiemaweb.com/assets/fs-images/12-10.png)

### 7. 다양한 함수의 형태

### 7.1 즉시실행함수

- 즉시 실행 함수는 단 한번만 호출되며 다시 호출할 수는 없다.

```
// 익명 즉시 실행 함수
(function () {
  var a = 3;
  var b = 5;
  return a * b;
}());

// 기명 즉시 실행 함수
(function foo() {
  var a = 3;
  var b = 5;
  return a * b;
}());

foo(); // ReferenceError: foo is not defined

// 즉시 실행 함수도 일반 함수처럼 값을 반환할 수 있다.
var res = (function () {
  var a = 3;
  var b = 5;
  return a * b;
}());

console.log(res); // 15

// 즉시 실행 함수에도 일반 함수처럼 인수를 전달할 수 있다.
res = (function (a, b) {
  return a * b;
}(3, 5));

console.log(res); // 15
```

### 7.2 재귀 함수

- 함수가 자기 자신을 호출하는 행위, 즉 재귀 호출을 수행하는 함수를 말한다

```
// 함수 표현식
var factorial = function foo(n) {
  // 탈출 조건: n이 1 이하일 때 재귀 호출을 멈춘다.
  if (n <= 1) return 1;
  // 함수를 가리키는 식별자로 자기 자신을 재귀 호출
  return n * factorial(n - 1);

  // 함수 이름으로 자기 자신을 재귀 호출할 수도 있다.
  // console.log(factorial === foo); // true
  // return n * foo(n - 1);
};

console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
```

### 7.3 중첩 함수

- 함수 내부에 정의된 함수를 중첩 함수 또는 내부 함수라 한다.
- 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수의 역할을 한다.

```
function outer() {
  var x = 1;

  // 중첩 함수
  function inner() {
    var y = 2;
    // 외부 함수의 변수를 참조할 수 있다.
    console.log(x + y); // 3
  }

  inner();
}

outer();
```

### 7.4 콜백 함수

```
// n만큼 어떤 일을 반복한다
function repeat1(n) {
  // i를 출력한다.
  for (var i = 0; i < n; i++) console.log(i);
}

repeat1(5); // 0 1 2 3 4

// n만큼 어떤 일을 반복한다
function repeat2(n) {
  for (var i = 0; i < n; i++) {
    // i가 홀수일 때만 출력한다.
    if (i % 2) console.log(i);
  }
}

repeat2(5); // 1 3

// 외부에서 전달받은 f를 n만큼 반복 호출한다
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    // i를 전달하면서 f를 호출
    f(i);
  }
}

var logAll = function (i) {
  console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll); // 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1 3

```

- **함수의 매개변수를 통해 전달되는 함수를 콜백 함수(callback function)라고 하며, 콜백 함수를 매개변수를 통해 전달받은 함수를 고차 함수(Higher-Order Function, HOF)라고 한다**

### 7.5 순수 함수와 비순수 함수

- 부수 효과가 없는 함수를 순수 함수(pure function), 외부 상태를 변경시키는 즉, 부수 효과가 있는 함수를 비순수 함수(impure function)라고 부른다.