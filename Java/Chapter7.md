# 7. 연산자

- 연산자(Operator)는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산(operation) 등을 수행해 하나의 값을 만듬. 이때 연산의 대상을 피연산자(Operand)라 함.
- 피연산자는 값으로 평가될 수 있는 표현식이어야 하고 피연산자와 연산자의 조합으로 이루어진 연산자 표현식도 값으로 평가될 수 있는 표현식

```
// 산술 연산자
5 * 4 // -> 20
// 문자열 연결 연산자
'My name is ' + 'Lee' // -> 'My name is Lee'
// 할당 연산자
color = 'red' // -> 'red'
// 비교 연산자
3 > 5 // -> false
// 논리 연산자
true && false // -> false
// 타입 연산자
typeof 'Hi' // -> string
```

### 1. 산술 연산자

- 산술 연산자는 피연산자를 대상으로 수학적 계산을 수행해 새로운 숫자 값을 만들고 연산이 불가능한 경우, NaN을 반환
- 피연산자의 개수에 따라 이항 산술 연산자와 단항 산술 연산자로 구분할수 있음

### 1.1 이항 산술 연산자

- 2개의 피연산자를 산술 연산하여 숫자 타입의 값을 만듬
- 부수효과: 피연산자의 값을 변경

| 이항 산술 연산자 |  의미  | 부수 효과 |
| :--------------: | :----: | :-------: |
|        +         |  덧셈  |     ✕     |
|        -         |  뺄셈  |     ✕     |
|        *         |  곱셈  |     ✕     |
|        /         | 나눗셈 |     ✕     |
|        %         | 나머지 |     ✕     |

### 1.2 단항 산술 연산자

- 1개의 피연산자를 산술 연산하여 숫자 타입의 값을 만듬
- 증가/감소 ( ++ / - ) 연산자는 피연산자의 값을 변경하는 부수 효과가 있음

| 단항 산술 연산자 | 의미                                                 | 부수 효과 |
| :--------------: | :--------------------------------------------------- | :-------: |
|        ++        | 증가                                                 |     ○     |
|        --        | 감소                                                 |     ○     |
|        +         | 어떠한 효과도 없다. 음수를 양수로 반전하지도 않는다. |     ✕     |
|        -         | 양수를 음수로 음수를 양수로 반전한 값을 반환한다.    |     ✕     |

- 증가/감소(++/--) 연산자는 위치에 의미가 있음
  - 피연산자 앞에 위치한 전위 증가/감소 연산자(Prefix increment/decrement operator)는 먼저 피연산자의 값을 증가/감소시킨 후, 다른 연산을 수행
  - 피연산자 뒤에 위치한 후위 증가/감소 연산자(Postfix increment/decrement operator)는 먼저 다른 연산을 수행한 후, 피연산자의 값을 증가/감소시킴

```
var x = 5, result;

// 선할당 후증가 (Postfix increment operator)
result = x++;
console.log(result, x); // 5 6

// 선증가 후할당 (Prefix increment operator)
result = ++x;
console.log(result, x); // 7 7

// 선할당 후감소 (Postfix decrement operator)
result = x--;
console.log(result, x); // 7 6

// 선감소 후할당 (Prefix decrement operator)
result = --x;
console.log(result, x); // 5 5
```

- ( + )단항 연산자는 피연산자에 어떠한 효과도 없으나 숫자 타입이 아닌 피연산자에 사용할시 피연산자를 숫자 타입으로 변환하여 반환

  

```
// 아무런 효과가 없다.
+10;    // -> 10
+(-10); // -> -10

// 문자열을 숫자로 타입 변환한다.
+'10'; // -> 10

// 불리언 값을 숫자로 타입 변환한다.
+true; // -> 1

// 불리언 값을 숫자로 타입 변환한다.
+false; // -> 0

// 문자열을 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
+'Hello'; // -> NaN
```

- ( - ) 단항 연산자는 피연산자의 부호를 반전한 값을 반환함

```
// 부호를 반전한다.
-(-10); // -> 10

// 문자열을 숫자로 타입 변환한다.
-'10'; // -> -10

// 불리언 값을 숫자로 타입 변환한다.
-true; // -> -1

// 문자열을 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
-'Hello'; // -> NaN
```

### 1.3 문자열 연결 연산자

- ( + ) 연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작. 외의 경우는 덧셈 연산자로 동작

```
// 문자열 연결 연산자
'1' + 2; // -> '12'
1 + '2'; // -> '12'

// 산술 연산자
1 + 2; // -> 3

// true는 1로 타입 변환된다.
1 + true; // -> 2

// false는 0으로 타입 변환된다.
1 + false; // -> 1

// null는 0으로 타입 변환된다.
1 + null; // -> 1

// undefined는 숫자로 타입 변환되지 않는다.
+undefined;    // -> NaN
1 + undefined; // -> NaN
```

- 암묵적 타입 변환 or 타입 강제 변환 :  개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환됨

### 2. 할당 연산자

- 우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당

| 할당 연산자 | 사례   | 동일 표현 | 부수 효과 |
| :---------: | :----- | :-------- | :-------: |
|      =      | x = 5  | x = 5     |     ○     |
|     +=      | x += 5 | x = x + 5 |     ○     |
|     -=      | x -= 5 | x = x - 5 |     ○     |
|     *=      | x *= 5 | x = x * 5 |     ○     |
|     /=      | x /= 5 | x = x / 5 |     ○     |
|     %=      | x %= 5 | x = x % 5 |     ○     |

```
x = 10;
console.log(x); // 10

x += 5; // x = x + 5;
console.log(x); // 15

x -= 5; // x = x - 5;
console.log(x); // 10

x *= 5; // x = x * 5;
console.log(x); // 50

x /= 5; // x = x / 5;
console.log(x); // 10

x %= 5; // x = x % 5;
console.log(x); // 0

var str = 'My name is ';

// 문자열 연결 연산자
str += 'Lee'; // str = str + 'Lee';

console.log(str); // 'My name is Lee'
```

- 할당문은 값으로 평가되는 표현식인 문

```
var x;

// 할당문은 표현식인 문이다.
console.log(x = 10); // 10

var a, b, c;

// 연쇄 할당. 오른쪽에서 왼쪽으로 진행.
// ① c = 0 : 0으로 평가된다
// ② b = 0 : 0으로 평가된다
// ③ a = 0 : 0으로 평가된다
a = b = c = 0;

console.log(a, b, c); // 0 0 0
```

### 3. 비교 연산자

- 좌항과 우항의 피연산자를 비교 후 불리언 값을 반환
- if 문이나 for 문과 같은 제어문의 조건식에서 주로 사용

### 3.1 동등 / 일치 비교 연산자

- 좌항과 우항의 피연산자가 같은 값을 갖는지 비교하여 불리언 값을 반환

| 비교 연산자 | 의미        | 사례    | 설명                     | 부수 효과 |
| :---------: | :---------- | :------ | :----------------------- | :-------: |
|     ==      | 동등 비교   | x == y  | x와 y의 값이 같음        |     ✕     |
|     ===     | 일치 비교   | x === y | x와 y의 값과 타입이 같음 |     ✕     |
|     !=      | 부동등 비교 | x != y  | x와 y의 값이 다름        |     ✕     |
|     !==     | 불일치 비교 | x !== y | x와 y의 값과 타입이 다름 |     ✕     |

- 일치 비교 (===) 연산자는 좌항과 우항의 피연산자가 타입도 같고 값도 같은 경우에 한하여 true를 반화

- 주의

```
// NaN은 자신과 일치하지 않는 유일한 값이다.
NaN === NaN; // -> false

// 빌트인 함수 isNaN은 주어진 값이 NaN인지 체크하고 그 결과를 반환한다.
isNaN(NaN); // -> true
isNaN(10);  // -> false
isNaN(1 + undefined); // -> true

// 양의 0과 음의 0의 비교. 일치 비교/동등 비교 모두 true이다.
0 === -0; // -> true
0 == -0;  // -> true
```

### 3.2 대소 관계 비교 연산자

- 피연산자의 크기를 비교하여 불리언 값을 반환

| 대소 관계 비교 연산자 | 예제   | 설명                  | 부수 효과 |
| :-------------------: | :----- | :-------------------- | :-------: |
|           >           | x > y  | x가 y보다 크다        |     ✕     |
|           <           | x < y  | x가 y보다 작다        |     ✕     |
|          >=           | x >= y | x가 y보다 같거나 크다 |     ✕     |
|          <=           | x <= y | x가 y보다 같거나 크다 |     ✕     |

### 4. 삼항 조건 연산자

- 조건식의 평가 결과에 따라 반환할 값을 결정

```
조건식 ? 조건식이 true일때 반환할 값 : 조건식이 false일때 반환할 값

var x = 2;

// 2 % 2는 0이고 0은 false로 암묵적 타입 변환된다.
var result = x % 2 ? '홀수' : '짝수';

console.log(result); // 짝수


var x = 2, result;

// 2 % 2는 0이고 0은 false로 암묵적 타입 변환된다.
if (x % 2) result = '홀수';
else       result = '짝수';

console.log(result); // 짝수
```

- 삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식인 문

### 5. 논리 연산자

- 우항과 좌항의 피연산자를 논리 연산

| 논리 연산자 | 의미        | 부수 효과 |
| :---------: | :---------- | :-------: |
|    \|\|     | 논리합(OR)  |     ✕     |
|     &&      | 논리곱(AND) |     ✕     |
|      !      | 부정(NOT)   |     ✕     |

```
// 논리합(||) 연산자
true || true;   // -> true
true || false;  // -> true
false || true;  // -> true
false || false; // -> false

// 논리곱(&&) 연산자
true && true;   // -> true
true && false;  // -> false
false && true;  // -> false
false && false; // -> false

// 논리 부정(!) 연산자
!true;  // -> false
!false; // -> true
```

- 논리합 또는 논리곱의 연산자 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가 되며 불리언 값이 아닐 수도 있음

```
// 단축 평가
'Cat' && 'Dog'; // -> 'Dog'
```

### 6. 쉼표 연산자

- 왼쪽 피연산자부터 차례대로 피연산자를 평가하고 마지막 피연산자의 평가가 끝나면 마지막 피연산자의 평가 결과를 반환

```
var x, y, z;

x = 1, y = 2, z = 3; // 3
```

### 7. 그룹 연산자

- 그룹 연산자 (...)는 자신의 피연산자인 표현식을 가장 먼저 평가
- 연산자의 우선 순위를 조절할 수 있음

```
10 * 2 + 3; // -> 23

// 그룹 연산자를 사용하여 우선 순위 조절
10 * (2 + 3); // -> 50
```

### 8.  Typeof 연산자

- typeof 연산자는 피연산자의 데이터 타입을 문자열로 반환
-  typeof 연산자는 7가지 문자열 “string”, “number”, “boolean”, “undefined”, “symbol”, “object”, “function” 중 하나를 반환
- 함수의 경우 “function”을 반환

```
typeof ''              // -> "string"
typeof 1               // -> "number"
typeof NaN             // -> "number"
typeof true            // -> "boolean"
typeof undefined       // -> "undefined"
typeof Symbol()        // -> "symbol"
typeof null            // -> "object"
typeof []              // -> "object"
typeof {}              // -> "object"
typeof new Date()      // -> "object"
typeof /test/gi        // -> "object"
typeof function () {}  // -> "function"
```

- null 타입을 확인할 때는 일치 연산자를 사용

```
var foo = null;

typeof foo === null; // -> false
foo === null;        // -> true
```

- 선언하지 않은 식별자를 typeof 연산자로 연산해 보면 ReferenceError가 발생하지 않고 “undefined”를 반환

### 9. 지수 연산자

- 좌항의 피연산자를 밑으로, 우항의 피연산자를 지수로 거듭 제곱하여 숫자 타입의 값을 반환

- 지수 연산자는 모든 이상 연산자보다 우선수위가 높음

### 10. 그 외의 연산자

| 연산자     | 개요                                                        |
| :--------- | :---------------------------------------------------------- |
| delete     | 프로퍼티 삭제                                               |
| new        | 생성자 함수를 호출할 때 사용                                |
| instanceof | 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별 |
| in         | 프로퍼티 존재 확인                                          |

### 11. 연산자의 부수 효과

- 부수 효과가 있는 연산자는 할당(=) 연산자, 증가/감소(++/–) 연산자, delete 연산자

```
var x;

// 할당 연산자는 변수 값이 변하는 부수 효과가 있다.
// 이는 변수 x를 사용하는 다른 코드에 영향을 준다.
x = 1;
console.log(x); // 1

// 증가/감소(++/--) 연산자는 피연산자의 값을 변경하는 부수 효과가 있다.
// 피연산자 x의 값이 변경된다. 이는 변수 x를 사용하는 다른 코드에 영향을 준다.
x++;
console.log(x); // 2

var o = { a: 1 };

// delete 연산자는 객체의 프로퍼티를 삭제하는 부수 효과가 있다.
// 이는 객체 o를 사용하는 다른 코드에 영향을 준다.
delete o.a;
console.log(o); // {}
```

