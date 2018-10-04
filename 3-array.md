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
