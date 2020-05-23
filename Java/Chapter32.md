# 32. String

### 1. String 생성자 함수

- 표준 빌트인 객체인 String 객체는 생성자 함수 객체이다. 따라서 new 연산자와 함께 호출하여 String 인스턴스를 생성할 수 있다.
- String 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[StringData]] 내부 슬롯에 빈 문자열을 할당한 String 래퍼 객체를 생성한다.

### 2. length 프로퍼티

- length 프로퍼티는 문자열의 문자 개수를 반환한다.

### 3. String 메소드

- String 객체의 모든 메소드는 언제나 새로운 문자열을 반환한다. 

### 3.1 String.prototype.indexOf

- indexOf 메소드는 문자열에서 인수로 전달한 문자열을 검색하여 첫번째 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.
- indexOf 메소드는 문자열에 특정 문자열이 존재하는지 확인할 때 유용하다.

### 3.2 String.prototype.search

- search 메소드는 문자열 내에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다. 검색에 실패하면 -1을 반환한다.

### 3.3 String.prototype.includes

- ES6에서 새롭게 도입된 includes 메소드는 문자열에 인수로 전달한 문자열이 포함되어 있는지 확인하여 그 결과를 true 또는 false로 반환한다.

### 3.4 String.prototype.startsWith

- ES6에서 새롭게 도입된 startsWith 메소드는 문자열이 인수로 전달한 문자열로 시작되는지 확인하여 그 결과를 true 또는 false로 반환한다.

### 3.5 String.prototype.endsWith

- ES6에서 새롭게 도입된 endsWith 메소드는 메소드는 문자열이 인수로 전달한 문자열로 끝나는지 확인하여 그 결과를 true 또는 false로 반환한다.

### 3.6 String.prototype.charAt

- charAt 메소드는 인수로 전달한 인덱스에 위치한 문자를 반환한다.

### 3.7 String.prototype.substring

- substring 메소드는 첫번째 인수로 전달한 인덱스에 위치하는 문자부터 두번째 인수로 전달한 인덱스에 위치하는 문자의 바로 이전 문자까지 문자열의 부분 문자열을 반환한다.

### ![32-1](https://poiemaweb.com/assets/fs-images/32-1.png)

- substring 메소드의 첫번째 인수는 두번째 인수보다 큰 정수이어야 정상이다. 하지만 아래와 같이 인수를 전달하여도 정상 동작한다.
  - 첫번째 인수 > 두번째 인수인 경우, 두 인수는 교환된다.
  - 인수 < 0 또는 NaN인 경우, 0으로 취급된다.
  - 인수 > 문자열의 길이(str.length)인 경우, 인수는 문자열의 길이(str.length)으로 취급된다.

```javascript
const str = 'Hello World'; // str.length == 11

// 첫번째 인수 > 두번째 인수인 경우, 두 인수는 교환된다.
str.substring(4, 1); // -> 'ell'

// 인수 < 0 또는 NaN인 경우, 0으로 취급된다.
str.substring(-2); // -> 'Hello World'

// 인수 > 문자열의 길이(str.length)인 경우, 인수는 문자열의 길이(str.length)으로 취급된다.
str.substring(1, 100); // -> 'ello World'
str.substring(20); // -> ''
```

### 3.8 String.prototype.slice

- slice 메소드는 substring 메소드와 동일하게 동작한다. 단, slice 메소드에는 음수인 인수를 전달할 수 있다. 음수인 인수를 전달하면 뒤에서부터 시작하여 문자열을 잘라내어 반환한다.

```javascript
const str = 'hello world';

// substring과 slice 메소드는 동일하게 동작한다.
// 0번째부터 5번째 이전 문자까지 잘라내어 반환
str.substring(0, 5); // -> 'hello'
str.slice(0, 5); // -> 'hello'

// 인덱스가 2인 문자부터 마지막 문자까지 잘라내어 반환
str.substring(2); // -> 'llo world'
str.slice(2); // -> 'llo world'

// slice 메소드는 음수인 인수를 전달할 수 있다.
// 인수 < 0 또는 NaN인 경우, 0으로 취급된다.
str.substring(-5); // -> 'hello world'
// 뒤에서 5자리를 잘라내어 반환한다.
str.slice(-5); // ⟶ 'world'
```

### 3.9 String.prototype.toUpperCase

- toUpperCase 메소드는 문자열의 모든 문자를 대문자로 변경하여 반환한다.

### 3.10 String.prototype.toLowerCase

- toLowerCase 메소드는 문자열의 모든 문자를 대문자로 변경하여 반환한다.

### 3.11 String.prototype.trim

- trim 메소드는 문자열 앞뒤에 공백 문자가 있을 경우, 이를 제거한 문자열을 반환한다.

### 3.12 String.prototype.repeat

- ES6에서 새롭게 도입된 repeat 메소드는 인수로 전달한 정수만큼 반복해 연결한 새로운 문자열을 반환한다. 인수로 전달한 정수가 0이면 빈 문자열을 반환하고 음수이면 RangeError를 발생시킨다.

### 3.13 String.prototype.replace

- replace 메소드는 첫번째 인수로 전달한 문자열 또는 정규표현식을 대상 문자열에서 검색하여 두번째 인수로 전달한 문자열로 치환하여 결과가 반영된 새로운 문자열을 반환한다.

### 3.14 String.prototype.split

- 첫번째 인수로 전달한 문자열 또는 정규표현식을 대상 문자열에서 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다. 인수가 없는 경우, 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.

