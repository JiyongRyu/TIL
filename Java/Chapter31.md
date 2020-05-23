# 31. RegExp

### 1. 정규 표현식이란?

- 정규 표현식(regular expression, regexp)은 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어(formal language)이다.

- 정규 표현식은 문자열을 대상으로 패턴 매칭 기능을 제공한다. 패턴 매칭 기능이란 특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환할 수 있는 기능을 말한다.

```javascript
// 사용자로 부터 입력받은 휴대폰 전화번호
const tel = '010-1234-567팔';

// 정규표현식 리터럴
// 휴대폰 전화번호 패턴(숫자 3개 + '-' + 숫자 4개 + '-' + 숫자 4개)
const regExp = /^\d{3}-\d{4}-\d{4}$/;

// tel이 휴대폰 전화번호 패턴에 매칭하는지 테스트(확인)한다.
regExp.test(tel); // -> false
```

### 2. 정규 표현식의 생성

- 정규 표현식 객체(RegExp 객체)를 생성하기 위해서는 정규 표현식 리터럴과 RegExp 생성자 함수를 사용할 수 있다. 일반적인 방법은 정규 표현식 리터럴을 사용하는 것이다. 

![31-1](https://poiemaweb.com/assets/fs-images/31-1.png)

### 3. RegExp 메서드

### 3.1 RegExp.prototype.exec

- exec 메서드는 문자열에서 패턴을 검색하여 매칭 결과를 배열로 반환한다. 매칭 결과가 없는 경우, null을 반환한다.

### 3.2 RegExp.prototype.test

- test 메서드는 문자열에서 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.

### 3.3 String.prototype.match

- String 표준 빌트인 객체가 제공하는 match 메서드는 문자열과 정규 표현식과의 매칭 정보를 배열로 반환한다.

### 4. 플래그

- 패턴과 함께 정규 표현식을 구성하는 플래그는 정규 표현식의 검색 방식을 설정한다. 

| 플래그 | 의미        | 설명                                      |
| :----: | :---------- | :---------------------------------------- |
|   i    | Ignore case | 대소문자를 구별하지 않고 검색한다.        |
|   g    | Global      | 문자열 내의 모든 패턴을 검색한다.         |
|   m    | Multi line  | 문자열의 행이 바뀌더라도 검색을 계속한다. |

### 5. 패턴

- 정규 표현식의 패턴은 검색 대상 문자열에서 검색하고 싶은 문자열의 형식을 의미한다. 

### 5.1 문자열 검색

- 패턴에 문자 또는 문자열을 지정하면 검색 대상 문자열에서 해당 문자 또는 문자열을 검색한다. 이때 대소문자를 구별하며 정규 표현식과 매치한 첫번째 결과만 반환한다.

```javascript
const target = 'Is this all there is?';

// 대소문자를 구별하여 'is'를 검색
const regExp = /is/;

// target이 정규 표현식과 매치하는지 테스트
regExp.test(target); // -> true
// target과 정규 표현식의 매칭 결과
target.match(regExp); // -> ["is", index: 5, input: "Is this all there is?", groups: undefined]

---------------------------------------------------------

const target = 'Is this all there is?';

// 대소문자를 구별하지 않고 'is'를 검색
const regExp = /is/i;

target.match(regExp); // -> ["Is", index: 0, input: "Is this all there is?", groups: undefined]

---------------------------------------------------------
  
const target = 'Is this all there is?';

// 대소문자를 구별하지 않고 'is'를 모두 검색
const regExp = /is/ig;

target.match(regExp);// -> ["Is", "is", "is"]
```

### 5.2 임의의 문자열 검색

- .은 임의의 문자 한 개를 의미한다. 문자의 내용은 무엇이든지 상관없다. 

```javascript
const target = 'Is this all there is?';

// 임의의 3자리 문자열을 검색
const regExp = /.../g;

target.match(regExp);// -> ["Is ", "thi", "s a", "ll ", "the", "re ", "is?"]
```

### 5.3 반복 검색

- `{m,n}`은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다. 

```javascript
const target = 'A AA B BB Aa Bb';

// 'A'가 최소 1번, 최대 2번 반복되는 문자열을 모두 검색
const regExp = /A{1,2}/g;

target.match(regExp); // -> ["A", "AA", "A"]
```

### 5.4 OR 검색

- `|`은 or의 의미를 갖는다. `/A|B/`는 ‘A’ 또는 ‘B’를 의미한다.

```javascript
const target = 'A AA B BB Aa Bb';

// 'A' 또는 'B'를 모두 검색
const regExp = /A|B/g;

target.match(regExp);// -> ["A", "A", "A", "B", "B", "B", "A", "B"]
```

### 5.5 NOT 검색

- `[…]` 내의 `^`은 not의 의미를 갖는다. 예를 들어 `[^0-9]`는 숫자를 제외한 문자를 의미한다

```javascript
const target = 'AA BB Aa Bb 12';

// 'A' ~ 'Z' 또는 'a' ~ 'z' 또는 공백 문자가 아닌 문자가 한번 이상 반복되는 문자열을 모두 검색
const regExp = /[^A-Za-z\s]+/g;

target.match(regExp);// -> ["12"]
```

### 5.6 시작 위치로 검색

- `[…]` 밖의 `^`은 문자열의 시작을 의미한다. `[…]` 내의 `^`은 not의 의미를 갖는다.

### 5.7 마지막 위치로 검색

- `$`는 문자열의 마지막을 의미한다.

### 6. 자주 사용하는 정규표현식

특정 단어로 시작하는지 검사한다.

```javascript
const url = 'https://example.com';

// 'http'로 시작하는지 검사
// ^ : 문자열의 처음을 의미한다.
const regExr = /^https/;

regExr.test(url); // -> true
```

특정 단어로 끝나는지 검사한다.

```javascript
const fileName = 'index.html';

// 'html'로 끝나는지 검사
// $ : 문자열의 끝을 의미한다.
const regExr = /html$/;

regExr.test(fileName); // -> true
```

숫자인지 검사한다.

```javascript
const target = '12345';

// 모두 숫자인지 검사
// [^]: 부정(not)을 의미한다. 예를 들어 [^a-z]는 알파벳 소문자로 시작하지 않는 모든 문자를 의미한다.
// [] 바깥의 ^는 문자열의 처음을 의미한다.
const regExr = /^\d+$/;

regExr.test(target); // -> true
```

하나 이상의 공백으로 시작하는지 검사한다.

```javascript
const target = ' Hi!';

// 1개 이상의 공백으로 시작하는지 검사
// \s : 여러 가지 공백 문자 (스페이스, 탭 등) => [\t\r\n\v\f]
const regExr = /^[\s]+/;

regExr.test(target); // -> true
```

아이디로 사용 가능한지 검사한다. (영문자, 숫자만 허용, 4~10자리)

```javascript
const id = 'abc123';

// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~10자리인지 검사
// {4,10}: 4 ~ 10자리
const regExr = /^[A-Za-z0-9]{4,10}$/;

regExr.test(id); // -> true
```

메일 주소 형식에 맞는지 검사한다.

```javascript
const email = 'ungmo2@gmail.com';

const regExr = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/;

regExr.test(email); // -> true
```

핸드폰 번호 형식에 맞는지 검사한다.

```javascript
const cellphone = '010-1234-5678';

const regExr = /^\d{3}-\d{3,4}-\d{4}$/;

regExr.test(cellphone); // -> true
```

특수 문자 포함 여부를 검사한다.

```javascript
const target = 'abc#123';

// A-Za-z0-9 이외의 문자가 있는지 검사
let regExr = /[^A-Za-z0-9]/gi;

regExr.test(target); // -> true

// 아래 방식도 동작한다. 이 방식의 장점은 특수 문자를 선택적으로 검사할 수 있다.
regexr = /[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi;

regExr.test(targetStr); // -> true

// 특수 문자 제거
regExr.replace(regexr, ''); // -> abc123
```