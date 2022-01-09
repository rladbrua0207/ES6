### #8.0 Introduction to Async

강의목표

1. 자바스크립트의 비동기성과 동기성 알기

```javascript
const hello = fetch("http://google.com");

console.log("something");
console.log(hello);
```

=> ![image-20220103181000158](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103181000158.png)

>  이론적으로는

1. google.com을 fetch하고 바로 에러가 나오고,
2. something을 출력하고,
3. 아무것도 출력하지 않아야한다.

> 위에서는

1. something이 출력되고
2. 에러가 출력됐다

=> 자바스크립트의 비동기성(async)

- 자바스크립트는 프로그램의 실행을 멈추지 않는다.
- 순차적으로 처리되는 게 아니라 한꺼번에 실행.
- fetch를 실행하자 마자 한쪽에서 어떤 action을 시작 => something을 출력하고 fetch쪽에서 에러가생기고 다시 돌아와 에러가 있다고 말하는것.



### #8.1 Creating Promises

> Promise

- 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다.
- Promise를 만들 때는 실행할 수 있는 function을 넣어야한다.
- Promise를 호출할 때, 자바스크립트는 설정한 다른 function과 함께 이 Promise를 실행한다.
- Promise의 핵심은, 아직 모르는 value와 함께 작업할 수 있게 해준다.
- resolve
  - 야, 이게 네 값이야. 자바스크립트로 돌아가.
- reject
  - 야, 미안한데 에러가 있어.

```javascript
const amISexy = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Yes you are!");
  }, 3000);
});
//== setTimeout(resolve, 3000, "Yes you are");

console.log(amISexy);

setInterval(() => {
  console.log(amISexy);
}, 1000);
```

=> 3초가 지났을 때 부터 pending => resolve로 바뀜

![image-20220103190246762](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103190246762.png)



### #8.2 Using Promises

> then

- Promise가 끝났을 때 값을 돌려달라고 명령을 내리는거.
- 어떤 값을 resolve로 입력해주던 입력 한 값이 then의 value로 들어온다.

> reject

- 거부된 Promise를 반환

```javascript
const amISexy = new Promise((resolve, reject) => {
  setTimeout(reject, 3000, "you are ugly");
});

amISexy.then((value) => console.log(value));
```

=> ![image-20220103191958315](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103191958315.png)

> catch

- then이랑 비슷하지만 에러를 위해 쓰인다.
- Promise가 reject 되면 실행.
- catch가 실행되면 then은 절대 실행되지 않는다. 반대도 똑같다.



### #8.3 Chaining Promises

> Chaining

- then은 넣고 싶은 만큼 넣어서 chaining을 해주면 되는거다.
- 단, promise들을 엮고 싶을 때는 기존의 then에서 return값이 있어야 한다.

```javascript
const amIsexy = new Promise((resolve, reject) => {
  resolve(2);
});

amIsexy
  .then((number) => {
    console.log(number * 2);
    return number * 2;
  })
  .then((othernumber) => {
    console.log(othernumber * 2);
  });
```

=> ![image-20220103193222390](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103193222390.png)

```javascript
const amIdouble = new Promise((resolve, reject) => {
  resolve(2);
});

const timesTwo = (numbertwo) => numbertwo * 2;

amIdouble
  .then(timesTwo)
  .then(timesTwo)
  .then(timesTwo)
  .then(timesTwo)
  .then(() => {
    throw Error("something is wrong");
  })
  .then((lastNumber) => console.log(lastNumber))
  .catch((error) => console.log(error));
```

=> catch가 다른 모든 then이랑 function 안의 에러들을 모두 잡아준다. 

 ![image-20220103193738791](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103193738791.png)



### #8.4 Promise.all

> Promise.all

- 주어진 모든 Promise를 실행한 후 진행되는 하나의 Promise를 반환
- ex) 여러개의 API를 받아와야하는데 여러개 API에 다 then을 넣어주는거 보다는 Promise.all을 통해 하나의 리턴값만 받는거
- 모든 Promise가 전부 Resolve 되고 나면 마지막 Promise를 리턴값으로 주는거
- 시간이 얼마나 걸리던 전부 끝났을 때 값을 순서대로 제공
- Promise.all에 제공한 Promise가 하나라도 reject면 motherPromise도 reject 된다

- ```javascript
  const p1 = new Promise((resolve) => {
    setTimeout(resolve, 3000, "First");
  });
  
  const p2 = new Promise((resolve, reject) => {
    setTimeout(resolve, 2000, "second");
  });
  
  const p3 = new Promise((resolve) => {
    setTimeout(resolve, 1000, "third");
  });
  
  const motherPromise = Promise.all([p1, p2, p3]);
  
  motherPromise
    .then((value) => console.log(value))
    .catch((err) => console.log(err));
  ```

=> ![image-20220103194643163](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103194643163.png) p2가 reject일때 ![image-20220103194731067](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103194731067.png)



### #8.5 Promise.race

> Promise Race

- 말 그대로 race
- PromiseAll과는 다르지만 사용법은 같다.
- Promise.race에 제공한 Promise가 하나라도 resolve 되거나 reject되면 된다. (가장 빠른게 결과를 정한다)



### #8.6 .finally

> finally

- Promise가 성공하든 실패하든 실행된다.
- 보통 API를 호출할 떄 사용.

```javascript
const p1 = new Promise((resolve, reject) => {
setTimeout(reject, 1000, "First");
})
.then((value) => console.log(value))
.catch((e) => console.log(`${e}error`))
.finally(() => console.log("Im done"));
```



### #8.7 Real world Promises

강의목표

1. 니꼬가 사용하는 Promise 구경

```javascript
fetch("https://yts.mx/api/v2/list_movies.json")
  .then((response) => {
    console.log(response);
    return response.json();
  })
  .then((potato) => console.log(potato))
  .catch((e) => console.log(`✔${e}`));
```

=> Response

![image-20220103201458990](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103201458990.png)

response.json() (body에 있는 ReadableStream을 읽어준다)

![image-20220103201552872](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220103201552872.png)