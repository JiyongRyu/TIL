# 35. 스프레드 문법

- ES6에서 새롭게 도입된 스프레드 문법(Spread syntax; 전개 문법) `...`은 하나로 뭉쳐 있는 여러 값들의 집합을 펼쳐서(전개, 분산하여, spread) 개별적인 값들의 목록으로 만든다.
- for…of 문으로 순회할 수 있는 이터러블에 한정된다.

```javascript
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(→ 1, 2, 3)
console.log(...[1, 2, 3]); // 1 2 3

// 문자열은 이터러블이다.
console.log(...'Hello'); // H e l l o

// Map과 Set은 이터러블이다.
console.log(...new Map([['a', '1'], ['b', '2']])); // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3])); // 1 2 3

// 이터러블이 아닌 일반 객체는 스프레드 문법의 대상이 될 수 없다.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```

- 스프레드 문법의 결과물은 값으로 사용할 수 없고, 아래와 같이 쉼표로 구분한 값의 목록을 사용하는 문맥에서만 사용할 수 있다.
  - 함수 호출문의 인수 목록
  - 배열 리터럴의 요소 목록
  - 객체 리터럴의 프로퍼티 목록

### 1. 함수 호출문의 인수 목록에서 사용하는 경우

- 요소값들의 집합인 배열을 펼쳐서 개별적인 값들의 목록으로 만든 후, 이를 함수의 인수 목록으로 전달해야 하는 경우가 있다. 

```javascript
const arr = [1, 2, 3];

// 배열 arr의 요소 중에서 최대값을 구하기 위해 Math.max를 사용한다.
const max = Math.max(arr); // -> NaN

const arr = [1, 2, 3];

// 스프레드 문법을 사용하여 배열 arr을 1, 2, 3으로 펼쳐서 Math.max에 전달한다.
// Math.max(...[1, 2, 3])는 Math.max(1, 2, 3)과 같다.
const max = Math.max(...arr); // -> 3
```

### 2. 배열 리터럴 내부에서 사용하는 경우

### 2.1 concat

- 기존의 배열 요소들을 새로운 배열의 일부로 만들고 싶은 경우, 배열 리터럴 만으로 해결할 수 없고 concat 메서드를 사용해야 한다.

```javascript
// ES5
var arr = [1, 2].concat([3, 4]);
console.log(arr); // [1, 2, 3, 4]

// ES6
const arr = [...[1, 2], ...[3, 4]];
console.log(arr); // [1, 2, 3, 4]
```

### 2.2 push

- 기존의 배열에 다른 배열의 요소들을 push하려면 아래와 같은 방법을 사용한다.

```javascript
// ES5
var arr1 = [1, 2];
var arr2 = [3, 4];

Array.prototype.push.apply(arr1, arr2);
// arr1 = arr1.concat(arr2);

console.log(arr1); // [1, 2, 3, 4]

// ES6
const arr1 = [1, 2];
const arr2 = [3, 4];

// arr1.push(3, 4)와 같다.
arr1.push(...arr2);

console.log(arr1); // [1, 2, 3, 4]
```

### 2.3  splice

- 기존의 배열에 다른 배열의 요소들을 삽입하려면 splice 메서드를 사용한다.

```javascript
// ES5
var arr1 = [1, 4];
var arr2 = [2, 3];

// apply 메서드의 2번째 인수는 배열이다. 이것은 인수 목록으로 splice 메서드에 전달된다.
// [1, 0].concat(arr2) → [1, 0, 2, 3]
// arr1.splice(1, 0, 2, 3) → arr1[1]부터 0개의 요소를 제거하고
// 그자리(arr1[1])에 새로운 요소(2, 3)를 삽입한다.
Array.prototype.splice.apply(arr1, [1, 0].concat(arr2));

console.log(arr1); // [1, 2, 3, 4]

// ES6
const arr1 = [1, 4];
const arr2 = [2, 3];

arr1.splice(1, 0, ...arr2);

console.log(arr1); // [1, 2, 3, 4]
```

### 2.4 배열 복사

-  기존의 배열을 복사하기 위해서는 slice 메서드를 사용한다.

```javascript
// ES5
var origin = [1, 2];
var copy = origin.slice();

console.log(copy); // [1, 2]
console.log(copy === origin); // false

// ES6
const origin = [1, 2];
const copy = [...origin];

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```

### 2.5 이터러블을 배열로 변환

- 이터러블을 배열로 변환하려면 slice 메서드를 apply 함수로 호출하는 것이 일반적이다.

```javascript
// ES5
function sum() {
  // 이터러블이면서 유사 배열 객체인 arguments를 배열로 변환
  var args = Array.prototype.slice.apply(arguments);

  return args.reduce(function (pre, cur) {
    return pre + cur;
  }, 0);
}

console.log(sum(1, 2, 3)); // 6

// ES6
function sum() {
  // 이터러블이면서 유사 배열 객체인 arguments를 배열로 변환
  const args = [...arguments];

  return args.reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2, 3)); // 6
```

### 3. 객체 리터럴 내부에서 사용하는 경우

```javascript
// 스프레드 프로퍼티
// 객체 복사(얕은 복사)
const obj = { x: 1, y: 2 };
const copy = { ...obj };
console.log(copy); // { x: 1, y: 2 }
console.log(obj === copy); // false

// 객체 병합
const merged = { x: 1, y: 2, ...{ a: 3, b: 4 } };
console.log(merged); // { x: 1, y: 2, a: 3, b: 4 }
```

