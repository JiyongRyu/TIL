# 27. 배열

### 1. 배열이란?

- 배열(array)은 여러 개의 값을 순차적으로 나열한 자료 구조이다

```javascript
const arr = ['apple', 'banana', 'orange'];
```

- 배열이 가지고 있는 값을 요소(element)라고 부른다
- 배열의 요소는 배열에서 자신의 위치를 나타내는 0 이상의 정수인 인덱스(index)를 갖는다.

```javascript
arr[0] // -> 'apple'
arr[1] // -> 'banana'
arr[2] // -> 'orange'
```

- 배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 갖는다.

```javascript
arr.length // -> 3
```

- 자바스크립트에 배열이라는 타입은 존재하지 않는다. 배열은 객체이다.
- 배열은 배열 리터럴 또는 Array 생성자 함수로 생성할 수 있다.

```javascript
const arr = [1, 2, 3];

arr.constructor === Array // -> true
Object.getPrototypeOf(arr) === Array.prototype // -> true
```

| 구분            |           객체            |     배열      |
| :-------------- | :-----------------------: | :-----------: |
| 구조            | 프로퍼티 키와 프로퍼티 값 | 인덱스와 요소 |
| 값의 참조       |        프로퍼티 키        |    인덱스     |
| 값의 순서       |             x             |       ○       |
| length 프로퍼티 |             x             |       ○       |

### 2. 자바스크립트 배열은 배열이 아니다.

- 배열의 요소는 하나의 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열을 **밀집 배열(dense array)**이라 한다.

![27-1](https://poiemaweb.com/assets/fs-images/27-1.png)

- 위 그림처럼 메모리 주소 1000에서 시작하고 각 요소의 크기가 8byte인 배열을 생각해 보자.

  - 인덱스가 0인 요소의 메모리 주소 : 1000 + 0 * 8 = 1000
  - 인덱스가 1인 요소에 메모리 주소 : 1000 + 1 * 8 = 1008
  - 인덱스가 2인 요소에 메모리 주소 : 1000 + 2 * 8 = 1016

  이처럼 배열은 인덱스를 통해 효율적으로 요소에 접근할 수 있다는 장점이 있다. 하지만 배열 요소를 처음부터 값을 발견할 때까지 탐색해야하는 시간적인 부분에서 단점이 있다.

- 배열에 요소를 삽입하거나 삭제하는 경우, 배열 요소를 연속적으로 유지하기 위해 요소를 이동시켜야 하는 단점도 있다.

![27-2](https://poiemaweb.com/assets/fs-images/27-2.png)

- 자바스크립트의 배열은 일반적인 의미의 배열과는 다르며 배열의 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며 연속적으로 이어져 있지 않을 수도 있다. 배열의 요소가 연속적으로 이어져 있지 않는 배열을 **희소 배열(sparse array)**이라 한다.
- 일반적인 배열과 자바스크립트 배열의 장단점을 정리해보면 아래와 같다.
  - 일반적인 배열은 인덱스로 배열 요소에 빠르게 접근할 수 있다. 하지만 특정 요소를 탐색하거나 요소를 삽입 또는 삭제하는 경우에는 효율적이지 않다.
  - 자바스크립트 배열은 해시 테이블로 구현된 객체이므로 인덱스로 배열 요소에 접근하는 경우, 일반적인 배열보다 성능적인 면에서 느릴 수 밖에 없는 구조적인 단점을 갖는다. 하지만 특정 요소를 탐색하거나 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠른 성능을 기대할 수 있다.

### 3.  length 프로퍼티와 희소 배열

- length 프로퍼티는 요소의 개수, 즉 배열의 길이를 나타내는 정수를 값으로 갖는다. length 프로퍼티의 값은 빈 배열일 경우, 0이며 빈 배열이 아닐 경우, 가장 큰 인덱스에 1을 더한 것과 같다.

```javascript
[].length        // -> 0
[1, 2, 3].length // -> 3
```

- length 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.

```javascript
const arr = [1, 2, 3];

console.log(arr.length); // 3

// length 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.
// 요소 추가
arr.push(4);
console.log(arr.length); // 4

// 요소 삭제
arr.pop();
console.log(arr.length); // 3
```

- length 프로퍼티의 값은 요소의 개수, 즉 배열의 길이를 바탕으로 결정되지만 임의의 숫자 값을 명시적으로 할당할 수도 있다.

  현재 length 프로퍼티 값보다 작은 숫자 값을 할당하면 배열의 길이가 줄어든다.

```javascript
const arr = [1, 2, 3, 4, 5];

// length 프로퍼티에 현재 length 프로퍼티 값보다 작은 숫자 값을 할당
arr.length = 3;

// 배열의 길이가 줄어든다.
console.log(arr); // [1, 2, 3]
```

- 주의할 것은 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우이다. 이때 length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.

```javascript
const arr = [1];

// length 프로퍼티에 현재 length 프로퍼티 값보다 큰 숫자 값을 할당
arr.length = 3;

// length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.
console.log(arr.length); // 3
console.log(arr); // [1, empty × 2]
```

- 위 예제의 출력 결과에서 empty × 2는 실제로 추가된 배열의 요소가 아니다. 즉, arr[1]과 arr[2]에는 값이 존재하지 않는다.

  이와 같이 length 프로퍼티에 현재 length 프로퍼티 값보다 큰 숫자 값을 할당하는 경우, length 프로퍼티 값은 성공적으로 변경되지만 실제 배열에는 아무런 변함이 없다. 값이 없이 비어있는 요소를 위해 메모리 공간을 확보하지 않으며 빈 요소를 생성하지도 않는다.

### 4. 배열 생성

### 4.1 배열 리터럴

- 배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호([])로 묶는다. 배열 리터럴은 객체 리터럴과 달리 프로퍼티 이름이 없고 값만이 존재한다.

```javascript
const arr = [1, 2, 3];
console.log(arr.length); // 3
```

### 4.2  Array 생성자 함수

- 전달된 인수가 1개이고 숫자인 경우, 인수를 length 프로퍼티의 값으로 갖는 배열을 생성한다.

```javascript
const arr = new Array(10);

console.log(arr); // [empty × 10]
console.log(arr.length); // 10
```

- 전달된 인수가 없는 경우, 빈 배열을 생성한다. 즉, 배열 리터럴 []과 같다.

```javascript
const empty = new Array();

console.log(empty); // []
```

- 전달된 인수가 2개 이상이거나 숫자가 아닌 경우, 인수를 요소로 갖는 배열을 생성한다.

```javascript
// 전달된 인수가 1개이지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성한다.
const arr1 = new Array({});

console.log(arr1); // [{}]

// 전달된 인수가 2개 이상이면 인수를 요소로 갖는 배열을 생성한다.
const arr2 = new Array(1, 2, 3);

console.log(arr2); // [1, 2, 3]
```

- Array 생성자 함수는 new 연산자와 함께 호출하지 않더라도, 즉 함수로 호출하더라도 배열을 생성하는 생성자 함수로 동작한다. 이는 Array 생성자 함수 내부에서 new.target을 확인하기 때문이다.

```javascript
const arr = Array(1, 2, 3);
console.log(arr); // [1, 2, 3]
```

### 4.3  Array.of

- ES6에서 새롭게 도입된 Array.of 메소드는 전달된 인수를 요소로 갖는 배열을 생성한다.

  Array.of는 Array 생성자 함수와 다르게 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.

```javascript
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.
const arr1 = Array.of(1);
console.log(arr1); // [1]

const arr2 = Array.of(1, 2, 3);
console.log(arr2); // [1, 2, 3]

const arr3 = Array.of('string');
console.log(arr3); // ['string']
```

### 4.4 Array.from

- ES6에서 새롭게 도입된 Array.from 메소드는 유사 배열 객체(array-like object) 또는 이터러블 객체(iterable object)를 변환하여 새로운 배열을 생성한다.

```javascript
// 문자열은 이터러블이다.
const arr1 = Array.from('Hello');
console.log(arr1); // ['H', 'e', 'l', 'l', 'o']

// 유사 배열 객체를 새로운 배열을 변환하여 반환한다.
const arr2 = Array.from({ length: 2, 0: 'a', 1: 'b' });
console.log(arr2); // ['a', 'b']
```

- Array.from을 사용하면 두번째 인수로 전달한 함수를 통해 값을 만들면서 요소를 채울 수 있다. 두번째 인수로 전달한 함수는 첫번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달받아 새로운 요소를 생성할 수 있다.

```javascript
// Array.from의 두번째 인수로 배열의 모든 요소에 대해 호출할 함수를 전달할 수 있다.
// 이 함수는 첫번째 인수에 의해 생성된 배열의 요소값괴 인덱스를 순차적으로 전달받아 호출된다.
const arr3 = Array.from({ length: 5 }, function (_, i) { return i; });
console.log(arr3); // [0, 1, 2, 3, 4]
```

### 5. 배열 요소의 참조

- 배열 요소를 참조할 때에는 대괄호([]) 표기법을 사용한다. 대괄호 안에는 인덱스가 와야 한다.
- 존재하지 않는 요소에 접근하면 undefined가 반환된다.

```javascript
const arr = [1, 2];

// 인덱스가 0인 요소를 참조
console.log(arr[0]); // 1
// 인덱스가 1인 요소를 참조
console.log(arr[1]); // 2


const arr = [1, 2];

// 인덱스가 2인 요소를 참조
// 배열 arr에 인덱스가 2인 요소는 존재하지 않는다.
console.log(arr[2]); // undefined
```

### 6. 배열 요소의 추가와 갱신

- 객체에 프로퍼티를 동적으로 추가할 수 있는 것처럼 배열에도 요소를 동적으로 추가할 수 있다. 요소가 존재하지 않는 인덱스의 배열 요소에 값을 할당하면 새로운 요소가 추가된다. 이때 length 프로퍼티 값은 자동 갱신된다.

```javascript
const arr = [0];

// 배열 요소의 추가
arr[1] = 1;

console.log(arr); // [0, 1]
console.log(arr.length); // 2
```

- 이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.
- 인덱스는 요소의 위치를 나타내므로 반드시 0 이상의 정수(또는 정수 형태의 문자열)를 사용하여야 한다. 만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다. 이때 추가된 프로퍼티는 length 프로퍼티의 값에 영향을 주지 않는다.

```javascript
const arr = [];

// 배열 요소의 추가
arr[0] = 1;
arr['1'] = 2;

// 프로퍼티 추가
arr['foo'] = 3;
arr[1.1] = 4;
arr[-1] = 5;

console.log(arr); // [1, 2, foo: 3, 1.1: 4, -1: 5]

// 프로퍼티는 length에 영향을 주지 않는다.
console.log(arr.length); // 2
```

### 7. 배열 요소의 삭제

- 배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 delete 연산자를 사용할 수 있다.

```javascript
const arr = [1, 2, 3];

// 배열 요소의 삭제
delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
console.log(arr.length); // 3
```

- 희소 배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 Array.prototype.splice 메소드를 사용한다.

```javascript
const arr = [1, 2, 3];

// Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소수)
// arr[1]부터 1개의 요소를 제거
arr.splice(1, 1);
console.log(arr); // [1, 3]

// length 프로퍼티에 변경이 반영된다.
console.log(arr.length); // 2
```

### 8.  배열 메소드

- 배열의 프로토타입인 Array.prototype는 배열을 다룰 때 필요한 메소드를 제공한다.
- 배열에는 원본 배열(배열 메소드를 호출한 배열, 즉 배열 메소드의 구현체 내부에서 this가 가리키는 객체)을 직접 변경하는 메소드(mutator method)와 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메소드(accessor method)가 있다. 

```javascript
const arr = [1];

// push 메소드는 원본 배열(arr)을 직접 변경한다.
arr.push(2);
console.log(arr); // [1, 2]

// concat 메소드는 원본 배열(arr)을 직접 변경하지 않고 새로운 배열을 생성하여 반환한다.
const result = arr.concat(3);
console.log(arr);    // [1, 2]
console.log(result); // [1, 2, 3]
```

### 8.1 Array.isArray

- Array.isArray는 Array 생성자 함수의 정적 메소드이다.
- Array.isArray는 주어진 인수가 배열이면 true, 배열이 아니면 false를 반환한다.

### 8.2 Array.prototype.indexOf

- indexOf 메소드는 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.
  - 중복되는 요소가 있는 경우, 첫번째 인덱스를 반환한다.
  - 해당하는 요소가 없는 경우, -1을 반환한다.

```javascript
const arr = [1, 2, 2, 3];

// 배열 arr에서 요소 2를 검색하여 첫번째 인덱스를 반환
arr.indexOf(2);    // -> 1
// 배열 arr에서 요소 4가 없으므로 -1을 반환
arr.indexOf(4);    // -1
// 두번째 인수는 검색을 시작할 인덱스이다. 두번째 인수를 생략하면 처음부터 검색한다.
arr.indexOf(2, 2); // 2
```

- indexOf 메소드는 배열에 특정 요소가 존재하는지 확인할 때 유용하다.
- indexOf 메소드 대신 ES7에서 새롭게 도입된 Array.prototype.includes 메소드를 사용하면 보다 가독성이 좋다.

```javascript
const foods = ['apple', 'banana'];

// ES7: Array.prototype.includes
// foods 배열에 'orange' 요소가 존재하는지 확인
if (!foods.includes('orange')) {
  // foods 배열에 'orange' 요소가 존재하지 않으면 'orange' 요소를 추가
  foods.push('orange');
}

console.log(foods); // ["apple", "banana", "orange"]
```

### 8.3 Array.prototype.push

- push 메소드는 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 값을 반환한다. push 메소드는 원본 배열을 직접 변경한다.

```javascript
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.push(3, 4);
console.log(result); // 4

// push 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 2, 3, 4]
```

- push 메소드는 성능면에서 좋지 않다. push 메소드는 배열의 마지막에 요소를 추가하므로 length 프로퍼티를 사용하여 직접 요소를 추가할 수도 있다. 이 방법이 push 메소드보다 빠르다.

```javascript
const arr = [1, 2];

// arr.push(3)과 동일한 처리를 한다. 이 방법이 push 메소드보다 빠르다.
arr[arr.length] = 3;

console.log(arr); // [1, 2, 3]
```

### 8.4 Array.prototype.pop

- pop 메소드는 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다. 원본 배열이 빈 배열이면 undefined를 반환한다. pop 메소드는 원본 배열을 직접 변경한다.

```javascript
const arr = [1, 2];

// 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.pop();
console.log(result); // 2

// pop 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```

### 8.5 Array.prototype.unshift

- unshift 메소드는 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 값을 반환한다. unshift 메소드는 원본 배열을 직접 변경한다.

```javascript
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.unshift(3, 4);
console.log(result); // 4

// unshift 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [3, 4, 1, 2]
```

### 8.6 Array.prototype.shift

- shift 메소드는 원본 배열에서 첫번째 요소를 제거하고 제거한 요소를 반환한다. 원본 배열이 빈 배열이면 undefined를 반환한다. shift 메소드는 원본 배열을 직접 변경한다.

```javascript
const arr = [1, 2];

// 원본 배열에서 첫번째 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.shift();
console.log(result); // 1

// shift 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [2]
```

- shift 메소드와 push 메소드를 사용하면 큐를 쉽게 구현할 수 있다.

  큐(queue)는 데이터를 마지막에 밀어 넣고, 처음 데이터, 즉 가장 먼저 밀어 넣은 데이터를 먼저 꺼내는 선입 선출(FIFO - First In First Out) 방식의 자료 구조이다.

![27-4](https://poiemaweb.com/assets/fs-images/27-4.png)

### 8.7 Array.prototype.concat

- concat 메소드는 인수로 전달된 값들(배열 또는 값)을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다. 인수로 전달한 값이 배열인 경우, 배열을 해체하여 새로운 배열의 요소로 추가한다. 원본 배열은 변경되지 않는다.
- push와 unshift 메소드는 concat 메소드로 대체할 수 있다. push와 unshift 메소드는 concat 메소드와 유사하게 동작하지만 미묘한 차이가 있다.
  - push와 unshift 메소드는 원본 배열을 직접 변경하지만 concat 메소드는 원본 배열을 변경하지 않고 새로운 배열을 반환한다. 따라서 push와 unshift 메소드를 사용할 경우, 원본 배열을 반드시 변수에 할당해야 하며 concat 메소드를 사용할 경우, 반환값을 반드시 변수에 할당 받아야 한다.

```javascript
const arr1 = [3, 4];

// unshift 메소드는 원본 배열을 직접 변경한다.
arr1.unshift(1, 2);
// unshift 메소드를 사용할 경우, 원본 배열을 반드시 변수에 할당해야 결과를 확인할 수 있다.
console.log(arr1); // [1, 2, 3, 4]

// push 메소드는 원본 배열을 직접 변경한다.
arr1.push(5, 6);
// push 메소드를 사용할 경우, 원본 배열을 반드시 변수에 할당해야 결과를 확인할 수 있다.
console.log(arr1); // [1, 2, 3, 4, 5, 6]

// unshift와 push 메소드는 concat 메소드로 대체할 수 있다.
const arr2 = [3, 4];

// concat 메소드는 원본 배열을 변경하지 않고 새로운 배열을 반환한다.
// arr1.unshift(1, 2)를 아래와 같이 대체할 수 있다.
let result = [1, 2].concat(arr2);
console.log(result); // [1, 2, 3, 4]

// arr1.push(5, 6)를 아래와 같이 대체할 수 있다.
result = result.concat(5, 6);
console.log(result); // [1, 2, 3, 4, 5, 6]
```

- 인수로 전달받은 값이 배열인 경우, push와 unshift 메소드는 배열을 그대로 원본 배열의 마지막/첫번째 요소로 추가하지만 concat 메소드는 인수로 전달받은 배열을 해체하여 새로운 배열의 마지막 요소로 추가한다.

```javascript
const arr = [3, 4];

// unshift와 push 메소드는 인수로 전달받은 배열을 그대로 원본 배열의 요소로 추가한다
arr.unshift([1, 2]);
arr.push([5, 6]);
console.log(arr); // [[1, 2], 3, 4,[5, 6]]

// concat 메소드는 인수로 전달받은 배열을 해체하여 새로운 배열의 요소로 추가한다
let result = [1, 2].concat([3, 4]);
result = result.concat([5, 6]);

console.log(result); // [1, 2, 3, 4, 5, 6]
```

### 8.8 Array.prototype.splice

- 원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우, splice 메소드를 사용한다. splice 메소드는 3개의 매개변수가 있으며 원본 배열을 직접 변경한다.
  - start : 원본 배열의 요소를 제거하기 시작할 인덱스이다. start 만을 지정하면 원본 배열의 start부터 모든 요소를 제거한다. start가 음수인 경우, 배열의 끝에서의 인덱스를 나타낸다. 만약 start가 -1이면 마지막 요소를 가리키고 -n이면 마지막에서 n번째 요소를 가리킨다.
  - deleteCount : 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수이다. deleteCount가 0인 경우, 아무런 요소도 제거되지 않는다. (옵션)
  - items : 제거한 위치에 삽입될 요소들의 목록이다. 생략할 경우, 원본 배열에서 지정된 요소들을 제거만 한다. (옵션)

![27-5](https://poiemaweb.com/assets/fs-images/27-5.png)

```javascript
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
const result = arr.splice(1, 2, 20, 30);

// 제거한 요소가 배열로 반환된다.
console.log(result); // [2, 3]
// splice 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 20, 30, 4]
```

- splice 메소드의 두번째 인수, 즉 제거할 요소의 개수를 0으로 지정하면 아무런 요소도 제거하지 않고 새로운 요소들을 삽입한다.
- splice 메소드의 세번째 인수, 즉 제거한 위치에 추가할 요소들의 목록을 전달하지 않으면 원본 배열에서 지정된 요소만을 제거한다.

### 8.9  Array.prototype.slice

- slice 메소드는 인수로 전달된 범위의 요소들을 복사하여 반환한다. 원본 배열은 변경되지 않는다. 
- slice 메소드는 2개의 매개변수를 갖는다.
  - start : 복사를 시작할 인덱스이다. 음수인 경우, 배열의 끝에서의 인덱스를 나타낸다. 예를 들어 slice(-2)는 배열의 마지막 2개의 요소를 반환한다.
  - end : 복사를 종료할 인덱스이다. 이 인덱스에 해당하는 요소는 복사되지 않는다. 옵션이며 기본값은 length 값이다.

```javascript
const arr = [1, 2, 3];

// arr[0]부터 arr[1] 이전(arr[1] 미포함)까지 복사하여 반환한다.
let result = arr.slice(0, 1);
console.log(result); // [1]

// arr[1]부터 arr[2] 이전(arr[2] 미포함)까지 복사하여 반환한다.
result = arr.slice(1, 2);
console.log(result); // [2]

// 원본은 변경되지 않는다.
console.log(arr); // [1, 2, 3]
```

- slice 메소드의 두번째 인수를 생략하면 첫번째 인수에 해당하는 인덱스부터 모든 요소를 복사하여 반환한다.
- slice 메소드의 인수를 모두 생략하면 원본 배열의 새로운 복사본을 생성하여 반환한다.

### 8.10 Array.prototype.join

- join 메소드는 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 값, 즉 구분자(separator)로 연결한 문자열을 반환한다. 구분자는 생략 가능하며 기본 구분자는 ‘,’이다.

```javascript
const arr = [1, 2, 3, 4];

// 기본 구분자는 ','이다.
// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 기본 구분자 ','로 연결한 문자열을 반환
let result = arr.join();
console.log(result); // '1,2,3,4';

// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 빈문자열로 연결한 문자열을 반환
result = arr.join('');
console.log(result); // '1234'

// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 구분자 ':'로 연결한 문자열을 반환
result = arr.join(':');
console.log(result); // '1:2:3:4'
```

### 8.11 Array.prototype.reverse

- reverse 메소드는 원본 배열의 요소 순서를 반대로 변경한다. 이때 원본 배열이 변경된다. 반환값은 변경된 배열이다.

### 8.12 Array.prototype.fill

- ES6에서 새롭게 도입된 fill 메소드는 인수로 전달 받은 값을 요소로 배열의 처음부터 끝까지 채운다. 이때 원본 배열이 변경된다.

### 8.13 Array.prototype.includes

- ES7에서 새롭게 도입된 includes 메소드는 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다. 첫번째 인수로 검색할 대상을 지정한다.

```javascript
const arr = [1, 2, 3];

// 배열에 요소 2가 포함되어 있는지 확인한다.
let result = arr.includes(2);
console.log(result); // true

// 배열에 요소 100이 포함되어 있는지 확인한다.
result = arr.includes(100);
console.log(result); // false
```

### 8.14 Array.prototype.flat

- flat 메소드는 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다.

```javascript
console.log([1, [2, 3, 4, 5]].flat()); // [1, 2, 3, 4, 5]
```

### 9. 배열 고차 함수

### 9.1 Array.prototype.sort

- sort 메소드는 배열의 요소를 정렬한다. 원본 배열을 직접 변경하며 정렬된 배열을 반환한다. sort 메소드는 기본적으로 오름차순으로 요소를 정렬한다.

```javascript
const fruits = ['Banana', 'Orange', 'Apple'];

// 오름차순(ascending) 정렬
fruits.sort();

// sort 메소드는 원본 배열을 직접 변경한다.
console.log(fruits); // ['Apple', 'Banana', 'Orange']
```

- 숫자 요소들로 이루어진 배열을 정렬할 때는 주의가 필요한데 숫자 요소를 정렬하기 위해서는 sort 메소드에 **정렬 순서를 정의하는 비교 함수를 인수로 전달**한다. 비교 함수를 생략하면 배열의 각 요소는 일시적으로 문자열로 변환되어 Unicode 코드 포인트 순서에 따라 정렬된다.

```javascript
const points = [40, 100, 1, 5, 2, 25, 10];

// 숫자 배열 오름차순 정렬
// 비교 함수의 반환값이 0보다 작은 경우, a를 우선하여 정렬한다.
points.sort((a, b) => a - b);
console.log(points); // [1, 2, 5, 10, 25, 40, 100]

// 숫자 배열에서 최소값 취득
console.log(points[0]); // 1

// 숫자 배열 내림차순 정렬
// 비교 함수의 반환값이 0보다 큰 경우, b를 우선하여 정렬한다.
points.sort((a, b) => b - a);
console.log(points); // [100, 40, 25, 10, 5, 2, 1]

// 숫자 배열에서 최대값 취득
console.log(points[0]); // 100
```

### 9.2 Array.prototype.forEach

- forEach 메소드는 for 문을 대체할 수 있는 메소드이다. 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다.

```
const numbers = [1, 2, 3];
let pows = [];

// for 문으로 배열 순회
for (let i = 0; i < numbers.length; i++) {
  pows.push(numbers[i] ** 2);
}

console.log(pows); // [1, 4, 9]

pows = [];

// forEach 메소드로 배열 순회
numbers.forEach(item => pows.push(item ** 2));

console.log(pows); // [1, 4, 9]
```

- forEach 메소드의 콜백 함수는 요소값, 인덱스, forEach 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.
- forEach 메소드는 원본 배열을 변경하지 않는다. 하지만 콜백 함수가 원본 배열을 변경할 수는 있다.
- forEach 메소드의 반환값은 언제나 undefined이다.

### 9.3 Array.prototype.map

- map 메소드는 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다. 그리고 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다. 이때 원본 배열은 변경되지 않는다.

```javascript
const numbers = [1, 4, 9];

// 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다.
// 그리고 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.
const roots = numbers.map(item => Math.sqrt(item));

// 위 코드의 축약 표현은 아래와 같다.
// const roots = numbers.map(Math.sqrt);

// map 메소드는 새로운 배열을 반환한다
console.log(roots);   // [ 1, 2, 3 ]
// map 메소드는 원본 배열은 변경하지 않는다
console.log(numbers); // [ 1, 4, 9 ]
```

- forEach 메소드는 배열을 순회하며 요소 값을 참조하여 무언가를 하기 위한 함수이며 map 메소드는 배열을 순회하며 요소 값을 다른 값으로 맵핑하기 위한 함수이다. 따라서 **map 메소드가 생성하여 반환하는 새로운 배열의 length는 map 메소드를 호출한 배열, 즉 this의 length와 반드시 일치한다. 즉, 1:1 매핑(mapping)한다.**

![27-9](https://poiemaweb.com/assets/fs-images/27-9.png)

- forEach 메소드와 마찬가지로 map 메소드의 콜백 함수는 요소값, 인덱스, map 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.
- forEach 메소드와 마찬가지로 map 메소드에 두번째 인자로 map 메소드 내부에서 this로 사용될 객체를 전달할 수 있다.

### 9.4 Array.prototype.filter

- filter 메소드는 배열을 순회하며 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행한다. 그리고 콜백 함수의 실행 결과가 true인 배열 요소의 값만을 추출한 새로운 배열을 반환한다. 이때 원본 배열은 변경되지 않는다.

```javascript
const numbers = [1, 2, 3, 4, 5];

// 홀수만을 필터링한다 (1은 true로 평가된다)
const odds = numbers.filter(item => item % 2);

console.log(odds); // [1, 3, 5]
```

- filter 메소드는 배열에서 특정 요소만을 필터링 조건으로 추출하여 새로운 배열을 만들고 싶을 때 사용한다. 
- **filter 메소드가 생성하여 반환하는 새로운 배열의 length는 filter 메소드를 호출한 배열, 즉 this의 length와 같거나 작다.**

![27-10](https://poiemaweb.com/assets/fs-images/27-10.png)

- forEach, map 메소드와 마찬가지로 filter 메소드의 콜백 함수는 요소값, 인덱스, filter 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.

### 9.5 Array.prototype.reduce

- reduce 메소드는 배열을 순회하며 콜백 함수의 이전 반환값과 배열의 각 요소에 대하여 인수로 전달된 콜백 함수를 실행하여 하나의 결과값을 반환한다. 이때 원본 배열은 변경되지 않는다.
- reduce 메소드는 첫번째 인수로 콜백 함수, 두번째 인수로 초기값을 전달받는다. reduce 메소드의 콜백 함수에는 4개의 인수, 초기값 또는 콜백 함수의 이전 반환값, 요소값, 인덱스, reduce 메소드를 호출한 배열, 즉 this가 전달된다.

```javascript
// 1부터 4까지 누적을 구한다.
const sum = [1, 2, 3, 4].reduce((accumulator, currentValue, index, array) => accumulator + currentValue, 0);

console.log(sum); // 10
```

### 9.6 Array.prototype.some

- some 메소드는 배열을 순회하며 각 요소에 대하여 인수로 전달된 콜백 함수를 실행하여 그 결과가 하나라도 참이라면 true, 모두 거짓이라면 false를 반환한다. 즉, 배열의 요소 중에 콜백 함수를 통해 정의한 조건을 만족하는 요소가 1개 이상 존재하는지 확인하여 그 결과를 불리언 타입으로 반환한다.
- forEach, map, filter 메소드와 마찬가지로 some 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.

```javascript
// 배열의 요소 중에 10보다 큰 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(item => item > 10); // -> true

// 배열의 요소 중에 0보다 작은 요소가 1개 이상 존재하는지 확인
[5, 10, 15].some(item => item < 0); // -> false

// 배열의 요소 중에 'banana'가 1개 이상 존재하는지 확인
['apple', 'banana', 'mango'].some(item => item === 'banana'); // -> true
```

### 9.7 Array.prototype.every

- every 메소드는 배열을 순회하며 각 요소에 대하여 인수로 전달된 콜백 함수를 실행하여 그 결과가 모두 참이라면 true, 하나라도 거짓이라면 false를 반환한다. 즉, 배열의 모든 요소가 콜백 함수를 통해 정의한 조건을 모두 만족하는지 확인하여 그 결과를 불리언 타입으로 반환한다.
- forEach, map, filter 메소드와 마찬가지로 every 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.

```javascript
// 배열의 모든 요소가 3보다 큰지 확인
[5, 10, 15].every(item => item > 3); // -> true

// 배열의 모든 요소가 10보다 큰지 확인
[5, 10, 15].every(item => item > 10); // -> false
```

### 9.8 Array.prototype.find

- ES6에서 새롭게 도입된 find 메소드는 배열을 순회하며 각 요소에 대하여 인수로 전달된 콜백 함수를 실행하여 그 결과가 참인 첫번째 요소를 반환한다. 콜백 함수의 실행 결과가 참인 요소가 존재하지 않는다면 undefined를 반환한다.
- forEach, map, filter 메소드와 마찬가지로 find 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.

```javascript
const users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' }
];

// id가 2인 요소를 반환한다.
const result = users.find(item => item.id === 2);

// Array#find는 배열이 아니라 요소를 반환한다.
console.log(result); // {id: 2, name: 'Kim'}
```

### 9.9 Array.prototype.findIndex

- ES6에서 새롭게 도입된 findIndex 메소드는 배열을 순회하며 각 요소에 대하여 인수로 전달된 콜백 함수를 실행하여 그 결과가 참인 첫번째 요소의 인덱스를 반환한다. 콜백 함수의 실행 결과가 참인 요소가 존재하지 않는다면 -1를 반환한다.
- forEach, map, filter 메소드와 마찬가지로 findIndex 메소드의 콜백 함수는 요소값, 인덱스, 메소드를 호출한 배열, 즉 this를 전달 받을 수 있다.

```javascript
const users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' },
  { id: 2, name: 'Choi' },
  { id: 3, name: 'Park' }
];

// Array#findIndex는 콜백 함수를 실행하여 그 결과가 참인 첫번째 요소의 인덱스를 반환한다.
// id가 2인 요소의 인덱스를 구한다.
users.findIndex(user => user.id === 2); // -> 1

// name이 'Park'인 요소의 인덱스를 구한다.
users.findIndex(user => user.name === 'Park'); // -> 3

// 위와 같이 프로퍼티 키와 프로퍼티 값으로 요소의 인덱스를 구하는 경우,
// 아래와 같이 콜백 함수를 추상화할 수 있다.
function predicate(key, value) {
  // key와 value를 기억하는 클로저를 반환
  return item => item[key] === value;
}

// id가 2인 요소의 인덱스를 구한다.
users.findIndex(predicate('id', 2)); // -> 1

// name이 'Park'인 요소의 인덱스를 구한다.
users.findIndex(predicate('name', 'Park')); // -> 3
```

### 9.10 Array.prototype.flatMap

- ES10(ECMAScript 2019)에서 새롭게 도입된 flatMap 메소드는 map을 통해 생성된 새로운 배열을 평탄화한다. 즉, map 메소드와 flat 메소드를 순차적으로 실행하는 효과가 있다.

```javascript
let arr = ['hello', 'world'];

// map과 flat을 순차적으로 실행
console.log(arr.map(str => str.split('')).flat());
// ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']

// flatMap은 map을 통해 생성된 새로운 배열을 평탄화한다.
console.log(arr.flatMap(str => str.split('')));
// ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
```

