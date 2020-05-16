# 25. 클래스

### 1. 클래스는 프로토타입의 문법적 설탕인가?

- 클래스는 함수이며 기존 프로토타입 기반 패턴을 클래스 기반 패턴처럼 사용할 수 있도록 하는 형식이다.
- 클래스는 생성자 함수와 매우 유사하게 동작하지만 몇가지 차이가 있다.
  1. 클래스는 new 연산자를 사용하지 않고 호출하면 에러가 발행한다. 하지만 생성자 함수는 new 연산자를 사용하지 않고 호출하면 일반 함수로서 호출된다.
  2. 클래스는 상속을 지원하는 extends와 super 키워드를 제공한다. 하지만 생성자 함수는 extends와 super 키워드를 지원하지 않는다.
  3. 클래스는 호이스팅이 발생하지 않는 것처럼 동작한다. 하지만 함수 선언문으로 정의된 생성자 함수는 함수 호이스팅이, 함수 표현식으로 정의한 생성자 함수는 변수 호이스팅이 발생한다.
  4. 클래스 내의 모든 코드에는 암묵적으로 strict 모드가 지정되어 실행되며 strict 모드를 해지할 수 없다. 하지만 생성자 함수는 암묵적으로 strict 모드가 지정되지 않는다.
  5. 클래스의 constructor, 프로토타입 메소드, 정적 메소드는 모두 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false이다. 다시 말해, 열거되지 않는다.

### 2. 클래스 정의

- 클래스는 class 키워드를 사용하여 정의한다. 클래스 이름은 생성자 함수와 마찬가지로 파스칼 케이스를 사용하는 것이 일반적이다.

- 클래스는 값으로 사용할 수 있는 일급객체이다,
  - 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
  - 변수나 자료 구조(객체, 배열 등)에 저장할 수 있다.
  - 함수의 매개 변수에게 전달할 수 있다.
  - 함수의 반환값으로 사용할 수 있다.

### 3. 클래스 호이스팅

- 클래스 선언문도 변수 선언, 함수 정의와 마찬가지로 호이스팅이 발생한다. 단, 클래스는 let, const 키워드로 선언한 변수처럼 호이스팅된다

### 4. 인스턴스 생성

- 클래스는 생성자 함수이며 new 연산자와 함께 호출되어 인스턴스를 생성한다.

### 5. 메소드

- 클래스 몸체에는 0개 이상의 메소드 만을 선언할 수 있다. 클래스 몸체에서 정의할 수 있는 메소드는 construnctor(생성자), 프로토타입 메소드, 정적 메소드 3가지가 있다.

### 5.1 constructor

- constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메소드이다. constructor는 이름을 변경할 수 없다.
- constructor는 메소드로 해석되는 것이 아니라 클래스가 평가되어 생성한 함수 객체 코드의 일부가 된다. 다시 말해, 클래스 정의가 평가되면 constructor의 기술된 동작을 하는 함수 객체가 생성된다.

### 5.2 프로토타입 메소드

- 클래스 몸체에서 정의한 메소드는 생성자 함수에 의한 객체 생성 방식과는 다르게 클래스의 prototype 프로퍼티에 메소드를 추가하지 않아도 기본적으로 프로토타입 메소드가 된다.
- 생성자 함수와 마찬가지로 클래스가 생성한 인스턴스는 프로토타입 체인의 일원이 된다.

### 5.3 정적 메소드

- 정적(static) 메소드는 인스턴스를 생성하지 않아도 호출할 수 있는 메소드를 말한다.
- 정적 메소드는 프로토타입 메소드처럼 인스턴스로 호출하지 않고 클래스로 호출한다.

### 5.4 정적 메소드와 프로토타입 메소드의 차이

1. 정적 메소드와 프로토타입 메소드는 자신이 속해 있는 프로토타입 체인이 다르다.
2. 정적 메소드는 클래스로 호출하고 프로토타입 메소드는 인스턴스로 호출한다.
3. 정적 메소드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메소드는 인스턴스 프로퍼티를 참조할 수 있다.

- 정적 메소드는 애플리케이션 전역에서 사용할 유틸리티 함수를 전역 함수로 정의하지 않고 메소드로 구조화할 때 유용하다.

### 5.5 클래스에서 정의한 메소드의 특징

1. function 키워드를 생략한 메소드 축약 표현을 사용한다.
2. 객체 리터럴과는 다르게 클래스에 메소드를 정의할 때는 콤마가 필요 없다.
3. 암묵적으로 strict 모드로 실행된다.
4. for…in 문이나 Object.keys 메소드 등으로 열거할 수 없다. 즉, 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false이다. 
5. 내부 메소드 [[Construct]]를 갖지 않는 non-constructor이다. 따라서 new 연산자와 함께 호출할 수 없다. 

### 6. 클래스의 인스턴스 생성 과정

1. 인스턴스 생성과 this 바인딩

   new 연산자와 함께 클래스를 호출하면 constructor의 내부 코드가 실행되기에 앞서 암묵적으로 빈 객체가 생성된다. 이 빈 객체가 클래스가 생성한 인스턴스이다. 

   클래스가 생성한 인스턴스는 this에 바인딩 되며 constructor 내부의 this는 클래스가 생성한 인스턴스를 가리킨다.

2. 인스턴스 초기화

   constructor의 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티 값을 초기화한다.

3. 프로토타입 / 정적 메소드 추가

   클래스 몸체에 정의한 프로토타입 메소드가 존재하면 클래스의 prototype 프로퍼티가 가리키는 프로토타입에 추가한다. 클래스 몸체에 정의한 정적 메소드가 존재하면 클래스에 추가한다.

4. 인스턴스 반환

   클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

### 7. 프로퍼티

### 7.1 인스턴스 프로퍼티

- 인스턴스 프로퍼티는 construnctor 내부에서 정의해야 한다.
- constructor 내부에서 this에 인스턴스 프로퍼티를 추가한다. 이로써 클래스가 암묵적으로 생성한 빈 객체, 즉 인스턴스에 프로퍼티가 추가되어 인스턴스가 초기화된다.

### 7.2 접근자 프로퍼티

- 접근자 프로퍼티(accessor property)는 자체적으로는 값([[Value]] 내부 슬롯)을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(accessor function)로 구성된 프로퍼티다.

### 7.3 클래스 필드 정의 제안

- 클래스 필드는 클래스 기반 객체지향 언어에서 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어이다.
- 클래스 필드를 마치 변수처럼 클래스 몸체에 this 없이 선언해야 한다.

### 7.4 private 필드 정의 제안

- constructor 내부에서 this를 통해 정의한 인스턴스 프로퍼티는 인스턴스를 통해 클래스 외부에서 언제나 참조할 수 있다. 즉, 언제나 public이다.
- Private 필드를 정의할 수 있는 새로운 표준 사양이 제안되어 있다

```
class Person {
  // private 필드 정의
  #name = '';

  constructor(name) {
    // private 필드 참조
    this.#name = name;
  }
}

const me = new Person('Lee');

// private 필드 #name은 클래스 외부에서 참조할 수 없다.
console.log(me.#name);
// SyntaxError: Private field '#name' must be declared in an enclosing class
```

- public 필드는 어디서든지 참조할 수 있지만 private 필드는 클래스 내부에서만 참조할 수 있다.

| 접근 가능성                 | public | private |
| :-------------------------- | :----: | :-----: |
| 클래스 내부                 |   ◯    |    ◯    |
| 자식 클래스 내부            |   ◯    |    ✕    |
| 클래스 인스턴스를 통한 접근 |   ◯    |    ✕    |

### 7.5 static 필드 정의 제안

```
class MyMath {
  // static public 필드 정의
  static PI = 22 / 7;

  // static private 필드 정의
  static #num = 10;

  // static 메소드
  static increment() {
    return ++MyMath.#num;
  }
}

console.log(MyMath.PI); // 3.142857142857143
console.log(MyMath.increment()); // 11
```

### 8. 상속에 의한 클래스 확장

### 8.1 클래스 상속과 생성자 함수 상속

- 상속에 의한 클래스 확장은 기존의 클래스를 상속받아 새로운 클래스를 확장(extends)하여 정의하는 것이다.

![25-7](https://poiemaweb.com/assets/fs-images/25-7.png)

- 클래스는 상속을 통해 다른 클래스를 확장할 수 있는 문법인 extends 키워드가 기본적으로 제공된다

### 8.2 extends 키워드

```
// 수퍼(파생/부모) 클래스
class Base {}

// 서브(파생/자식) 클래스
class Derived extends Base {}
```

![25-10](https://poiemaweb.com/assets/fs-images/25-10.png)

- 클래스도 프로토타입을 통해 상속관계를 구현한다.

### 8.3 동적 상속

- extends 키워드는 생성자 함수를 상속받아 클래스를 확장할 수도 있다. 단, extends 키워드 앞에는 반드시 클래스가 와야 한다.

```
// 생성자 함수
function Base(a) {
  this.a = a;
}

// 생성자 함수를 상속받는 서브 클래스
class Derived extends Base {}

const derived = new Derived(1);
console.log(derived); // Derived {a: 1}
```

- extends 키워드 다음에는 클래스뿐만이 아니라 [[Construct]] 내부 메소드를 갖는 함수 객체를 반환하는 모든 표현식을 사용할 수 있다. 이를 통해 동적으로 상속받을 대상을 결정할 수 있다.

### 8.4 서브 클래스의 constructor

- 서브 클래스에 constructor를 생략하면 클래스에 아래와 같이 디폴트 constructor가 암묵적으로 정의된다.

```
// 수퍼 클래스
class Base {
  constructor() {}
}

// 서브 클래스
class Derived extends Base {
  constructor() { super(); }
}

const derived = new Derived();
console.log(derived); // Derived {}
```

### 8.5 super 키워드

- super 키워드는 함수처럼 호출할 수도 있고 this와 같이 식별자처럼 참조할 수 있는 특수한 키워드이다. super는 아래와 같이 동작한다.
  - super를 호출하면 수퍼 클래스의 constructor(super-constructor)를 호출한다.
  - super를 참조하면 수퍼 클래스의 메소드를 호출할 수 있다.
- Super 호출
  - super를 호출하면 수퍼 클래스의 constructor(super-constructor)를 호출한다.
  - 수퍼 클래스의 constructor 내부에서 추가한 프로퍼티를 그대로 갖는 인스턴스를 생성한다면 서브 클래스의 constructor를 생략할 수 있다. 이때 new 연산자와 함께 서브 클래스를 호출하면서 전달한 인수는 모두 서브 클래스에 암묵적으로 정의된 디폴트 constructor의 super 호출을 통해 수퍼 클래스의 constructor에게 전달된다.

```
// 수퍼 클래스
class Base {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}

// 서브 클래스
class Derived extends Base {
  // 아래와 같이 암묵적으로 디폴트 constructor가 정의된다.
  // constructor(...args) { super(...args); }
}

const derived = new Derived(1, 2);
console.log(derived); // Derived {a: 1, b: 2}
```

- super를 호출할 때 주의 사항

  1. 서브 클래스에서 constructor를 생략하지 않는 경우, 서브 클래스의 constructor에서는 반드시 super를 호출해야 한다.
  2. 서브 클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없다.
  3. super는 반드시 서브 클래스의 constructor에서만 호출한다. 서브 클래스가 아닌 클래스 또는 함수에서 호출하면 에러를 발생시킨다.

- super 참조

  - 메소드 내에서 super를 참조하면 수퍼 클래스의 메소드를 호출할 수 있다.

  1. 서브 클래스의 프로토타입 메소드 내에서 super.prop는 수퍼 클래스의 프로토타입 메소드 prop를 가리킨다.

  2. 서브 클래스의 정적 메소드 내에서 super.prop는 수퍼 클래스의 정적 메소드 prop를 가리킨다.

### 8.6 상속 클래스의 인스턴스 생성 과정

```
// 수퍼 클래스
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }

  toString() {
    return `width = ${this.width}, height = ${this.height}`;
  }
}

// 서브 클래스
class ColorRectangle extends Rectangle {
  constructor(width, height, color) {
    super(width, height);
    this.color = color;
  }

  // 메소드 오버라이딩
  toString() {
    return super.toString() + `, color = ${this.color}`;
  }
}

const colorRectangle = new ColorRectangle(2, 4, 'red');
console.log(colorRectangle); // ColorRectangle {width: 2, height: 4, color: "red"}

// 상속을 통해 getArea 메소드를 호출
console.log(colorRectangle.getArea()); // 8
// 오버라이딩된 toString 메소드를 호출
console.log(colorRectangle.toString()); // width = 2, height = 4, color = red
```

![25-11](https://poiemaweb.com/assets/fs-images/25-11.png)

1. 서브 클래스의 super 호출

- 자바스크립트 엔진은 클래스를 평가할 때, 수퍼 클래스와 서브 클래스를 구분하기 위해 “base” 또는 “derived”를 값으로 갖는 내부 슬롯[[ConstructorKind]]를 갖는다. 
- 서브 클래스는 자신이 직접 인스턴스를 생성하지 않고 인스턴스 생성을 수퍼 클래스에게 위임한다. 이것이 바로 서브 클래스의 constructor에서 반드시 super를 호출해야하는 이유이다.
- 서브 클래스(ColorRectangle)가 new 연산자와 함께 호출되면 서브 클래스 constructor 내부의 super 키워드가 함수처럼 호출된다. super를 호출하면 수퍼 클래스의 constructor(super-constructor)가 호출된다. 

2. 수퍼 클래스의 인스턴스 생성과 this 바인딩

- 수퍼 클래스의 constructor 내부의 코드가 실행되기 이전에 암묵적으로 빈 객체를 생성한다. 이 빈 객체가 바로 (아직 완성되지는 않았지만) 클래스가 생성한 인스턴스이다. 그리고 암묵적으로 생성된 빈 객체, 즉 인스턴스는 this에 바인딩된다. 따라서 수퍼 클래스의 constructor 내부의 this는 생성된 인스턴스를 가리킨다.

3. 수퍼 클래스의 인스턴스 초기화

- 수퍼 클래스의 constructor가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화한다.

4. 수퍼 클래스의 프로토타입 / 정적 메소드 추가

- 수퍼 클래스 몸체에 프로토타입 메소드가 존재하면 수퍼 클래스의 prototype 프로퍼티가 가리키는 객체에 메소드로 추가된다. 수퍼 클래스 몸체에 정적 메소드가 존재하면 클래스에 메소드로 추가된다.

5. 서브 클래스 constructor로의 복귀와 this 바인딩

- super의 호출이 종료되고 컨트롤이 서브 클래스 constructor로의 복귀한다. 이때 super가 반환한 인스턴스가 this에 바인딩된다. 이처럼 서브 클래스는 별도의 인스턴스를 생성하지 않고 super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용한다.
- super가 호출되지 않으면 인스턴스가 생성되지 않으며 this 바인딩도 할 수 없다. 서브 클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없는 이유는 바로 이 때문이다.

6. 서브 클래스의 인스턴스 초기화

- super 호출 이후, 서브 클래스의 constructor에 기술되어 있는 인스턴스 초기화가 실행된다. 즉, this에 바인딩되어 있는 인스턴스에 프로퍼티를 추가하고 constructor가 인수로 전달받은 초기값으로 인스턴스의 프로퍼티를 초기화한다.

7. 인스턴스 반환

- 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

### 8.7 표준 빌트인 생성자 함수 확장

- extends 키워드 다음에는 클래스뿐만이 아니라 [[Construct]] 내부 메소드를 갖는 함수 객체를 반환하는 모든 표현식을 사용할 수 있다. String, Number, Array와 같은 표준 빌트인 객체도 [[Construct]] 내부 메소드를 갖는 생성자 함수이므로 extends 키워드를 사용하여 확장할 수 있다.

```
​``` c
// Array 생성자 함수를 상속받아 확장한 MyArray
class MyArray extends Array {
  // 중복된 배열 요소를 제거하고 반환한다: [1, 1, 2, 3] => [1, 2, 3]
  uniq() {
    return this.filter((v, i, self) => self.indexOf(v) === i);
  }

  // 모든 배열 요소의 평균을 구한다: [1, 2, 3] => 2
  average() {
    return this.reduce((pre, cur) => pre + cur, 0) / this.length;
  }
}

const myArray = new MyArray(1, 1, 2, 3);
console.log(myArray); // MyArray(4) [1, 1, 2, 3]

// MyArray.prototype.uniq 호출
console.log(myArray.uniq()); // MyArray(3) [1, 2, 3]
// MyArray.prototype.average 호출
console.log(myArray.average()); // 1.75
​```
```

