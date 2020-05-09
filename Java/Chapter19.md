# 19. 프로토타입

### 1. 객체지향 프로그래밍

- 객체지향 프로그래밍은 실체를 인식하는 철학적 사고를 프로그래밍에 접목하려는 시도에서 시작한다. 실체는 특징이나 성질을 나타내는 속성 (attribute, property)을 가지고 있고, 이를 통해 실체를 인식하거나 구별할 수 있다.

- 다양한 속성 중에서 프로그램에 필요한 속성만을 간추려 내어 표현하는것을 추상화라 한다.
- 속성을 통해 여러 개의 값을 하나의 단위로 구성한 복합적인 자료 구조를 객체라한다.
- 객체지향 프로그래밍은 객체의 상태를 나타내는 데이터와 상태 데이터를 조작할 수 있는 동작을 하나의 논리적인 단위로 묶어 생각하며 이러한 복합적인 자료 구조를 가지고 있다.

### 2. 상속과 프로토타입

- 상속은 어떤 객체의 프로퍼티 또는 메소드를 다른 객체가 상속 받아 그대로 사용할 수 있는 것을 말한다.

- 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거한다. 중복을 제거하는 방법은 기존의 코드를 적극적으로 재사용하는 것이다.

  ```
  // 생성자 함수
  function Circle(radius) {
    this.radius = radius;
  }
  
  // Circle 생성자 함수가 생성한 모든 인스턴스가 공유할 수 있도록 getArea 메소드를 프로토타입에 추가한다.
  // 프로토타입은 Circle 생성자 함수의 prototype 프로퍼티에 바인딩되어 있다.
  Circle.prototype.getArea = function () {
    return Math.PI * Math.pow(this.radius, 2);
  };
  
  // 인스턴스 생성
  const circle1 = new Circle(1);
  const circle2 = new Circle(2);
  
  // Circle 생성자 함수가 생성한 모든 인스턴스는 부모 객체의 역할을 하는
  // 프로토타입 Circle.prototype로부터 getArea 메소드를 상속받는다.
  // 즉, Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메소드를 공유한다.
  console.log(circle1.getArea === circle2.getArea); // true
  
  console.log(circle1.getArea()); // 3.141592653589793
  console.log(circle2.getArea()); // 12.566370614359172
  ```

  

![19-2](https://poiemaweb.com/assets/fs-images/19-2.png)

- Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 즉 상위(부모) 객체 역할을 하는 Circle.prototype의 모든 프로퍼티와 메소드를 상속 받는다.

### 3. 프로토타입 객체

- 객체 지향 프로그래밍의 근간을 이루는 객체간 상속(inheritance)을 구현하기 위해 사용된다. 
- 객체가 생성될 때 객체 생성 방식에 따라 프로토타입이 결정되고 [[Prototype]]에 저장된다.

### 3.1 proto 접근자 프로퍼티

- 모든 객체는 __proto__ 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있다.
  1. proto 는 접근자 프로퍼티이다.
  2. 접근자 프로퍼티는 상속을 통해 사용된다
     - 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype의 프로퍼티이다.
  3. 접근자 프로퍼티를 통해 프로토타입에 접근하는이유
     - 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위함이다.
  4. 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 비추천이다.
     - 접근자 프로퍼티 대신 [Object.getPrototypeOf 메소드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)를, 프로토타입을 교체하고 싶은 경우, [Object.setPrototypeOf 메소드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf)를 사용할 것을 권장한다.

### 3.2 함수 객체의 prototype 프로퍼티

- 함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다.
- prototype 프로퍼티는 생성자 함수가 생성할 객체(인스턴스)의 프로토타입을 가리킨다
- **모든 객체가 가지고 있는(엄밀히 말하면 Object.prototype로부터 상속받은) __proto__ 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다.** 하지만 이들 프로퍼티를 사용하는 주체가 다르다.

| 구분                      | 소유      | 값                | 사용 주체   | 사용 목적                                                    |
| :------------------------ | :-------- | :---------------- | :---------- | :----------------------------------------------------------- |
| __proto__ 접근자 프로퍼티 | 모든 객체 | 프로토타입의 참조 | 모든 객체   | 객체가 자신의 프로토타입에 접근 또는 교체하기 위해 사용      |
| prototype 프로퍼티        | 함수 객체 | 프로토타입의 참조 | 생성자 함수 | 생성자 함수가 자신이 생성할 객체(인스턴스)의 프로토타입을 할당하기 위해 사용 |

### 3.3 프로토타입의 constructor 프로퍼티와 생성자 함수

- 모든 프로토타입은 constructor 프로퍼티를 갖는다. 이 constructor 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다. 이 연결은 생성자 함수가 생성될 때, 즉 함수 객체가 생성될 때 이루어진다. 

#### 4. 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

```
// obj 객체를 생성한 생성자 함수는 Object이다.
const obj = new Object();
console.log(obj.constructor === Object); // true

// add 함수 객체를 생성한 생성자 함수는 Function이다.
const add = new Function('a', 'b', 'return a + b');
console.log(add.constructor === Function); // true

// 생성자 함수
function Person(name) {
  this.name = name;
}

// me 객체를 생성한 생성자 함수는 Person이다.
const me = new Person('Lee');
console.log(me.constructor === Person); // true
```

- 리터럴 표기법에 의해 생성된 객체도 상속을 위해 프로토타입이 필요하다.
- 프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍으로 존재한다.

| 리터럴 표기법      | 생성자 함수 | 프로토타입         |
| :----------------- | :---------- | :----------------- |
| 객체 리터럴        | Object      | Object.protptype   |
| 함수 리터럴        | Function    | Function.prototype |
| 배열 리터럴        | Array       | Array.prototype    |
| 정규 표현식 리터럴 | RegExp      | RegExp.protptype   |

### 5. 프로토타입의 생성 시점

- 프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다.

### 5.1 사용자 정의 생성자 함수와 프로토타입 생성 시점

- 생성자 함수로서 호출할 수 있는 함수, 즉 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.
- 생성자 함수로서 호풀할 수 없는 함수, non-constructor는 포로토타입이 생성되지 않는다.

### 5.2 빌트인 생성자 함수와 프로토타입 생성 시점

- 모든 빌트인 생성자 함수는 전역 객체가 생성되는 시점에 생성된다. 생성된 프로토타입은 빌트인 생성자 함수의 프로토타입 프로퍼티에 바인딩 된다.

### 6. 객체 생성 방식과 프로토타입의 결정

### 6.1 객체 리터럴에 의해 생성된 객체의 프로토타입

- 객체 리터럴에 의해 생성되는 객체의 프로토타입은 Object.prototype이다. 

### 6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입

- 명시적으로 Object 생성자 함수를 호출하여 객체를 생성하면 빈 객체가 생성된다. Object 생성자 함수를 호출하면 객체 리터럴과 마찬가지로 [추상 연산 ObjectCreate를 호출](https://www.ecma-international.org/ecma-262/10.0/#sec-object-value)한다. 이때 추상 연산 ObjectCreate에 전달되는 프로토타입은 Object.prototype이다.
- 객체 리터럴과 Object 생성자 함수에 의한 객체 생성 방식의 차이는 프로퍼티를 추가하는 방식에 있다. 객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가하지만 Object 생성자 함수 방식은 일단 빈 객체를 생성한 이후 프로퍼티를 추가해야 한다.

### 6.3 생성자 함수에 의해 생성된 객체의 프로토타입

- new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하면 다른 객체 방식과 마찬가지로 [추상 연산 ObjectCreate를 호출](https://www.ecma-international.org/ecma-262/10.0/#sec-ordinarycreatefromconstructor)한다. 이때 추상 연산 ObjectCreate에 전달되는 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩되어 있는 객체이다.

### 7. 프로토타입 체인

- 자바스크립트는 객체의 프로퍼티(메소드 포함)에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. 이것을 프로토타입 체인이라 한다. 프로토타입 체인은 자바스크립트가 객체 지향 프로그래밍의 상속을 구현하는 메커니즘이다.
- 프로토타입 체인의 최상위에 위치하는 객체는 언제나 Object.prototype이다. 따라서 모든 객체는 Object.prototype을 상속받는다. 

### 8. 캡슐화

- 정보의 일부를 외부에 감추어 은닉하는 것을 말한다

### 9. 오버라이딩과 프로퍼티 쉐도잉

![19-19](https://poiemaweb.com/assets/fs-images/19-19.png)

- 오버라이딩 : 상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의하여 사용하는 방식이다.
- 프로퍼티 쉐도잉 : 상속 관계에 의해 프로퍼티가 가려지는 현상을 말한다.

### 10.  프로토타입의 교체

### 10.1 생성자 함수에 의한 포로토타입의 교체

```
const Person = (function () {
  function Person(name) {
    this.name = name;
  }

  // ① 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
  Person.prototype = {
    sayHello() {
      console.log(`Hi! My name is ${this.name}`);
    }
  };

  return Person;
}());

const me = new Person('Lee');
```

![19-20](https://poiemaweb.com/assets/fs-images/19-20.png)

### 10.2 인스턴스에 의한 프로토타입의 교체

- 인스턴스의 접근자 프로퍼티를 통해 프로토타입을 교체할 수 있다.
- 접근자 프로퍼티를 통해 프로토타입을 교체하는 것은 이미 생성된 객체의 프로토타입을 교체하는 것이다.

### 11. Instanced 연산자

- Instanced 연산자는 이항 연산자로서 좌변에 객체를 가리키는 식별자, 우변에 생성자 함수를 가리키는 식별자를 피연산자로 받는다
- instanceof 연산자는 좌변 피연산자의 프로토타입 체인 상에 우변의 피연산자, 즉 생성자 함수의 prototype 프로퍼티에 바인딩된 객체가 존재하는 지 검색한다.

### 12. 직접상속

### 12.1 Object.create에 의한 직접 상속

- Object.create 메소드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성한다.

- Object.create 메소드의 첫번째 매개변수에는 생성할 객체의 프로토타입으로 지정할 객체를 전달한다. 두번째 매개변수에는 생성할 객체의 프로퍼티를 갖는 객체를 전달한다.

- Object.create 메소드는 첫번째 매개변수에 전달한 객체의 프로토타입 체인에 속하는 객체를 생성한다. 즉, 객체를 생성하면서 직접적으로 상속을 구현하는 것이다.

  장점

  1. new 연산자가 없이도 객체를 생성할 수 있다.
  2. 객체 리터럴에 의해 생성된 객체도 특정 객체를 상속받을 수 있다.
  3. 프로토타입을 지정하면서 객체를 생성할 수 있다.

### 12.2 객체 리터럴 내부에서 proto에 의한 직접 상속

- ES6에서는 객체 리터럴 내부에서 __proto__ 접근자 프로퍼티를 사용하여 직접 상속을 구현할 수 있다.

### 13. 정적 프로퍼티/메소드

- 정적(static) 프로퍼티/메소드는 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출할 수 있는 프로퍼티/메소드를 말한다. 

### 14. 프로퍼티 존재 확인

- in 연산자는 객체 내에 프로퍼티가 존재하는지 여부를 확인한다.

### 15. 프로퍼티 열거

### 15.1 for...in 문

- 객체의 모든 프로퍼티를 순회하며 열거(enumeration)하려면 for…in 문을 사용한다.
- for…in 문은 in 연산자처럼 순회 대상 객체의 프로퍼티 뿐만 아니라 상속받은 프로토타입의 프로퍼티까지 열거한다. 

### 15.2 Object.keys/values/entries 메소드

- 객체 자신의 프로퍼티만을 열거하기 위해서는 for…in 문을 사용하는 것 보다 Object.keys/values/entries 메소드를 사용하는 것이 좋다.