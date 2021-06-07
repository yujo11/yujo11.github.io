---
title: 'Javascript의 callback'
date: 2021-03-22 09:03:18
category: 'JavaScript'
draft: false
---

## 1. 동기와 비동기

Javascript는 동기적(synchronous)으로 동작합니다. Javascript 코드를 동작시키면 위에서부터 순차적으로 실행됩니다.

```js
console.log(1)
console.log(2)
console.log(3)
```

위와 같은 코드를 실행 시켰을 때 `1, 2, 3`이 순서대로 출력되는걸 예상할 수 있습니다. 그렇다면 다음 코드는 어떻게 실행될까요?

```js
console.log(1)
setTimeout(() => console.log(2), 100)
console.log(3)
```

위 코드는 `1, 3, 2`의 순서로 출력됩니다. 이 때 `setTimeout`의 인자로 넘긴 `() => console.log(2)`가 바로 오늘 알아볼 콜백 함수입니다.

## 2. 콜백 함수란?

콜백 함수는 다른 코드의 인자로 넘겨주는 함수입니다. 콜백 함수를 넘겨받은 코드는 콜백 함수를 필요에 따라 적절한 시점에 실행합니다.

### 2-1. 콜백 함수의 제어권

콜백 함수를 다른 함수의 매개변수로 전달할 때 콜백함수를 받은 함수는 콜백 함수의 제어권을 가집니다.

```js
const arr = ['무', '야', '호']
const mooyaho = () => {
  console.log(arr.shift())
  if (!arr.length) {
    clearInterval(timer)
  }
}

const timer = setInterval(mooyaho, 500)
> 무 (0.5초)
  야 (1.0초)
  호 (1.5초)
```

예시를 위해 위와 같은 함수를 작성해보았습니다. `setInterval`의 매개변수로 넘긴 `mooyaho`의 호출시점은 `setInterval`내에서 결정됩니다. 함수의 제어권을 `setInterval`이 가지게 된거죠.

### 2-2. Callback이 필요한 이유

자바스크립트에서 비동기처리를 하기 위해 Callback이 필요합니다. 동기적으로 실행되는 자바스크립트의 특성상 다음과 같은 코드를 작성할 경우 제대로 요청을 받을 수 없습니다.

```js
// ajax()는 ajax요청을 보내는 가상의 함수
const response = ajax('...');

console.log(response);
> undefined
```

위 코드에서 undefined가 출력되는 것은 response에 ajax의 응답값이 담기는걸 기다리지 않고 바로 다음 줄의 `console.log()`를 실행하기 때문입니다. 서버와의 요청을 주고받는 것처럼 요청에 대한 응답을 받은 후 다음 로직을 실행하기 위한 경우 callback을 사용하게 됩니다.

## 3. 콜백 지옥

콜백 지옥(callback hell)은 콜백 함수를 익명 함수로 전달하는 과정이 반복되어 코드의 들여쓰기 수준이 감당하기 힘들정도로 깊어지는 현상을 얘기합니다. 주로 이벤트 처리나 서버 통신과 같은 비동기적인 작업을 수행하기 위해 이런 형태가 자주 등장하는데, 가독성이 떨어지면서 코드를 수정하기 어렵습니다.

### 3-1. 콜백 지옥 예시

```javascript
setTimeout(
  name => {
    let coffeeList = name
    console.log(coffeeList)

    setTimeout(
      name => {
        coffeeList += ', ' + name
        console.log(coffeeList)

        setTimeout(
          name => {
            coffeeList += ', ' + name
            console.log(coffeeList)

            setTimeout(
              name => {
                coffeeList += ', ' + name
                console.log(coffeeList)
              },
              500,
              'Latte'
            )
          },
          500,
          'Mocha'
        )
      },
      500,
      'Americano'
    )
  },
  500,
  'Espresso'
)
```

위 코드는 0.5초마다 커피 목록을 수집하고 출력합니다.

```javascript
> 출력값
Espresso (0.5초)
Espresso, Americano (1.0초)
Espresso, Americano, Mocha (1.5초)
Espresso, Americano, Mocha, Latte (2.0초)
```

각 콜백은 커피 이름을 전달하고 목록에 이름을 추가합니다. 정상적으로 실행되지만 들여쓰기 수준이 과도하게 깊어지고 값이 아래에서 위로 전달되어 가독성이 떨어집니다.

### 3-2. 콜백 지옥을 탈출하는 방법 1. 기명함수

독성 문제와 어색함을 동시에 해결하는 가장 간단한 방법은 익명의 콜백 함수를 모두 기명함수로 전환하는 것입니다.

```javascript
let coffeeList = ''

const addEspresso = name => {
  coffeeList = name
  console.log(coffeeList)
  setTimeout(addAmericano, 500, 'Americano')
}

const addAmericano = name => {
  coffeeList += ', ' + name
  console.log(coffeeList)
  setTimeout(addMocha, 500, 'Mocha')
}

const addMocha = name => {
  coffeeList += ', ' + name
  console.log(coffeeList)
  setTimeout(addLatte, 500, 'Latte')
}

const addLatte = name => {
  coffeeList += ', ' + name
  console.log(coffeeList)
}

setTimeout(addEspresso, 500, 'Espresso')
```

위 코드는 익명함수를 모두 기명함수로 변경한 코드입니다. 이 방식은 코드의 가독성을 높일 수 있고 함수 선언과 함수 호출만 구분할 수 있다면 위에서부터 아래로 순서대로 읽는데 어려움이 없습니다. 하지만 일회성 함수를 전부 변수에 할당하는 것은 코드명을 일일이 따라다녀야 하기 때문에 오히려 헷갈림을 유발할 소지가 있습니다.

### 3-3. 콜백 지옥을 탈출하는 방법 2. Promise

```javascript
new Promise(resolve => {
  setTimeout(() => {
    let name = 'Espresso'
    console.log(name)
    resolve(name)
  }, 500)
})
  .then(prevName => {
    return new Promise(resolve => {
      setTimeout(() => {
        let name = prevName + ', Americano'
        console.log(name)
        resolve(name)
      }, 500)
    })
  })
  .then(prevName => {
    return new Promise(resolve => {
      setTimeout(() => {
        let name = prevName + ', Mocha'
        console.log(name)
        resolve(name)
      }, 500)
    })
  })
  .then(prevName => {
    return new Promise(resolve => {
      setTimeout(() => {
        let name = prevName + ', Latte'
        console.log(name)
        resolve(name)
      }, 500)
    })
  })
```

위 코드는 ES6의 `Promise`를 이용한 방식입니다. new 연산자와 함께 호출한 `Promise`의 인자로 넘겨주는 콜백 함수는 호출할 때 바로 실행되지만 그 내부에 `resolve` 또는 `reject`함수를 호출하는 구문이 있을 경우 둘 중 하나가 실행되기 전까지는 `then`또는 `catch`로 넘어가지 않습니다. 따라서 비동기 작업이 완료될 때 `resolve` 또는 `reject`를 호출하는 방법으로 비동기 작업의 동기적 표현이 가능해집니다.

```javascript
const addCoffee = name => {
  return prevName => {
    return new Promise(resolve => {
      setTimeout(() => {
        const newName = prevName ? `${prevName}, ${name}` : name
        console.log(newName)
        resolve(newName)
      }, 500)
    })
  }
}

addCoffee('Espresso')()
  .then(addCoffee('Americano'))
  .then(addCoffee('Mocha'))
  .then(addCoffee('Latte'))
```

위와 같이 반복적인 내용을 함수화해서 짧게 표현할 수도 있습니다.

### 3-4. 콜백 지옥을 탈출하는 방법 3. async/await

```javascript
const addCoffee = name => {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(name)
    }, 500)
  })
}

const coffeeMaker = async () => {
  let coffeeList = ''
  let _addCoffee = async name => {
    coffeeList += (coffeeList ? ', ' : '') + (await addCoffee(name))
  }
  await _addCoffee('Espresso')
  console.log(coffeeList)
  await _addCoffee('Americano')
  console.log(coffeeList)
  await _addCoffee('Mocha')
  console.log(coffeeList)
  await _addCoffee('Latte')
  console.log(coffeeList)
}

coffeeMaker()
```

위 코드는 ES2017애서 추가 된 `async/await`를 이용한 코드입니다. 비동기 작업을 수행하고자 하는 함수 앞에 `async`를 표기하고, 함수 내부에서 실직적인 비동기 작업이 필요한 위치마다 `await`를 표기하는 것만으로 뒤의 내용을 `Promise`로 자동 전환하고 해당 내용이 `resolve`된 이후에야 다음으로 진행됩니다.

---
