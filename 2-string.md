### 문제 1

두 문자열을 입력받아, 대소문자를 구분하지 않고(case insensitive) 두 문자열이 동일한지를 반환하는 함수를 작성하세요.

예:
```
insensitiveEqual('hello', 'hello'); -> true
insensitiveEqual('hello', 'Hello'); -> true
insensitiveEqual('hello', 'world'); -> false
```

```js
function insensitiveEqual(a, b) {
  // a = a.toUpperCase();
  // b = b.toUpperCase();
  return a.toUpperCase() === b.toUpperCase();
}

// insensitiveEqual('hello', 'hello');
// insensitiveEqual('hello', 'Hello');
insensitiveEqual('hello', 'world');
```

### 문제 2

문자열 `s`와 자연수 `n`을 입력받아, 만약 `s`의 길이가 `n`보다 작으면 `s`의 왼쪽에 공백으로 추가해서 길이가 `n`이 되게 만든 후 반환하고, 아니면 `s`를 그대로 반환하는 함수를 작성해보세요.

예:
```
leftPad('hello', 8); -> '   hello'
leftPad('hello', 3); -> 'hello'
```

```js
function leftPad(s, n) {
  // if(s.length < n) {
  //   return a.padStart(n);
  // } else {
  //   return s;
  // }
  return s.length < n? s.padStart(n): s;
}

// leftPad('hello', 8);
leftPad('hello', 3);
```

### 문제 3

문자열을 입력받아, 문자열 안에 들어있는 모든 모음(a, e, i, o, u)의 갯수를 반환하는 함수를 작성하세요.

```js
function collectionNum(str) {
  let count = 0;
  for(let i=0; i < str.length; i++) {
    if(str[i]==='a' || str[i]==='e' || str[i]==='i' || str[i]==='o' || str[i]==='u') {
      count++;
    }
  }
  return count;
}

collectionNum('discovery');
```

### 문제 4

문자열을 입력받아, 해당 문자열에 포함된 문자의 종류와 갯수를 나타내는 객체를 반환하는 함수를 작성하세요.

예:
```
countChar('tomato'); -> {t: 2, o: 2, m: 1, a: 1}
```

```js
function countChar(str) {
  let obj = {};
  for(let i=0; i < str.length; i++) {
    obj[str[i]] = 0;
  }
  for(let i=0; i < str.length; i++) {
    obj[str[i]]++;
  } 
  return obj;
}

countChar('tomato');
```

### 문제 5

문자열을 입력받아 그 문자열이 회문(palindrome)인지 판별하는 함수를 작성하세요. (회문이란, '토마토', 'never odd or even'과 같이 뒤에서부터 읽어도 똑같이 읽히는 문자열을 말합니다.)

```js
function isPalindrome(str) {
  const arr = str.split(' ').join('');
  // 문자열을 공백 기준으로 분리한 배열로 만든 뒤 합쳐서 공백을 제거한 문자열을 만들고 다시 한글자씩 배열로 만든 뒤 뒤집어서 다시 문자열로 합친다.
  const rev = str.split(' ').join('').split('').reverse().join('');
  
  return arr === rev;
}

isPalindrome('never odd or even');
```

강사님 답안
```js
const isPalindrome = (str) => {
  for(let i=0; i <= (str.length/2)-1; i++) {
    const left = i;
    const right = str.length-1-i;
    if(str[left] !== str[right]) {
      return false;
    }
  }
  return true;
}
```

### 문제 6

문자열을 입력받아, 그 문자열의 모든 '부분 문자열'로 이루어진 배열을 반환하는 함수를 작성하세요.

예:
```
subString('햄버거');
// 결과: ['햄', '햄버', '햄버거', '버', '버거', '거']
```

```js
function subString(str) {
  const arr = new Array();
  for(let i=0; i < str.length; i++) {
    for(let j=i+1; j <= str.length; j++) {
      let str2 = str.substring(i, j);
      arr.push(str2);
    }
  }
  return arr;
}

subString('햄버거');
```
### 문제 7

문자열을 입력받아, 해당 문자열에서 중복된 문자가 제거된 새로운 문자열을 반환하는 함수를 작성하세요.

예:
```
removeDuplicates('tomato'); -> 'toma'
removeDuplicates('bartender'); -> 'bartend'
```

```js
function removeDuplicates(str) {
  let newStr = '';
  for(let i=0; i < str.length; i++) {
    if(newStr.includes(str[i])) {
      continue;
    }
    newStr += str[i];
  }
  return newStr;
}

removeDuplicates('bartender');
```
### 문제 8

이메일 주소를 입력받아, 아이디 부분을 별표(`*`)로 가린 새 문자열을 반환하는 함수를 작성하세요.

- 루프로 먼저 풀어보세요.
```js
// 루프
function hiddenEmail(email) {
  for(let i=0; i < email.length; i++) {
    if(email[i]==='@') {
      break;
    }
    email = email.replace(email[i], '*');
  }
  return email;
}
```

- `split` 메소드를 이용해서 풀어보세요.
```js
// split
function hiddenEmail(email) {
  let arr = email.split('@');
  let length = arr[0].length;
  arr.shift();
  arr.unshift('*'.repeat(length)+'@');
  return arr.join('');
}
```

- 강사님 답안
```js

```

### 문제 9

문자열을 입력받아, 대문자는 소문자로, 소문자는 대문자로 바꾼 결과를 반환하는 함수를 작성하세요.

```js
function change(str) {
  let newStr = '';
  for(let i=0; i < str.length; i++) {
    if(str[i] === str[i].toUpperCase()) {
      newStr += str[i].toLowerCase();
      // str[i] = str[i].toLowerCase(); -> array가 아닌 string에서는 한글자씩 바꾸는게 안된다. 그래서 string 변수 하나 만들고 거기다가 채워넣어야 한다.
    } else {
      newStr += str[i].toUpperCase();
    }
  }
  return newStr;  
}

change('JavaScript');
```
### 문제 10

문자열을 입력받아, 각 단어의 첫 글자를 대문자로 바꾼 결과를 반환하는 함수를 작성하세요. (문자열에 개행이 없다고 가정합니다.)

```js
function capitalization(str) {
  let newStr = '';
  for(let i=0; i < str.length; i++) {
    if(i === 0 || str[i-1] === ' ') {
      newStr += str[i].toUpperCase();
    } else {
      newStr += str[i];
    }
  }
  return newStr;
}

capitalization(`javascript typescript react`);
```

### 문제 11

문자열을 입력받아, 문자열 안에 들어있는 단어 중 가장 긴 단어를 반환하는 함수를 작성하세요. (문자열에 개행이 없다고 가정합니다.)

```js
const longWord = (str) => {
  const splitWord = str.split(' ');
  let max = 0;
  for(let i=1; i < splitWord.length; i++) {
    if(splitWord[max].length < splitWord[i].length) {
      max = i;
    }
  }
  return splitWord[max];
}

longWord('hi hello world');
```

### 문제 12

문자열 `s`과 자연수 `n`을 입력받아, `s`의 첫 `n`개의 문자만으로 이루어진 새 문자열을 반환하는 함수를 작성하세요.

```js
let firstWord = (str, num) => {
  // return str.slice(0, num);
  return Array.from(str).splice(0, num).join('');
}

firstWord('Hello', 4);
```

### 문제 13

Camel case의 문자열을 입력받아, snake case로 바꾼 새 문자열을 반환하는 함수를 작성하세요.

```js
const camelToSnake = str => {
  const arr = Array.from(str);
  const arr2 = Array.from(str);
  for(let i=1; i < arr2.length; i++) {
    if((arr2[i-1] === arr2[i-1].toLowerCase()) && (arr2[i] === arr2[i].toUpperCase())) {
      arr.splice(i, 1, arr[i].toLowerCase());
      arr.splice(i, 0, '-');
    }
  }
  return arr.join('');
}

camelToSnake('helloWorld');
```

### 문제 14

Snake case의 문자열을 입력받아, camel case로 바꾼 새 문자열을 반환하는 함수를 작성하세요.

```js
const snakeToCamel = str => {
  let newStr = '';
  for(let i=0; i < str.length; i++) {
    if(str[i] === '-') {
      newStr += str[i+1].toUpperCase();
      continue;
    } else if(str[i-1] === '-') {
      continue;
    } else {
      newStr += str[i];
    }    
  }
  return newStr;
}

snakeToCamel('hello-world');
```

### 문제 15

`String.prototype.split`과 똑같이 동작하는 함수를 작성하세요.

예:
```
split('Hello World'); -> ['Hello World']
split('Hello World', ' '); -> ['Hello', 'World']
split('let,const,var', ',') -> ['let', 'const', 'var']
```

```js
const split = (item, seperator) => {
  const arr = [];
  let index = 0;

  for(let i=0; i < item.length; i++) {
    if(item[i] === seperator) {
      arr.push(item.slice(index, i));
      index = i + 1;
    } else if(i === item.length-1) {
      // seperator가 없을 경우 여기로 들어와서 실행된다.
      arr.push(item.slice(index, item.length));
    }
  }
  return arr;
}

split('Hello World');
split('let,const,var', ',');
```

### 문제 16

2진수를 표현하는 문자열을 입력받아, 그 문자열이 나타내는 수 타입의 값을 반환하는 함수를 작성하세요. (`parseInt`를 사용하지 말고 작성해보세요.)

예:
```
convertBinary('1101'); -> 13
```

### 문제 17

숫자로만 이루어진 문자열을 입력받아, 연속된 두 짝수 사이에 하이픈(-)을 끼워넣은 문자열을 반환하는 함수를 작성하세요.

예:
```
insertHyphen('437027423'); -> '4370-274-23'
```
