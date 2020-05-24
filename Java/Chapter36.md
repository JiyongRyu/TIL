# 36. 디스트럭처링 할당

- 디스트럭처링 할당(구조 분해 할당, Destructuring assignment)은 구조화된 배열 또는 객체를 Destructuring(비구조화, 구조파괴)하여 1개 이상의 변수에 개별적으로 할당하는 것을 말한다. 배열 또는 객체 리터럴에서 필요한 값만을 추출하여 변수에 할당할 때 유용하다.

### 1. 배열 디스트럭처링 할당

```javascript
// ES5
var arr = [1, 2, 3];

var one   = arr[0];
var two   = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3

-------------------------------------------------------------

const arr = [1, 2, 3];

// ES6 배열 디스트럭처링 할당
// 변수 one, two, three를 선언하고 배열 arr을 디스트럭처링하여 할당한다.
// 이때 할당 기준은 배열의 인덱스이다.
const [one, two, three] = arr;

console.log(one, two, three); // 1 2 3
```

### 2. 객체 디스트럭처링 할당

- ES5에서 객체의 각 프로퍼티를 객체로부터 디스트럭처링하여 변수에 할당하기 위해서는 프로퍼티 키를 사용해야 한다.

```javascript
// ES5
var user = { firstName: 'Ungmo', lastName: 'Lee' };

var firstName = user.firstName;
var lastName  = user.lastName;

console.log(firstName, lastName); // Ungmo Lee
```

- ES6의 객체 디스트럭처링 할당은 객체의 각 프로퍼티를 객체로부터 추출하여 1개 이상의 변수에 할당한다. 배열 디스트럭처링 할당과 마찬가지로 객체 디스트럭처링 할당을 위해서는 할당 연산자 왼쪽에 값을 할당 받을 변수를 선언해야 한다.

  이를 위해 여러 개의 변수를 객체 리터럴 형태로 선언한다. 이때 할당 기준은 프로퍼티 키이다. 즉, 순서는 의미가 없으며 변수 이름과 프로퍼티 키가 일치하면 할당된다.

```javascript
const user = { firstName: 'Ungmo', lastName: 'Lee' };

// ES6 객체 디스트럭처링 할당
// 변수 lastName, firstName을 선언하고 객체 user를 디스트럭처링하여 할당한다.
// 이때 프로퍼티 키를 기준으로 디스트럭처링 할당이 이루어진다. 순서는 의미가 없다.
const { lastName, firstName } = user;

console.log(firstName, lastName); // Ungmo Lee
```

