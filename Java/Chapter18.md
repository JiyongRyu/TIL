# 18. 함수와 일급 객체

### 1. 일급 객체

- 4가지 조건을 모두 만족해야한다
  1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
  2. 변수나 자료 구조(객체, 배열 등)에 저장할 수 있다.
  3. 함수의 매개 변수에게 전달할 수 있다.
  4. 함수의 결과값으로 반환할 수 있다.

- 함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미이다.

### 2. 함수 객체의 프로퍼티

### 2.1 arguments 프로퍼티

- 함수 객체의 arguments 프로퍼티 값은 arguments 객체이다.
- arguments 객체는 함수 호출 시 전달된 인수(argument)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체(array-like object)이며 함수 내부에서 지역 변수처럼 사용된다. 함수 외부에서는 참조할 수 없다.
- 모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관된다.
- arguments 객체는 매개변수 개수를 확정할 수 없는 가변인자 함수를 구현할 때 유용하게 사용된다.
- 유사 배열 객체 : length 프로퍼티를 가진 객체로 for 문으로 순회할 수 있는 객체를 말한다.

### 2.2 caller 프로퍼티

-  비표준 프로퍼티

### 2.3 length 프로퍼티

- 함수 객체의 length 프로퍼티는 함수 정의 시 선언한 매개변수의 개수를 가리킨다.
- arguments 객체의 length 프로퍼티와 함수 객체의 length 프로퍼티의 값은 다를 수 있으므로 주의하여야 한다.

### 2.4 name 프로퍼티

- 함수 객체의 name 프로퍼티는 함수 이름을 나타낸다.

### 2.5 __proto__ 접근자 프로퍼티

- _ _ proto _ _ 프로퍼티는  [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티이다. 

### 2.6 prototype 프로퍼티

- prototype 프로퍼티는 함수 객체만이 소유하는 프로퍼티이다. 
- prototype 프로퍼티는 함수가 객체를 생성하는 생성자 함수로 사용될 때, 생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가리킨다.

- 프로토타입 체인의 최상위에 위치하는 객체는 언제나 Object.prototype이다. 따라서 모든 객체는 Object.prototype을 상속받는다. **Object.prototype을 프로토타입 체인의 종점(end of prototype chain)**이라 한다. Object.prototype의 프로토타입, 즉 [[Prototype]] 내부 슬롯의 값은 null이다.
- 프로토타입 체인의 종점인 Object.prototype에서도 프로퍼티를 검색할 수 없는 경우, undefined를 반환한다.
- 프로토타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘이다.
- 프로퍼티가 아닌 식별자는 스코프 체인에서 검색한다. 스코프 체인은 식별자 검색을 위한 메커니짐이라고 할수 있다.

### 8. 캡슐화

- 정보의 일부를 외부에 감추어 은닉하는 것을 말한다.

### 9. 오버라이딩과 프로퍼티 쉐도잉

```
const Person = (function () {
  // 생성자 함수
  function Person(name) {
    this.name = name;
  }

  // 프로토타입 메소드
  Person.prototype.sayHello = function () {
    console.log(`Hi! My name is ${this.name}`);
  };

  // 생성자 함수를 반환
  return Person;
}());

const me = new Person('Lee');

// 인스턴스 메소드
me.sayHello = function () {
  console.log(`Hey! My name is ${this.name}`);
};

// 인스턴스 메소드가 호출된다. 프로토타입 메소드는 인스턴스 메소드에 의해 가려진다.
me.sayHello(); // Hey! My name is Lee
```

![19-19](https://poiemaweb.com/assets/fs-images/19-19.png)