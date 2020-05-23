# 30. Date

- 표준 빌트인 객체(standard built-in object)인 Date는 날짜와 시간(년, 월, 일, 시, 분, 초, 밀리초(천분의 1초(millisecond, ms)))을 위한 메소드를 제공하는 빌트인 객체이면서 생성자 함수이다

### 1. Date 생성자 함수

- Date는 생성자 함수이다. Date 생성자 함수는 날짜와 시간을 가지는 인스턴스를 생성한다. 
- 현재 날짜와 시간이 아닌 다른 날짜와 시간을 다루고 싶은 경우, Date 생성자 함수에 명시적으로 해당 날짜와 시간 정보를 인수로 지정한다. 

### 1.1 new Date()

- Date 생성자 함수에 인수를 전달하지 않으면 현재 날짜와 시간을 가지는 인스턴스를 반환한다.

```javascript
const today = new Date();
// -> Thu Mar 26 2020 14:03:18 GMT+0900 (대한민국 표준시)
```

### 1.2 new Date(milliseconds)

- Date 생성자 함수에 숫자 타입의 밀리초를 인수로 전달하면 1970년 1월 1일 00:00(UTC)을 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 가지는 인스턴스를 반환한다.

### 1.3 new Date(dateString)

- Date 생성자 함수에 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환한다.

### 1.4 new Date(year, month[, day, hour, minute, second, millisecond])

- 인수로 년, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환한다. 이때 년, 월은 반드시 지정하여야 한다. 지정하지 않은 옵션 정보는 0 또는 1으로 초기화된다.

| 인수        | 내용                                                         |
| :---------- | :----------------------------------------------------------- |
| year        | 1900년 이후의 년                                             |
| month       | 월을 나타내는 **0 ~ 11**까지의 정수 (주의: 0부터 시작, 0 = 1월) |
| day         | 일을 나타내는 1 ~ 31까지의 정수                              |
| hour        | 시를 나타내는 0 ~ 23까지의 정수                              |
| minute      | 분을 나타내는 0 ~ 59까지의 정수                              |
| second      | 초를 나타내는 0 ~ 59까지의 정수                              |
| millisecond | 밀리초를 나타내는 0 ~ 999까지의 정수                         |

### 1.5 Date 생성자 함수를 new 연산자없이 호출

- Date 생성자 함수를 new 연산자없이 호출하면 인스턴스를 반환하지 않고 결과값을 문자열로 반환한다.

### 2. Date 메소드

### 2.1 Date.now

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환한다.

### 2.2 Date.parse

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간(new Date(dateString)의 인수와 동일한 형식)까지의 밀리초를 숫자로 반환한다.

### 2.3 Date.UTC

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환한다.

### 2.4 Date.prototype.getFullYear

- 년도를 나타내는 4자리 숫자를 반환한다.

### 2.5 Date.prototype.setFullYear

- Date 객체에 년도를 나타내는 4자리 숫자를 설정한다. 년도 이외에 옵션으로 월, 일도 설정할 수 있다.

### 2.6 Date.prototype.getMonth

- 월을 나타내는 0 ~ 11의 정수를 반환한다. 1월은 0, 12월은 11이다.

### 2.7 Date.prototype.setMonth

- Date 객체에 월을 나타내는 0 ~ 11의 정수를 설정한다. 1월은 0, 12월은 11이다. 월 이외에 옵션으로 일도 설정할 수 있다.

### 2.8 Date.prototype.getDate

- 날짜(1 ~ 31)를 나타내는 정수를 반환한다.

### 2.9 Date.prototype.setDate

- Date 객체에 날짜(1 ~ 31)를 나타내는 정수를 설정한다.

### 2.10 Date.prototype.getDay

- 요일(0 ~ 6)를 나타내는 정수를 반환한다. 

|  요일  | 반환값 |
| :----: | :----: |
| 일요일 |   0    |
| 월요일 |   1    |
| 화요일 |   2    |
| 수요일 |   3    |
| 목요일 |   4    |
| 금요일 |   5    |
| 토요일 |   6    |

### 2.11 Date.prototype.getHours

- 시간(0 ~ 23)를 나타내는 정수를 반환한다.

### 2.12 Date.prototype.setHours

- Date 객체에 시간(0 ~ 23)를 나타내는 정수를 설정한다. 시간 이외에 옵션으로 분, 초, 밀리초도 설정할 수 있다.

### 2.13 Date.prototype.getMinutes

- 분(0 ~ 59)를 나타내는 정수를 반환한다. 

### 2.14 Date.prototype.setMinutes

- Date 객체에 분(0 ~ 59)를 나타내는 정수를 설정한다. 분 이외에 옵션으로 초, 밀리초도 설정할 수 있다.

### 2.15 Date.prototype.getSeconds

- 초(0 ~ 59)를 나타내는 정수를 반환한다.

### 2.16 Date.prototype.setSeconds

- Date 객체에 초(0 ~ 59)를 나타내는 정수를 설정한다. 초 이외에 옵션으로 밀리초도 설정할 수 있다.

### 2.17 Date.prototype.getMilliseconds

- 밀리초(0 ~ 999)를 나타내는 정수를 반환한다.

### 2.18 Date.prototype.setMilliseconds

- Date 객체에 밀리초(0 ~ 999)를 나타내는 정수를 설정한다.

### 2.19 Date.prototype.getTime

- 1970년 1월 1일 00:00:00(UTC)를 기점으로 현재 시간까지 경과된 밀리초를 반환한다.

### 2.20 Date.prototype.setTime

- Date 객체에 1970년 1월 1일 00:00:00(UTC)를 기점으로 현재 시간까지 경과된 밀리초를 설정한다.

### 2.21 Date.prototype.getTimezoneOffset

- UTC와 지정 로케일(Locale) 시간과의 차이를 분단위로 반환한다. KST(Korea Standard Time)는 UTC에 9시간을 더한 시간이다. 즉, UTC = KST - 9h이다.

### 2.22 Date.prototype.toDateString

- 사람이 읽을 수 있는 형식의 문자열로 날짜를 반환한다.

### 2.23 Date.prototype.toISOString

- ISO 8601 형식으로 날짜와 시간을 표현한 문자열을 반환한다.

### 2.24 Date.prototype.toLocaleString

- 인수로 전달한 로케일을 기준으로 날짜와 시간을 표현한 문자열을 반환한다. 

### 2.25 Date.prototype.toLocaleTimeString

- 인수로 전달한 로케일을 기준으로 시간을 표현한 문자열을 반환한다. 

### 2.26 Date.prototype.toTimeString

- 사람이 읽을 수 있는 형식으로 시간을 표현한 문자열을 반환한다.

### 