## For of Loop

### 1. For ... of

> For ... of

- array에서만 동작하는 것이 아니라, iterable한 모든 것에서 동작한다.
  - String, Array, NodeLists, Typed Array, Map, Set 등 에서 사용가능
  - forEach는 array에서만 사용가능
- forEach와 다르게 중간에 루프를 멈출 수 있다.

```javascript
const friends = ["nico", "lynn", "ha", "hu"];

for (let i = 0; i < friends.length; i++) {
  console.log(`i love my friend ${friends[i]}`); //#1
}

const addHeart = (c, i, a) => console.log(c, i, a); //#2
//첫번째 인자 c: current item
//두번째 인자 i: index
//세번째 인자 a: current array

friends.forEach(addHeart);

friends.forEach((friend) => console.log(friend)); //#3

for (const friend of friends) {
  console.log(friend);//#4
}//forEach와는 다르게 let으로 선언할지 const로 선언할 지 선택가능


for (const letter of "Hello") {
  console.log(letter); //#5
}//for

for (const friendstop of friends) {
  if (friendstop === "ha") {
    break;
  } else {
    console.log(friendstop); //#6
  }
}
```

=>

#1![image-20211227191754022](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227191754022.png)

#2 ![image-20211227191736643](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227191736643.png)

#3, 4 ![image-20211227192000316](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227192000316.png)

#5 ![image-20211227192845550](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227192845550.png)

#6 ![image-20211227193423687](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20211227193423687.png)