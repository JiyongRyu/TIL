# 34. 이터러블

### 1. 이터레이션 프로토콜

- 이터레이션 프로토콜(iteration protocol)은 순회 가능한(iterable) 데이터 컬렉션(자료 구조)을 만들기 위해 ECMAScript 사양에 정의하여 미리 약속한 규칙이다.

- ES6에서 도입된 이터레이션 프로토콜에는 이터러블 프로토콜과 이터레이터 프로토콜이 있다.

  - 이터러블 프로토콜(iterable protocol)

    Well-known Symbol인 Symbol.iterator를 프로퍼티 키로 사용한 메소드를 직접 구현하거나 프로토타입 체인에 의한 상속을 통해 소유하고, Symbol.iterator 메소드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터(iterator)를 반환한다. 이러한 규약을 이터러블 프로토콜이라 하며 **이터러블 프로토콜을 준수한 객체를 이터러블(iterable)라 한다. 이터러블은 for…of 문으로 순회할 수 있으며 스프레드 문법과 디스트럭처링 할당의 대상으로 사용할 수 있다.**

  - 이터레이터 프로토콜(iterator protocol)

    이터러블의 Symbol.iterator 메소드를 호출하면 이터레이터 프로토콜을 준수한 **이터레이터(iterator)**를 반환한다. 이터레이터는 next 메소드를 소유하며 next 메소드를 호출하면 이터러블을 순회하며 value와 done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다. 이러한 규약을 이터레이터 프로토콜이라 하며 이터레이터 프로토콜을 준수한 객체를 이터레이터(iterator)라 한다. 이터레이터는 이터러블의 요소를 탐색하기 위한 포인터 역할을 한다.

### 1.1 이터러블

- 이터러블 프로토콜을 준수한 객체를 이터러블(iterable)이라 한다. 즉, 이터러블은 Symbol.iterator을 프로퍼티 키로 사용한 메소드를 직접 구현하거나 프로토타입 체인에 의해 상속한 객체를 말한다.

### 1.2 이터레이터

- 이터러블의 Symbol.iterator 메소드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터(iterator)를 반환한다. 이터러블의 Symbol.iterator 메소드가 반환한 이터레이터는 next 메소드를 갖는다. 이터레이터의 next 메소드는 이터러블의 각 요소를 순회하기 위한 포인터의 역할을 한다. 즉, next 메소드를 호출하면 이터러블을 순차적으로 한 단계씩 순회하며 순회 결과를 나타내는 **이터레이터 리절트 객체(Iterator result object)**를 반환한다. 이터레이터의 next 메소드가 반환하는 이터레이터 리절트 객체의 value 프로퍼티는 현재 순회 중인 이터러블의 값을 나타내며 done 프로퍼티는 이터러블의 순회 완료 여부를 나타낸다.

### 2. 빌트인 이터러블

| 빌트인 이터러블 | 프로퍼티 키가 Symbol.iterator인 메소드                       |
| :-------------- | :----------------------------------------------------------- |
| Array           | Array.prototype[Symbol.iterator]                             |
| String          | String.prototype[Symbol.iterator]                            |
| Map             | Map.prototype[Symbol.iterator]                               |
| Set             | Set.prototype[Symbol.iterator]                               |
| TypedArray      | TypedArray.prototype[Symbol.iterator]                        |
| arguments       | arguments[Symbol.iterator]                                   |
| DOM 컬렉션      | NodeList.prototype[Symbol.iterator], HTMLCollection.prototype[Symbol.iterator] |

### 3. for…of 문

- for…of 문은 이터러블을 순회하면서 이터러블의 요소를 변수에 할당한다. 

### 4. 이터러블과 유사 배열 객체

- 유사 배열 객체(Array-like Object)는 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다. 유사 배열 객체는 length 프로퍼티를 갖기 때문에 for 문으로 순회할 수 있다.

### 5. 이터레이션 프로토콜의 필요성

- 다양한 데이터 소스가 하나의 순회 방식을 갖도록 규정하여 데이터 소비자가 효율적으로 다양한 데이터 소스를 사용할 수 있도록 데이터 소비자와 데이터 소스를 연결하는 인터페이스의 역할을 한다.