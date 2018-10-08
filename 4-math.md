### 문제 1

양수를 입력받아 이 수를 반지름으로 하는 원의 넓이를 반환하는 함수를 작성하세요.

```js
// 원의 넓이 = 파이 * 반지름 제곱

const circleArea = num => {
  const pie = 3.14
  const area = pie * (num ** 2)

  return area
}

circleArea(5)
```
### 문제 2

두 정수 `min`, `max` 를 입력받아, `min` 이상 `max` 미만인 임의의 정수를 반환하는 함수를 작성하세요.

```js
const randNum = (min, max) => {
  const num = Math.floor(Math.random() * (max - min)) + min
  return num
}

randNum(3, 6)
```
### 문제 3

정수를 입력받아, 5 단위로 올림한 수를 반환하는 함수를 작성하세요.

예:
```
ceilBy5(32); -> 35
ceilBy5(37); -> 40
```

```js
const ceilBy5 = num => {
  arr = [...num.toString()]
  for(let i=arr.length-1; i > arr.length-2; i--) {
    if(arr[i] < 5) {
      arr[i] = 5
    } else if(arr[i] > 5) {
      arr[i] = 0
      arr[i-1] = parseInt(arr[i-1]) + 1
    }
  }
  return parseInt(arr.join(''))
}

ceilBy5(1332)
ceilBy5(1337)
```

### 문제 4

배열을 입력받아, 요소들의 순서를 뒤섞은 새 배열을 반환하는 함수를 작성하세요.

```js
const shuffle = arr => {
  for(let i=arr.length-1; i > 0; i--) {
    let temp
    let j = Math.floor(Math.random() * (i + 1))
    temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
  }
  return arr
}

shuffle([1, 2, 3, 4, 5])
```

### 문제 5

임의의 HTML 색상 코드를 반환하는 함수를 작성하세요.

```js
const randomColorCode = () => {
  const arr = [...Array(3)].reduce(acc => acc.concat(Math.floor(Math.random() * 256)), [])
  
  return `rgb(${arr[0]}, ${arr[1]}, ${arr[2]})`
}

randomColorCode()
```

### 문제 6

양수를 입력받아, 그 수만큼의 길이를 갖는 임의의 문자열을 반환하는 함수를 작성하세요.

```js
function randomString(length) {
  const sample = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'

  return [...Array(length)].reduce(acc => acc + sample[Math.floor(Math.random() * sample.length)], '')
}

randomString(20)
```

### 문제 7

수 타입의 값으로만 이루어진 배열을 입력받아, 그 값들의 표준편차를 구하는 함수를 작성하세요.

강사님 답안
```js
const stdDev = arr => {
  // arr의 평균 구하기
  const sum = arr.reduce((acc, item) => acc + item, 0)
  const mean = (sum/arr.length)
  console.log(`mean: ${mean}`)
  // 각 요소에 대한 편차 구하기 (편차 = 값 - 평균)
  const ps = arr.map(item => item - mean)
  console.log(`ps: ${ps}`)
  // 각 요소에 대해 제곱하기
  const square = ps.map(item => item ** 2)
  console.log(`square: ${square}`)
  // 제곱한 배열의 평균 구하기
  const variation = (square.reduce((acc, item) => acc + item, 0) / square.length)
  console.log(`variation: ${variation}`)
  // 루트 씌우기
  return Math.sqrt(variation) // sqrt === square root (제곱근)
}

stdDev([1, 2, 3, 4, 5])
```
