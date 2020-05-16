# 26. ES6 함수의 추가 기능

### 1. 함수의 구분

- ES6 이전의 함수는 동일한 함수라도 다양한 형태로 호출할 수 있다.

```javascript
var foo = function () {
  return 1;
};

// 일반적인 함수로서 호출
foo(); // -> 1

// 생성자 함수로서 호출
new foo(); // -> foo {}

// 메소드로서 호출
var obj = { a: foo };
obj.a(); // -> 1
```

- ES6 이전의 모든 함수는 callable이며 constructor이다.

| ES6 함수의 구분    | constructor | prototype | super | arguments |
| :----------------- | :---------: | :-------: | :---: | :-------: |
| 일반 함수(Normal)  |      ○      |     ○     |   ✗   |     ○     |
| 메소드(Method)     |      ✗      |     ✗     |   ○   |     ○     |
| 화살표 함수(Arrow) |      ✗      |     ✗     |   ✗   |     ✗     |

### 2. 메소드

- ES6 이전 사양에는 메소드에 대한 명확한 정의가 없었다. 일반적으로 메소드는 객체에 바인딩된 함수를 일컫는 의미로 사용되었다. ES6 사양에서는 메소드에 대한 정의가 명확하게 규정되었다. ES6 사양에서 메소드는 메소드 축약 표현으로 정의된 함수 만을 의미한다.

```javascript
const obj = {
  x: 1,
  // foo는 메소드이다.
  foo() { return this.x; },
  // bar에 바인딩된 함수는 메소드가 아닌 일반 함수이다.
  bar: function() { return this.x; }
};

console.log(obj.foo()); // 1
console.log(obj.bar()); // 1
```

### 3. 화살표 함수

- 화살표 함수(arrow function)는 function 키워드 대신 화살표(=>, fat arrow)를 사용하여 보다 기존의 함수 정의 방식보다 간략하게 함수를 정의할 수 있다. 화살표 함수는 표현만 간략한 것이 아니라 내부 동작도 기존의 함수보다 간략하다. 특히 화살표 함수는 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용하다.

### 3.1 화살표 함수 정의

1. 매개 변수 선언

```javascript
(x, y) => { ... } // 매개 변수가 여러 개인 경우, 소괄호 () 안에 매개 변수를 선언한다.
x => { ... } // 매개 변수가 한 개인 경우, 소괄호 ()를 생략할 수 있다.
() => { ... } // 매개 변수가 없는 경우, 소괄호 ()를 생략할 수 없다.
```

2. 함수 몸체 정의

   함수 몸체가 한 줄의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {}를 생략할 수 있다. 이때 문은 암묵적으로 반환된다

```javascript
x => x * x;
// 위 표현과 동일하다.
x => { return x * x; }

// 매개 변수가 없는 화살표 함수
const now = () => Date.now();
now(); // -> 1567061352352

// 함수 표현식
var now = function() {
  return Date.now();
};
now(); // -> 1567061352352

// 매개 변수가 한 개인 화살표 함수
const identity = value => value;

// 함수 표현식
var identity = function(value) {
  return value;
};

// 매개 변수가 여러 개인 화살표 함수
const sum = (a, b) => a + b;

// 함수 표현식
var sum = function(a, b) {
  return a + b;
};
```

함수 몸체가 여러 줄의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {}를 생략할 수 없다. 이때 반환값이 있다면 명시적으로 반환해야 한다.

```javascript
// 화살표 함수
const sum = (a, b) => {
  const result = a + b;
  return result;
};

// 함수 표현식
var sum = function (a, b) {
  const result = a + b;
  return result;
};
```

객체 리터럴을 반환하는 경우, 객체 리터럴을 소괄호 ()로 감싸 주어야 한다.

```javascript
() => { return { a: 1 }; };
// 위 표현과 동일하다.
() => ({ a: 1 });
// 화살표 함수
const create = (id, content) => ({ id, content });

// 함수 표현식
var create = function (id, content) {
  return { id, content };
};

create(1, 'JavaScript'); // -> {id: 1, content: "JavaScript"}
```

화살표 함수도 즉시 실행 함수(IIFE)로 사용할 수 있다.

```javascript
const person = (name => ({
  sayHi() { return `Hi? My name is ${name}.`; }
}))('Lee');

console.log(person.sayHi()); // Hi? My name is Lee.
```

화살표 함수도 일급 객체이므로 Array.prototype.map, Array.prototype.filter, Array.prototype.reduce와 같은 고차 함수(Higher-Order Function, HOF)에 인수로 전달할 수 있다. 이 경우, 일반적인 함수 표현식보다 표현이 간결하고 가독성이 좋다.

```javascript
// ES5
[1, 2, 3].map(function (v) {
  return v * 2;
});

// ES6
[1, 2, 3].map(v => v * 2); // -> [ 2, 4, 6 ]
```

### 3.2 화살표 함수와 일반 함수 차이

1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor이다.
   - 화살표 함수는 생성자 함수로서 호출할 수 없다.
   - 화살표 함수는 인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.
2. 중복된 매개 변수 이름을 선언할 수 없다.
   - 일반 함수는 중복된 매개 변수 이름을 선언해도 에러가 발생하지 않는다.
   - 화살표 함수는 중복된 매개 변수 이름을 선언할 수 없다.
3. 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않는다.
   - 화살표 함수 내부에서 this, arguments, super, new.target를 참조하면 스코프 체인을 통해 상위 스코프의 this, arguments, super, new.target를 참조한다.
   - 화살표 함수가 중첩 함수인 경우, 상위 스코프에 존재하는 가장 가까운 함수 중에서 화살표 함수가 아닌 부모 함수의 this, arguments, super, new.target를 참조한다.

### 3.3 this

- 화살표 함수가 일반 함수와 구별되는 가장 큰 특징은 바로 this이다. 그리고 화살표 함수는 다른 함수의 인수로 전달되어 콜백 함수로 사용되는 경우가 많다. 
- 아래의 예시에서 콜백 함수의 this(②)와 외부 함수의 this(①)가 서로 다른 객체를 가리키고 있기 때문에 TypeError가 발생하는일이 발생하는 것을 보여주는데 ES6 이전에는 이와 같은 “콜백 함수 내부의 this 문제”를 해결하기 위해  3가지 방법을 사용했다.

```javascript
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  prefixArray(arr) {
    // ①
    // Array.prototype.map 메소드는 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다.
    // 그리고 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다. ("27.9.3. Array.prototype.map" 참고)
    // 인수로 전달된 배열 arr을 순회하며 배열의 모든 요소에 prefix를 추가한다.
    return arr.map(function (item) {
      return this.prefix + ' ' + item; // ②
      // -> TypeError: Cannot read property 'prefix' of undefined
    });
  }
}

const prefixer = new Prefixer('Hi');
console.log(prefixer.prefixArray(['Lee', 'Kim']));
```

1. 메소드를 호출한 prefixer 객체를 가리키는 this를 일단 회피시킨 다음 콜백 함수 내부에서 사용한다.

```javascript
...
prefixArray(arr) {
  const that = this;
  return arr.map(function (item) {
    return that.prefix + ' ' + item;
  });
}
...
```

2. Array.prototype.map의 2번째 인수로 메소드를 호출한 prefixer 객체를 가리키는 this를 전달한다.

```javascript
...
prefixArray(arr) {
  return arr.map(function (item) {
    return this.prefix + ' ' + item;
  }, this);
}
...
```

3. Function.prototype.bind 메소드를 사용하여 메소드를 호출한 prefixer 객체를 가리키는 this를 바인딩한다.

```javascript
class Prefixer {
  constructor(prefix) {
    this.prefix = prefix;
  }

  prefixArray(arr) {
    return arr.map(item => `${this.prefix} ${item}`);
  }
}
const prefixer = new Prefixer('Hi');
prefixer.prefixArray(['Lee', 'Kim']); // -> ['Hi Lee', 'Hi Kim']
```

- 화살표 함수는 함수 자체의 this 바인딩이 없다. 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다. 이를 lexical this라 한다. 이는 마치 렉시컬 스코프와 같이 화살표 함수의 this가 함수가 정의된 위치에 의해 결정된다는 것을 의미한다.
- 화살표 함수가 중첩 함수인 경우, 상위 스코프에 존재하는 가장 가까운 함수 중에서 화살표 함수가 아닌 부모 함수의 this를 참조한다. 만약 화살표 함수가 전역 함수라면 화살표 함수의 this는 전역 객체를 가리킨다.

```javascript
// 화살표 함수는 함수 자체의 this 바인딩이 없다.
// 전역 함수 foo의 상위 스코프는 전역이다.
// 따라서 화살표 함수 foo의 this는 전역 객체를 가리킨다.
const foo = () => console.log(this);
foo(); // window

// 중첩 함수 bar의 상위 스코프는 즉시 실행 함수이다.
// 따라서 화살표 함수 foo의 this는 즉시 실행 함수의 this를 가리킨다.
(function () {
  const bar = () => console.log(this);
  bar();
}).call({ a: 1 }); // { a: 1 }

// 함수 baz는 화살표 함수를 반환한다.
// 반환된 화살표 함수의 상위 스코프는 화살표 함수 baz이고 화살표 함수 baz의 상위 스코프는
// 즉시 실행 함수이므로 this는 즉시 실행 함수의 this를 가리킨다.
(function () {
  const baz = () => () => console.log(this);
  baz()();
}).call({ a: 1 }); // { a: 1 }

// increase 프로퍼티에 할당한 화살표 함수의 상위 스코프는 전역이다.
// 따라서 increase 프로퍼티에 할당한 화살표 함수의 this는 전역 객체를 가리킨다.
const counter = {
  num: 1,
  increase: () => ++this.num
};

console.log(counter.increase()); // NaN
```

- 화살표 함수는 함수 자체의 this 바인딩이 없기 때문에 Function.prototype.call, Function.prototype.apply, Function.prototype.bind 메소드를 사용하여도 화살표 함수 내부의 this를 교체할 수 없다.
- 메소드를 화살표 함수로 정의하는 것은 피해야 한다.

### 3.4 super

- 화살표 함수는 함수 자체의 super 바인딩이 없다. 따라서 화살표 함수 내부에서 super를 참조하면 상위 스코프의 super를 참조한다.

```javascript
class Base {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return `Hi! ${this.name}`;
  }
}

class Derived extends Base {
  /*
  super 키워드는 ES6 메소드 내에서만 사용 가능하다.
  화살표 함수는 ES6 메소드가 아니지만 함수 자체의 super 바인딩이 없으므로 에러가 발생하지 않고 상위 스코프의 super를 참조한다.
  화살표 함수 sayHi의 상위 스코프는 constructor이다. 따라서 화살표 함수 sayHi의 super는 constructor의 super를 가리킨다.
  */
  sayHi = () => `${super.sayHi()} how are you doing?`;
}

const derived = new Derived('Lee');
console.log(derived.sayHi()); // Hi! Lee how are you doing?
```

### 3.5 arguments

- 화살표 함수는 함수 자체의 arguments 바인딩이 없다. 따라서 화살표 함수 내부에서 arguments를 참조하면 상위 스코프의 arguments를 참조한다.

```javascript
(function () {
  // 화살표 함수는 함수 자체의 arguments 바인딩이 없다.
  // 중첩 함수 foo의 상위 스코프는 즉시 실행 함수이다.
  // 따라서 화살표 함수 foo의 arguments는 즉시 실행 함수의 arguments를 가리킨다.
  const foo = () => console.log(arguments); // [Arguments] { '0': 1, '1': 2 }
  foo(3, 4);
}(1, 2));

// 전역 함수 foo의 상위 스코프는 전역이다.
// 전역에는 arguments 객체가 없다. arguments 객체는 함수 내부에서만 유효하다.
const foo = () => console.log(arguments);
foo(1, 2); // ReferenceError: arguments is not defined
```

- 화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 Rest 파라미터를 사용해야 한다.

### 4. Rest 파라미터

### 4.1 기본 문법

- Rest 파라미터(Rest parameter, 나머지 매개변수)는 매개변수 이름 앞에 세개의 점 …을 붙여서 정의한 매개변수를 의미한다. Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받는다.

```javascript
function foo(...rest) {
  // 매개변수 rest는 인수들의 목록을 배열로 전달받는 Rest 파라미터이다.
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
  // 매개변수 rest에는 배열이 할당된다.
  console.log(Array.isArray(rest)); // true
}

foo(1, 2, 3, 4, 5);

function foo(param, ...rest) {
  console.log(param); // 1
  console.log(rest);  // [ 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
-----------------------------------------------------
function bar(param1, param2, ...rest) {
  console.log(param1); // 1
  console.log(param2); // 2
  console.log(rest);   // [ 3, 4, 5 ]
}

bar(1, 2, 3, 4, 5);
```

- Rest 파라미터는 이름 그대로 먼저 선언된 매개변수에 할당된 인수를 제외한 나머지 인수들이 모두 배열에 담겨 할당된다. 따라서 Rest 파라미터는 반드시 마지막 이어야 한다.
- Rest 파라미터는 단 하나만 선언할 수 있다.
- Rest 파라미터는 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티에 영향을 주지 않는다.

### 4.2 Rest 파라미터와 arguments 객체

- ES6에서는 rest 파라미터를 사용하여 가변 인자의 목록을 배열로 직접 전달받을 수 있다. 

```javascript
function sum(...args) {
  // Rest 파라미터 args에는 배열 [1, 2, 3, 4, 5]이 할당된다.
  return args.reduce((pre, cur) => pre + cur, 0);
}
console.log(sum(1, 2, 3, 4, 5)); // 15
```

- 일반 함수와 메소드는 Rest 파라미터와 arguments 객체를 모두 사용할 수 있다. 하지만 화살표 함수는 함수 자체의 arguments 객체를 갖지 않는다. 따라서 화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 Rest 파라미터를 사용해야 한다.

### 5. 매개변수 기본값

- 함수를 호출할 때 매개변수의 개수만큼 인수를 전달하는 것이 바람직하지만 그렇지 않은 경우에도 에러가 발생하지는 않는다. 이는 자바스크립트 엔진이 함수의 매개변수의 개수와 인수의 개수를 체크하지 않기 때문이다. 인수가 부족한 경우, 매개변수의 값은 undefined이다.

```javascript
function sum(x, y) {
  return x + y;
}

console.log(sum(1)); // NaN
```

- 매개변수 기본값은 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티와 arguments 객체에 영향을 주지 않는다.