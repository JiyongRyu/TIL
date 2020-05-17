# 29. Math

### 1. Math 프로퍼티

### 1.1 Math.PI

- 원주율 PI 값(π ≈ 3.141592653589793)을 반환한다.

### 2. Math 메소드

### 2.1 Math.abs

- 전달받은 인수의 절댓값(absolute value)을 반환한다. 절댓값은 반드시 0 또는 양수이어야 한다.

### 2.2 Math.round

- 전달받은 인수의 소수점 이하를 반올림한 정수를 반환한다.

### 2.3 Math.ceil

- 전달받은 인수의 소수점 이하를 올림한 정수를 반환한다.

### 2.4 Math.floor

- 전달받은 인수의 소수점 이하를 내림한 정수를 반환한다. Math.ceil의 반대 개념이다.
- 전달받은 인수가 양수인 경우, 소수점 이하를 떼어 버린 다음 정수를 반환하고, 음수인 경우, 소수점 이하를 떼어 버린 다음 -1을 한 정수를 반환한다.

### 2.5 Math.sqrt

- 전달받은 인수의 제곱근을 반환한다.

### 2.6 Math.random

- 임의의 부동 소수점을 반환한다. 반환된 부동 소수점은 0부터 1 미만이다. 즉, 0은 포함되지만 1은 포함되지 않는다.

### 2.7 Math.pow

- 첫번째 인수를 밑(base), 두번째 인수를 지수(exponent)로하여 거듭제곱을 반환한다.

```javascript
Math.pow(2, 8);  // -> 256
Math.pow(2, -1); // -> 0.5
Math.pow(2);     // -> NaN

// ES7(ECMAScript 2016) Exponentiation operator(거듭 제곱 연산자)
2 ** 8; // -> 256
```

### 2.8 Math.max

- 전달받은 인수 중에서 가장 큰 수를 반환한다.

```javascript
Math.max(1, 2, 3); // -> 3

// 배열 요소 중에서 최대값 취득
const arr = [1, 2, 3];
const max = Math.max.apply(null, arr); // -> 3

// ES6 스프레드 문법
Math.max(...arr); // -> 3
```



### 2.9 Math.min

- 전달받은 인수 중에서 가장 작은 수를 반환한다.

```javascript
Math.min(1, 2, 3); // -> 1

// 배열 요소 중에서 최소값 취득
const arr = [1, 2, 3];
const min = Math.min.apply(null, arr); // -> 1

// ES6 스프레드 문법
Math.min(...arr); // -> 1
```

