#### 1.var

var 절대사용 X, let 사용

default로 const사용, 덮어씌워지는 수에 let 사용

var는 hoisting이슈, block scope 없음 function scope는 있음



#### 2.Arrow Function 

```javascript
//이전방식:
//ex) 
const names = ["nico", "lynn", "flynn"];
function addHeart(item) {
	return item + " * "
}
const hearts = names.map(addHeart);
//callback 함수를 각각의 요소에 대해 한번씩 
//순서대로 불러 그 함수의 반환값으로 새로운 배열 생성
console.log(hearts);

=>["nico *", "lynn *, "flynn *"]
   
//요즘방식(Arrow Fucntion):
//ex) 
const names = ["nico", "lynn", "flynn"];
const hearts = names.map(item => item + " *"); //implicit return
//argument가 없거나 두 개 이상 있을경우 ( )괄호
console.log(hearts);

=>["nico *", "lynn *, "flynn *"]

/**implicit return : 같은 줄에 뭘 적던지 간에 return
괄호{}를 추가하게 되면 implicit return 사라짐(return 필요)=> 함수가 복잡 해 질때
this를 사용할 땐 arrow function 사용 X 
javascript에서 arrow funtion에서의 this 는 window 참조 
object를 return할땐 소괄호 안에 중괄호 ({})=> object를 return 하겠다 밑에 예시**/
```



#### 3.array.prototype.find()

제공되는 테스트 조건을 만족하는 첫번째 엘리먼트 값 리턴

```javascript
//@gmail.com이 들어간 첫번째 문자열 
//ex)
const email = [
    "nco@no.com",
    "naver@google.com",
    "lynn@gmail.com",
    "nico@nomad.com"
];
const foundMail = email.find(item => item.includes("@gmail.com"));//
//include는 boolean
console.log(foundMail);

=> "lynn@gmail.com"
```



#### 4.array.prototype.filter()

제공된 함수의 조건을 만족한 모든 엘리먼트로 새로운 array 생성

```javascript
//@gmail.com 제외 
//ex)
const email = [
    "nco@no.com",
    "naver@google.com",
    "lynn@gmail.com",
    "nico@nomad.com",
    "nico@gmail.com"
];
const noGmail = emails.filter(email => !email.includes("@gmail.com"));
console.log(noGmail);

=> ["nco@no.com", "naver@google.com", "nnico@nomad.com"]
```



#### 5.array.prototype.forEach(), array.prototype.map()

forEach(): 각 array의 엘리먼트 마다 제공된 함수 실행

map(): callback 함수를 각각의 요소에 대해 한번씩 순서대로 불러 그 함수의 반환값으로 새로운 배열 생성

```javascript
//@이전 내용만, 
//forEach() ex)
const email = [
    "nco@no.com",
    "naver@google.com",
    "lynn@gmail.com",
    "nico@nomad.com",
    "nico@gmail.com"
];
const cleaned = [];
emails.forEach(email => {
   cleaned.push(email.split("@")[0]); 
});

=> ["nco", "naver", "lynn", "nico", "nico"]

//map() ex)
const email = [
    "nco@no.com",
    "naver@google.com",
    "lynn@gmail.com",
    "nico@nomad.com",
    "nico@gmail.com"
];

const cleaned = emails.map(email => email.split("@")[0]);

=> => ["nco", "naver", "lynn", "nico", "nico"]
```



#### 6.object return

object를 return 할 땐  소괄호() 안에 중괄호{}  ({})=> objcet를 return하겠다 라는 말 함축

```javascript
//object return ex)
const email = [
    "nco@no.com",
    "naver@google.com",
    "lynn@gmail.com",
    "nico@nomad.com",
    "nico@gmail.com"
];

const cleaned = emails.map((email, index) => ({
    username = email.split("@")[0], 
    index;
}));
console.log(cleaned);

=>
0: {username: "nco", index 0}
1: {username: "naver", index 1}
2: {username: "lynn", index 2}
3: {username: "nico", index 3}
4: {username: "nico", index 4}
```

