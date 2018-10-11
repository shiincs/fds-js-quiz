### 문제 1

두 정수 `start`, `end`를 입력받아, `start`부터 `end`까지의 모든 정수를 배열로 반환하는 함수를 작성하세요.

예:
```
range(3, 6); -> [3, 4, 5, 6]
```

```js
const range = (start, end) => {
  const arr = []
  for(let i=start; i <= end; i++) {
    arr.push(i)
  }
  return arr
}

range(3, 6)
```

### 문제 2

수 타입의 값으로만 이루어진 배열을 입력받아, 그 값들의 합을 구하는 함수를 작성하세요.

```js
const sum = arr => {
  // return arr.reduce((x, y) => x + y, 0)
  let sum = 0;
  for(let i=0; i < arr.length; i++) {
    sum += arr[i]
  }
  return sum;
}

sum([1, 2, 3, 4, 5])
```

### 문제 3

배열을 입력받아, falsy인 요소가 제거된 새 배열을 반환하는 함수를 작성하세요.

```js
const removeFalsy = arr => {
  return arr.filter(item => item !== false && item !== null && item !== undefined && item !== 0 && !Number.isNaN(item) && item !== '')
}

removeFalsy([0, 1, null, undefined, false, NaN, ''])
```

강사님 답안
```js
function removeFalsy(arr) {
  const newArr = []
  for(let i=0; i < arr.length; i++) {
    if(arr[i]) {  // 조건문 안이 true 일 경우 (=== falsy가 아닐 경우)
      newArr.push(arr[i])
    }
  }
  return newArr
}
```

### 문제 4

배열을 입력받아, 중복된 요소가 제거된 새 배열을 반환하는 함수를 작성하세요.

```js
const removeDuplicate = arr => {
  const newArr = []
  for(let i=0; i < arr.length; i++) {
    if(!newArr.includes(arr[i])) {
      newArr.push(arr[i])
    } else continue
  }
  return newArr
}

removeDuplicate([1, 1, 2, 3, 3, 4, 5])
```

### 문제 5

수 타입의 값으로만 이루어진 두 배열을 입력받아, 다음과 같이 동작하는 함수를 작성하세요.
- 두 배열의 같은 자리에 있는 요소를 더한 결과가 새 배열의 요소가 됩니다.
- 만약 입력받은 두 배열의 길이가 갖지 않다면, 긴 배열에 있는 요소를 새 배열의 같은 위치에 포함시키세요.

예:
```
addArray([1, 2, 3], [4, 5, 6, 7]) -> [5, 7, 9, 7]
```

```js
function arrPush(arr1, arr2) {
  const newArr = []
  for(let i=0; i < arr1.length; i++) {
    newArr.push(arr1[i]+arr2[i])
  }
  return newArr
}

const addArray = (arr1, arr2) => {
  const firstLength = arr1.length
  const secondLength = arr2.length

  if(firstLength - secondLength > 0) {
    arr2.length = arr1.length
    arr2.fill(0, secondLength, firstLength)
    return arrPush(arr1, arr2);
  } else {
    arr1.length = arr2.length
    arr1.fill(0, firstLength, secondLength)
    return arrPush(arr1, arr2);
  }
}

addArray([1, 2, 3, 5, 6], [4, 5, 6, 7])
```

```js
// 강사님 답안
function addArray(arr1, arr2) {
  let longer
  let shorter
  if(arr1.length > arr2.length) {
    longer = arr1.slice() // 원본 배열이 바뀐다는 문제를 해결하기 위해 배열을 복사해서 사본을 만든다.
    shorter = arr2.slice()
  } else {
    longer = arr2.slice()
    shorter = arr1.slice()
  }
  for(let i=0; i < shorter.length; i++) {
    longer[i] += shorter[i]
  }
  return longer
}

const ARR1 = [1, 2, 3]
const ARR2 = [4, 5, 6, 7]
addArray(ARR1, ARR2)
```

### 문제 6

배열을 입력받아, 배열의 요소 중 두 개를 선택하는 조합을 모두 포함하는 배열을 작성하세요.

예:
```
combination([1, 2, 3]); -> [[1, 2], [1, 3], [2, 3]]
```

```js
const combination = arr => {
  const newArr = new Array()
  for(let i=0; i < arr.length; i++) {
    for(let j=i+1; j < arr.length; j++) {
      const innerArr = new Array()
      innerArr.push(arr[i])
      innerArr.push(arr[j])
      newArr.push(innerArr)
    }    
  }
  return newArr
}

combination([1, 2, 3])
```

강사님 답안
```js
const combination = arr => {
  const newArr = new Array()
  for(let i=0; i < arr.length - 1; i++) {
    for(let j=i+1; j < arr.length; j++) {
      newArr.push([arr[i], arr[j]])
    }    
  }
  return newArr
}

combination([1, 2, 3])
```

### 문제 7

'금액'과 '동전의 종류가 들어있는 배열'를 입력받아, 최소한의 동전을 사용해서 금액을 맞출 수 있는 방법을 출력하는 함수를 작성하세요.
(단, 동전의 종류가 들어있는 배열에는 큰 동전부터 순서대로 들어있다고 가정합니다.)

예:
```
coins(263, [100, 50, 10, 5, 1]);
// 출력
100
50
10
1
1
1
```

```js
const coins = (price, coins) => {
  for(let i=0; i < coins.length; i++) {
    if(price <= 0) break
    for(let j=0; j < coins.length; j++) {
      if(price < coins[i]) {
        break
      } else {
        price = price-coins[i]
        console.log(coins[i])
      }      
    }
  }
}

coins(263, [100, 50, 10, 5, 1]);
```

강사님 답안(1)
```js
function coins(input, coinTypes) {
  // coinTypes를 내림차순 정렬
  coinTypes.sort((x, y) => y - x)
  // 남은 액수
  let remain = input
  // 현재 내가 보고 있는 동전
  let currentIndex = 0
  while(remain > 0 && currentIndex < coinTypes.length) {  // 더이상 가진 동전으로 뺄 수 없을 경우를 방어해야 한다.
    // 남은 액수가 내가 지금 보고있는 동전보다 크거나 같으면
    if(remain >= coinTypes[currentIndex]) {
      console.log(coinTypes[currentIndex])
      remain -= coinTypes[currentIndex]
    } else {
      // 다음 동전으로 넘어간다.
      currentIndex++
    }
  }
}

coins(263, [50, 100, 10, 5]);
```

강사님 답안(2)
```js
function coins(input, coinTypes) {
  // coinTypes를 내림차순 정렬
  coinTypes.sort((x, y) => y - x)
  // 남은 액수
  let remain = input
  // 현재 내가 보고 있는 동전
  for(let i=0; i < coinTypes.length; i++) {
    while(coinTypes[i] <= remain) {
      remain -= coinTypes[i]
      console.log(coinTypes[i])
    }
  }
}
```

### 문제 8

수 타입의 값만 들어있는 배열을 입력받아, 해당 배열을 오름차순 정렬하는 함수를 작성하세요. (`Array.prototype.sort`를 사용하지 않고 작성해보세요. [선택 정렬](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)을 참고하세요.)

```js
const sortAscending = arr => {
  for(let i=0; i < arr.length; i++) {
    for(let j=i+1; j < arr.length; j++) {
      if(arr[i] > arr[j]) {
        let temp;
        temp = arr[i]
        arr[i] = arr[j]
        arr[j] = temp
      }
    }
  }
  return arr
}

sortAscending([5000, 1, 20, 3, 400])
```

### 문제 9

배열을 입력받아, 해당 배열에 들어있는 요소들 중 최대값을 찾는 함수를 작성하세요. (루프 & reduce를 이용하세요)

예:
```
max([3, 1, 4, 5, 2]) // -> 5
```

```
// reduce 이용
const max = arr => {
  // reduce를 쓸 때
  // '누적값의 역할'이 무엇인지를 잘 정하는 것이 중요하다.

  // 누적값: 지금까지 봤던 숫자 중에 제일 큰 수
  return arr.reduce((acc, item) => { 
    // 안에 들어있는 함수의 반환값이, 다음 단계의 누적값이 된다.
    if(acc > item) {
      return acc
    } else {
      return item
    }
  }, 0)
}
```

```
// loop 이용
const max = arr => {
  let max = -Infinity;
  for(const item of arr) {
    if(max < item) {
      max = item;
    }
  }
  return max;
}

max([-1, -2, -7, -3, -5, -4])
```

### 문제 10

2차원 배열을 입력받아 1차원 배열로 바꾸는 함수를 작성하세요. (루프 & reduce를 이용하세요)

예:
```
flatten([
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]) // -> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```js
// reduce 이용
const flatten = arr => {
  return arr.reduce((acc, item) => {
    // Array 객체의 concat 메서드는 한 개 이상의 배열을 인수로 받아서 메서드를 호출한 배열의 끝에 인수로 받은 배열의 원소를 추가한다. 이렇게 합쳐진 배열은 새로운 배열로 반환된다.
    return acc.concat(item)
  }, [])
}
```

```js
// loop 이용
function flatten(arr) {
  const newArr = new Array();
  // i 루프는 중간 배열을 뽑아내기 위한 루프
  for(let i=0; i < arr.length; i++) {
    // j 루프는 중간 배열 내부의 원소들을 뽑아내기 위한 루프
    for(let j=0; j < arr[i].length; j++) {
      newArr.push(arr[i][j])
    }
  }
  return newArr
}

flatten([
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
])
```

강사님 답안
```js
function flatten(arr) {
  // 누적값: 지금까지 본 배열이 다 이어붙여진 새 배열
  return arr.reduce((acc, innerArr) => acc.concat(innerArr), [])
}
```

### 문제 11

(3 * 3) 빙고 판을 표현한 배열을 입력받아, 빙고인 경우 true, 아니면 false를 반환하는 함수를 작성하세요. (단, 칸이 비어있는 경우는 0, 칸이 채워져 있는 경우는 1로 표현합니다.)

예:
```
bingo([
  [0, 1, 0],
  [0, 1, 1],
  [0, 0, 1]
]) // -> false

bingo([
  [1, 1, 0],
  [0, 1, 1],
  [0, 0, 1]
]) // -> true

bingo([
  [0, 1, 0],
  [0, 1, 1],
  [0, 1, 1]
]) // -> true
```

```
// 루프를 사용하긴 했지만 노가다 그 자체...
const bingo = arr => {
  // 수평 빙고 확인
  const isHorizontal = arr.some(item => item.every(item => item === 1))

  // 수직 빙고 확인
  const verticalArr = []
  for(let i=0; i < arr.length; i++) {
    const innerArr = []
    for(let j=0; j < arr[i].length; j++) {      
      innerArr.push(arr[j][i])
    }
    verticalArr.push(innerArr)
  }
  const isVertical = verticalArr.some(item => item.every(item => item === 1))

  // 왼->오 대각선 빙고 확인
  let leftTopToRightBottom = true;
  for(let i=0; i < arr.length; i++) {
    for(let j=0; j < arr.length; j++) {
      if(i===j) {
        if(arr[i][j] === 1) {
          break
        } else if(arr[i][j] !== 1) {
          leftTopToRightBottom = false
          break
        }        
      }
    }
  }
  
  // 오 -> 왼 대각선 빙고 확인
  let rightTopToLeftBottom = true
  for(let i=0; i < arr.length; i++) {
    for(let j=arr.length-1-i; j >= 0; j--) {
      if(arr[i][j] === 1) {
        break
      } else if(arr[i][j] !== 1) {
        rightTopToLeftBottom = false
        break
      }
    }
  }

  console.log(`수평 빙고: ${isHorizontal}`);
  console.log(`수직 빙고: ${isVertical}`);
  console.log(`왼->오 대각선: ${leftTopToRightBottom}`);
  console.log(`오->왼 대각선: ${rightTopToLeftBottom}`);

  if(isHorizontal || isVertical || leftTopToRightBottom || rightTopToLeftBottom) {
    return `빙고!`
  } else {
    return `빙고가 없습니다 ㅠㅠ`
  }
}

bingo([
  [1, 1, 1],
  [1, 1, 0],
  [1, 1, 1]
]) // -> true
```

### 문제 12

(9 * 9) 오목 판을 표현한 배열을 입력받아, 흑이 이긴 경우 1, 백이 이긴 경우 2, 아무도 이기지 않은 경우 0을 반환하는 함수를 작성하세요. (단, 칸이 비어있는 경우는 0, 흑은 1, 백은 2로 표현합니다.)

예:
```
omok([
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 1, 0, 0, 0, 2, 0, 0],
  [0, 0, 0, 1, 0, 0, 2, 0, 0],
  [0, 0, 0, 0, 1, 0, 2, 0, 0],
  [0, 0, 0, 0, 0, 1, 2, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
]) // -> 0

omok([
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 1, 0, 0, 0, 2, 0, 0],
  [0, 0, 0, 1, 0, 0, 2, 0, 0],
  [0, 0, 0, 0, 1, 0, 2, 0, 0],
  [0, 0, 0, 0, 0, 1, 2, 0, 0],
  [0, 0, 0, 0, 0, 0, 1, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
]) // -> 1

omok([
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 1, 0, 0, 0, 2, 0, 0],
  [0, 0, 0, 1, 0, 0, 2, 0, 0],
  [0, 0, 0, 0, 1, 0, 2, 0, 0],
  [0, 0, 0, 0, 0, 1, 2, 0, 0],
  [0, 0, 0, 0, 0, 0, 2, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 0],
]) // -> 2
```

```js
const omok = arr => {
  let newArr = []

  // 수평 오목
  for(let i=0; i < arr.length; i++) {
    for(let j=0; j < arr[i].length-(arr[i].length-5); j++) {
      // newArr = arr[i].slice(j, j+5)
      if(arr.some(item => item.slice(j, j+5).every(item => item === 1))) {
        return 1
      } else if(arr.some(item => item.slice(j, j+5).every(item => item === 2))) {
        return 2
      }
    }
  }

  // 수직 오목
  // 수직 열을 수평 배열로 만들어서 저장한다.
  for(let i=0; i < arr.length; i++) {
    let innerArr = []
    for(let j=0; j < arr[i].length; j++) {
      innerArr.push(arr[j][i])
    }
    newArr.push(innerArr)
  }
  // 새로운 배열을 수평 오목 판별법으로 판별한다.
  for(let i=0; i < newArr.length; i++) {
    for(let j=0; j < newArr[i].length-(newArr[i].length-5); j++) {
      // newArr = arr[i].slice(j, j+5)
      if(newArr.some(item => item.slice(j, j+5).every(item => item === 1))) {
        return 1
      } else if(newArr.some(item => item.slice(j, j+5).every(item => item === 2))) {
        return 2
      }
    }
  }
  
  // 왼->오 대각선 오목
  for(let i=0; i < arr.length-4; i++) {
    for(let j=0; j < arr[i].length-4; j++) {
        if(arr[i][j]===1 && arr[i+1][j+1]===1 && arr[i+2][j+2]===1 && arr[i+3][j+3]===1 && arr[i+4][j+4]===1) {
          return 1
        } else if(arr[i][j]===2 && arr[i+1][j+1]===2 && arr[i+2][j+2]===2 && arr[i+3][j+3]===2 && arr[i+4][j+4]===2) {
          return 2
        }
    }
  }
  
  // 오->왼 대각선 오목
  for(let i=0; i < arr.length-4; i++) {
    for(let j=arr[i].length-1; j >= arr[i].length-5 ; j--) {
      if(arr[i][j]===1 && arr[i+1][j-1]===1 && arr[i+2][j-2]===1 && arr[i+3][j-3]===1 && arr[i+4][j-4]===1) {
        return 1
      } else if(arr[i][j]===2 && arr[i+1][j-1]===2 && arr[i+2][j-2]===2 && arr[i+3][j-3]===2 && arr[i+4][j-4]===2) {
        return 2
      }
    }
  }

  // 모든 판별법에 해당되지 않는다면 0을 return 한다.  
  return 0
}
```
### 문제 13

배열을 입력받아, 요소 중 아무거나 하나를 골라서 반환하는 함수를 작성하세요.

예:
```
randomItem([1, 2, 3, 4, 5]) // 1, 2, 3, 4, 5 중 아무거나 반환
```

```js
const randomItem = arr => {
  const index = Math.floor(Math.random() * arr.length)
  return arr[index]
}

randomItem([1, 2, 3, 4, 5])
```

### 문제 14

배열을 입력받아, 요소들의 순서를 뒤섞은 새 배열을 반환하는 함수를 작성하세요. (단, 원본 배열이 변경되어서는 안 됩니다.)

예:
```
shuffle([1, 2, 3, 4, 5]) // [3, 1, 4, 5, 2] 와 같이 순서가 뒤섞인 새 배열 반환
```

```js
const shuffle = arr => {
  const newArr = []
  for(let i=0; i < Infinity; i++) {
    const randomIndex = Math.floor(Math.random() * arr.length)
    if(!newArr.includes(arr[randomIndex])) {
      newArr.push(arr[randomIndex])
    }
    if(newArr.length === arr.length) {
      break
    }
  }
  return newArr
}

shuffle([1, 2, 3, 4, 5])
```

```js
function shuffle(arr) {
  const newArr = arr.slice()
  for(let i=newArr.length-1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1));
    [newArr[i], newArr[j]] = [newArr[j], newArr[i]];
  }
  console.log(`원본 배열: [${arr}]`)
  console.log(`새 배열: [${newArr}]`)
  return newArr
}

shuffle([1, 2, 3, 4, 5])
```