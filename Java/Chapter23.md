# 23. 실행 컨텍스트

### 1. 소스 코드의 타입

| 소스 코드의 타입         | 설명                                                         |
| :----------------------- | :----------------------------------------------------------- |
| 전역 코드(global code)   | 전역에 존재하는 소스 코드를 말한다. 전역에 정의된 함수, 클래스 등의 내부 코드는 포함되지 않는다. |
| 함수 코드(function code) | 함수 내부에 존재하는 소스 코드를 말한다. 함수 내부에 중첩된 함수, 클래스 등의 내부 코드는 포함되지 않는다. |
| eval 코드(eval code)     | 빌트인 전역 함수인 eval 함수에 인수로 전달되어 실행되는 소스 코드를 말한다. |
| 모듈 코드(module code)   | 모듈 내부에 존재하는 소스 코드를 말한다. 모듈 내부의 함수, 클래스 등의 내부 코드는 포함되지 않는다. |

### 2. 소스 코드의 평가와 실행

- 소스 코드 평가 과정에서는 실행 컨텍스트를 생성하고 변수, 함수 등의 선언문 만을 먼저 실행하여 생성된 변수나 함수 식별자를 키로 실행 컨텍스트가 관리하는 스코프(렉시컬 환경의 환경 레코드)에 등록한다.
- 소스 코드의 평가 과정이 끝나면 비로소 선언문을 제외한 소스 코드가 순차적으로 실행되기 시작한다. 즉, 런타임에 시작된다. 이때 소스 코드 실행에 필요한 정보, 즉 변수나 함수의 참조를 실행 컨텍스트가 관리하는 스코프에서 취득한다. 그리고 변수 값의 변경과 같은 소스 코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록된다.

### 3. 실행 컨텍스트의 역할

1. 전역 코드 평가

   먼저 전역 코드를 실행하기에 앞서 전역 코드 평가 과정을 거치며 전역 코드 실행을 위한 준비를 한다. 소스 코드 평가 과정에서는 선언문 만을 먼저 실행한다. 

2. 전역 코드 실행

   전역 코드의 평가가 끝나면 런타임이 시작되어 전역 코드가 순차적으로 실행되기 시작한다. 이때 전역 변수에 값이 할당되고 함수가 호출된다. 함수가 호출되면 순차적으로 실행되던 전역 코드의 실행을 일시 중단하고 코드 실행 순서를 변경하여 함수 내부로 진입한다.

3. 함수 코드 평가

   코드 실행 순서가 변경되어 함수 내부로 진입하면 함수 내부의 문들을 실행하기에 앞서 함수 코드 평가 과정을 거치며 함수 코드 실행을 위한 준비를 한다. 이때 매개 변수와 지역 변수 선언문이 먼저 실행되고 그 결과 생성된 매개 변수와 지역 변수가 실행 컨텍스트가 관리하는 지역 스코프에 등록된다. 또한 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체가 생성되어 지역 스코프에 등록되고 this 바인딩도 결정된다.

4. 함수 코드 실행

   함수 코드의 평가가 끝나면 런타임이 시작되어 함수 코드가 순차적으로 실행되기 시작한다. 

- 실행 컨텍스트(execution context)는 소스 코드를 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.
- 실행 컨텍스트는 식별자(변수, 함수, 클래스 등의 이름)를 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 매커니즘으로 모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다.
- 식별자와 스코프는 실행 컨텍스트의 렉시컬 환경으로 관리하고 코드 실행 순서는 실행 컨텍스트 스택으로 관리한다.

### 4. 실행 컨텍스트 스택

- 자바스크립트 엔진은 먼저 전역 코드를 평가하여 전역 실행 컨텍스트를 생성한다. 그리고 함수가 호출되면 함수 코드를 평가하여 함수 실행 컨텍스트를 생성한다.
- 생성된 실행 컨텍스트는 스택 자료구조로 관리된다. 이를 실행 컨텍스트 스택이나 콜 스택이라고 부른다.
- 실행 컨텍스트 스택은 코드의 실행 순서를 관리한다. 
-  실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 현재 실행 중인 코드의 실행 컨텍스트이다.따라서 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트를 실행 중인 실행 컨텍스트(running execution context)라 부른다.

### 5. 렉시컬 환경

- 렉시컬 환경(Lexical Environment)은 식별자와 식별자에 바인딩된 값 그리고 상위 스코프에 대한 참조를 기록하는 환경으로 실행 컨텍스트를 구성하는 컴포넌트이다. 실행 컨텍스트 스택이 코드의 실행 순서를 관리한다면 렉시컬 환경은 스코프와 식별자를 관리한다.
- 렉시컬 환경은 객체 형태의 스코프(전역, 함수, 블록 스코프)를 생성하여 식별자를 키로 등록하고 식별자에 바인딩된 값을 관리한다. 즉, 렉시컬 환경은 스코프를 구분하여 식별자를 등록하고 관리하는 저장소 역할을 하는 렉시컬 스코프의 실체이다.
- 실행 컨텍스트는 LexicalEnvironment 컴포넌트와 VariableEnvironment 컴포넌트로 구성된다.
- 렉시컬 환경은 두개의 컴포넌트로 구성된다

![23-8](https://poiemaweb.com/assets/fs-images/23-8.png)

1. 환경 레코드(Environment Record)

   스코프에 포함된 식별자를 등록하고 등록된 식별자에 바인딩된 값을 관리하는 저장소이다. 환경 레코드는 소스 코드의 타입에 따라 내용에 차이가 있다.

2. 외부 렉시컬 환경에 대한 참조(Outer Lexical Environment Reference)

   외부 렉시컬 환경에 대한 참조는 상위 스코프를 가리킨다. 이때 상위 스코프란 외부 렉시컬 환경, 즉 해당 실행 컨텍스트를 생성한 소스 코드를 포함하는 상위 코드의 렉시컬 환경을 말한다. 외부 렉시컬 환경에 대한 참조를 통해 단방향 링크드 리스트인 스코프 체인을 구현한다.

### 6. 실행 컨텍스트의 생성고 식별자 검색 과정

```
var x = 1;
const y = 2;

function foo (a) {
  var x = 3;
  const y = 4;

  function bar (b) {
    const z = 5;
    console.log(a + b + x + y + z);
}
  bar(10);
}

foo(20); // 42
```

### 6.1 전역 객체 생성

- 전역 객체는 전역 코드가 평가되기 이전에 생성된다. 이때 전역 객체에는 빌트인 전역 프로퍼티와 빌트인 전역함수 그리고 표준 빌트인 객체가 추가된다.

### 6.2 전역 코드 평가

1. 전역 실행 컨텍스트 생성 

2. 전역 렉시컬 환경 생성 

    2.1. 전역 환경 레코드 생성   

   ​	 2.1.1. 객체 환경 레코드 생성    

   ​	 2.1.2. 선언적 환경 레코드 생성   

   ​	 2.1.3. this 바인딩  

   2.2. 외부 렉시컬 환경에 대한 참조 할당

![23-9](https://poiemaweb.com/assets/fs-images/23-9.png)

- 전역 실행 컨텍스트 생성

  먼저 비어있는 전역 실행 컨텍스트를 생성하여 실행 컨텍스트 스택에 푸시한다. 

- 전역 렉시컬 환경 생성

  전역 렉시컬 환경(Global Lexical Environment)을 생성하고 전역 실행 컨텍스트의 LexicalEnvironment 컴포넌트와 VariableEnvironment 컴포넌트에 바인딩한다.

- 전역 환경 레코드 생성

  전역 렉시컬 환경을 구성하는 컴포넌트인 전역 환경 레코드(Global Environment Record)는 전역 변수를 관리하는 전역 스코프 그리고 전역 객체의 빌트인 전역 프로퍼티와 빌트인 전역 함수 그리고 표준 빌트인 객체를 제공한다.

  var 키워드로 선언한 전역 변수와 ES6의 let, const 키워드로 선언한 전역 변수를 구분하여 관리하기 위해 전역 스코프 역할을 하는 전역 환경 레코드는 객체 환경 레코드(Object Environment Record)와 선언적 환경 레코드(Declarative Environment Record)로 구성되어 있다.

- 객체 환경 레코드 생성

  전역 환경 레코드를 구성하는 컴포넌트인 객체 환경 레코드는 BindingObject라고 부르는 객체와 연결된다.

  전역 코드 평가 과정에서 var 키워드로 선언한 전역 변수와 함수 선언문으로 정의된 전역 함수는 전역 환경 레코드의 객체 환경 레코드에 연결된 BindingObject를 통해 전역 객체의 프로퍼티와 메소드가 된다.

- 선언적 환경 레코드 생성

  var 키워드로 선언한 전역 변수와 함수 선언문으로 정의한 전역 함수 이외의 선언, 즉 let, const 키워드로 선언한 전역 변수(let, const 키워드로 선언한 변수에 할당한 함수 표현식 포함)는 선언적 환경 레코드에 등록되고 관리된다.

  let, const 키워드로 선언한 변수도 변수 호이스팅이 발생하는 것은 변함이 없다. 단, let, const 키워드로 선언한 변수는 런타임에 컨트롤이 변수 선언문에 도달하기 전까지 일시적 사각지대에 빠지기 때문에 참조할 수 없다.

- this 바인딩

  전역 환경 레코드의 [[GlobalThisValue]] 내부 슬롯에 this가 바인딩된다. 

- 외부 렉시컬 환경에 대한 참조 할당

  외부 렉시컬 환경에 대한 참조(Outer Lexical Environment Reference)는 현재 평가 중인 코드를 포함하는 외부 코드의 렉시컬 환경, 즉 상위 스코프를 가리킨다.

### 6.3 전역 코드 실행

- 동일한 이름의 식별자가 다른 스코프가 여러 개 존재할 수도 있다. 따라서 어느 스코프의 식별자를 참조하면 되는지 결정할 필요가 있다. 이를 식별자 결정(identifier resolution)이라 한다. 식별자 결정을 위해 식별자를 검색할 때는 실행 중인 실행 컨텍스트에서 식별자를 검색하기 시작한다. 선언된 식별자는 실행 컨텍스트의 렉시컬 환경의 환경 레코드에 등록되어 있다.
- 실행 컨텍스트의 렉시컬 환경에서 식별자를 검색할 수 없으면 외부 렉시컬 환경에 대한 참조가 가리키는 렉시컬 환경, 즉 상위 스코프로 이동하여 식별자를 검색한다. 이것이 스코프 체인의 동작 원리이다.

### 6.4 foo 함수 코드 평가

1. 함수 실행 컨텍스트 생성 

2. 함수 렉시컬 환경 생성  

   2.1. 함수 환경 레코드 생성 

   2.2. 외부 렉시컬 환경에 대한 참조 할당

    2.3. this 바인딩

![23-17](https://poiemaweb.com/assets/fs-images/23-17.png)

- 함수 실행 컨텍스트 생성

  먼저 foo 함수 실행 컨텍스트를 생성한다. 생성된 함수 실행 컨텍스트는 함수 렉시컬 환경이 완성된 다음 실행 컨텍스트 스택에 푸시된다.

- 함수 렉시컬 환경 생성

  foo 함수 렉시컬 환경(Function Lexical Environment)을 생성하고 foo 함수 실행 컨텍스트에 바인딩한다.

- 함수 환경 레코드 생성

  함수 렉시컬 환경을 구성하는 컴포넌트 중 하나인 함수 환경 레코드(Function Environment Record)는 매개 변수, arguments 객체, 함수 내에서 선언한 지역 변수와 중첩 함수를 등록하고 관리한다.

- 외부 렉시컬 환경에 대한 참조 할당

  외부 렉시컬 환경에 대한 참조에는 foo 함수 정의가 평가된 시점에 실행 중인 실행 컨텍스트의 렉시컬 환경의 참조가 할당된다.

- this 바인딩

  함수 환경 레코드의 [[ThisValue]] 내부 슬롯에 this가 바인딩된다.

### 6.5 foo 함수 코드 실행

- 이제 런타임이 시작되어 foo 함수 코드가 순차적으로 실행되기 시작한다. 매개 변수에 인수가 할당되고, 변수 할당문이 실행되어 지역 변수 x, y에 값이 할당된다. 그리고 함수 bar가 호출된다.
- 식별자 결정을 위해 실행 중인 실행 컨텍스트의 렉시컬 환경에서 식별자를 검색하기 시작한다.

### 6.6 bar 함수 코드 평가

![23-23](https://poiemaweb.com/assets/fs-images/23-23.png)

### 6.7 bar 함수 코드 실행

- 이제 런타임이 시작되어 bar 함수 코드가 순차적으로 실행되기 시작한다. 매개 변수에 인수가 할당되고, 변수 할당문이 실행되어 지역 변수 z에 값이 할당된 후 `console.log(a + b + x + y + z);`가 실행된다. 

1. 식별자 console 검색

   먼저 console 식별자를 스코프 체인에서 검색한다.

2. Log 메소드 검색

   이제 console 식별자에 바인딩된 객체, 즉 console 객체에서 log 메소드를 검색한다. 이때 console 객체의 프로토타입 체인을 통해 메소드를 검색한다. log 메소드는 상속된 프로퍼티가 아니라 console 객체가 직접 소유하는 프로퍼티이다.

3. 표현식 a + b + x + y + z의 평가

   별자는 스코프 체인, 즉 현재 실행 중인 실행 컨텍스트의 렉시컬 환경에서 시작하여 외부 렉시컬 환경에 대한 참조로 이어지는 렉시컬 환경의 연속에서 검색한다.

4. console.log 메소드 호출

   평가되어 생성한 값을 console.log 메소드에 전달하여 호출한다

### 6.8 bar 함수 코드 실행 종료

- console.log 메소드가 호출되고 종료하면 더 이상 실행할 코드가 없으므로 bar 함수 코드의 실행이 종료된다. 이때 실행 컨텍스트 스택에서 bar 함수 실행 컨텍스트가 팝되어 제거되고 foo 실행 컨텍스트가 실행 중인 실행 컨텍스트가 된다.
- 렉시컬 환경까지 즉시 소멸하는 것은 아니며 객체를 포함한 모든 값은 참조되지 않을때 메모리 공간의 확보가 해제되어 소멸한다

### 6.9 foo 함수 코드 실행 종료

### 6.10 전역 코드 실행 종료

### 7. 실행 컨텍스트와 블록 레벨 스코프

- var 키워드로 선언한 변수는 오로지 함수의 코드 블록 만을 지역 스코프로 인정하는 함수 레벨 스코프를 따른다. 하지만 let, const 키워드로 선언한 변수는 모든 코드 블록(함수, if 문, for 문, while 문, try/catch 문 등)을 지역 스코프로 인정하는 블록 레벨 스코프(block-level scope)를 따른다.
- for 문의 경우, 초기문에 let 키워드를 사용한 for 문은 반복될 때마다 새로운 렉시컬 환경을 생성한다. 