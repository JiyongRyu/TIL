1. 

```
var x = 21;

if (x > 10 && x < 20) {
  console.log(x);
}

```

2.

```
for (var i = 0; i < 10; i++) {
  if (i % 2 === 0) {
    console.log(i);
  }
}
```

3.

```
var str = '';
for (var i = 0; i < 10; i++) {
  if (i % 2 === 0) {
    str += i;
  }
}

console.log(str);

```

4.

```
for (var i = 10; i > 0; i--) {
  if (i % 2) {
    console.log(i);
  }
}
```

5.

```
var i = 0;

while (i < 10) {
  if (i % 2 === 0) {
    console.log(i);
  }
  i++;
}
```

6.

```
var n = 10;

while (n > 0) {
  if (n % 2) {
    console.log(n);
  }
  n--;
}

```

7.

```
var sum = 0;

for (var i = 0; i < 10; i++) {
  sum += i;
}

console.log(sum);
```

8.

```
var sum = 0;

for (var i = 0; i < 20; i++) {
  if (i % 2 && i % 3) {
  sum += i;
  }
}

console.log(sum);
```

9. 

```
var sum = 0;

for (var i = 0; i < 20; i++) {
  if (i % 2 === 0 || i % 3 === 0) {
  sum += i;
  }
}

console.log(sum);

```

10.

```
for (var i = 1; i < 6; i++) {
  for (var j = 1; j < 6; j++) {
    if (i + j === 6) {
      console.log([i, j]);
    }
  }
}
```

11.

```
var star = '';

for (var i = 0; i < 5; i++) {
  for (var j = 0; j <= i; j++) {
    star += '*';
  }
  star += '\n';
}

console.log(star);
```

12.

```
var star = '';

for (var i = 0; i < 5; i++) {
  for (var j = 0; j < i; j++) {
    star += ' ';
  }
  for (var k = i; k < 5; k++) {
    star += '*';
  }
  star += '\n';
}

console.log(star);

```

13.

```
var star = '';

for (var i = 0; i < 5; i++) {
  for (var j = 5; j > i; j--) {
    star += '*';
  }
  star += '\n';
}

console.log(star);

```

14.

```
var star = '';

for (var i = 5; i > 0; i--) {
  for (var j = i - 1; j > 0; j--) {
    star += ' ';
  }
  for (var k = i - 1; k < 5; k++) {
    star += '*';
  }
  star += '\n';
}

console.log(star);
```

15.

```
var star = '';

for (var i = 0; i < 5; i++) {
  for (var j = 4; j > i; j--) {
    star += ' ';
  }
  for (var k = 0; k < (i * 2) + 1; k++) {
    star += '*';
  }
  star += '\n';
}

console.log(star);
```

16.

```
var star = '';

for (var i = 5; i > 0; i--) {
  for (var j = 5; j > i; j--) {
    star += ' ';
  }
  for (var k = 0; k < (i * 2) - 1; k++) {
    star += '*';
  }
  star += '\n';
}

console.log(star);
```

