## Rest and Spread

### 1. Introduction to Spread

> spread

- 변수, 오브젝트 를 가져와서 풀어해치고 전개하는것

```javascript
const friends = [1, 2, 3, 4];
const family = ["a", "b", "c"];

console.log([friends, family]);//#1
console.log(friends + family);//#2
console.log([...friends, ...family]);//#3

const sexy = {
	name: "nico",
	age: 24
};
const hello = {
	sexy: true,
	hello: "hello"
}

console.log({...sexy, ...hello});//#4
console.log({sexy, hello});//#5
```

=> 

#1 ![image-20211227163518086](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227163518086.png)

#2 ![image-20211227163741059](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227163741059.png)

#3 ![image-20211227163026620](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227163026620.png)

#4 ![image-20211227163244034](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227163244034.png)

#5 ![image-20211227163355480](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227163355480.png)



### 2. Spread Applications

> spread

- 뭔가를 추가하거나, 합치거나, 업데이트 하는 방법

```javascript
const friends = ["nico", "lynn"];

const newFriends = [ "dal", ...friends,];

console.log(newFriends);//#1

const nico = {
username: "nico",
};

console.log({ ...nico, password: 123 });//#2

const first = ["mon", "tue", "wed"];

const weekend = ["sat", "sun"];

const fullweek = [...first, "thu", "fri", ...weekend];

console.log(fullweek);//#3

const lastName = prompt("Last name : ");
const user = {
username: "nico",
age: 24,
// lastName: lastName !== "" ? lastName : undefined,
...(lastName !== "" && { lastName }),
};

console.log(user);//#4
```

=>

#1 ![image-20211227164653443](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227164653443.png)

#2  ![image-20211227170305667](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227170305667.png)

#3 ![image-20211227165108356](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227165108356.png)

#4  (이 경우 spread로 전개하려면 데이터가 object이어야함, 중괄호로 감사줌)

- 입력값이 없을때 ![image-20211227165759123](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227165759123.png)
  - =>입력값이 없을때 빈 문자열이라면  object에 lastName이 없게

- 입력값 있을때 ![image-20211227170019364](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227170019364.png)

  

### 3. Intro to Rest Parameters

> spread

- 변수를 전개시킨다.

> rest

- 모든 값을 하나의 변수로 축소시킨다.
- 끝도없는 parameter를 전달받는 함수를 만들 수 있다.
- array를 만든다
- parameter에 들어가면 rest 나머지는 spread

```javascript
const infiniteArgs = (...kimchi) => console.log(kimchi); //#1

infiniteArgs("1", 2, true, "lalala");

const bestFriendMaker = (firstone, ...rest) =>{
    console.log(`mybestfriend is ${firstone}`); 
    console.log(rest);
}//#2

bestFriendMaker("nico", "lynn", "dall", "jspan guy");
```

=>

#1 ![image-20211227172306006](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227172306006.png)

#2 ![image-20211227173012557](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227173012557.png)

### 4. Rest + Spread + Destructure Magic

> rest, spread, destructure 모두 다 활용한 예제

```javascript
const user = {
name: "nico",
age: 24,
password: 12345,
};

user["password"] = null;

console.log(user); //#1

user["password"] = 12345;

const killPassword = ({ password, ...rest }) => rest;
//rest return

const cleanuser = killPassword(user);

console.log(cleanuser); //#2

const setCountry = ({ country = "KR", ...rest }) => ({ country, ...rest });
//set default

console.log(setCountry(user)); //#3

const rename = ({ name: newname, ...rest }) => ({ newname, ...rest });

console.log(rename(user)); //#4
```

=>

#1 ![image-20211227185204263](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227185204263.png)

#2 ![image-20211227185409194](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227185409194.png)

#3 ![image-20211227185811784](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227185811784.png)

#4 ![image-20211227190522966](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227190522966.png)



