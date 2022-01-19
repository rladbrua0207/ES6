### 1. Array.of()

어레이 만들어줌, 보통 element가 많을 때 사용

```javascript
const friends = Array.of("nico", "lynn", "dal", "mark");
```



### 2. Array.from()

array-like object로 부터 array만드는 메소드

ex) HTMLCollection

```javascript
const buttons = document.getElementByClassName("button");
buttons.forEach(button => {
	button.addEventListener("click",() => console.log("true"))
});
//=> Error, buttons.forEach is not a function(buttons은 Array가 아니라서)

const buttons = document.getElementByClassName("button");
Array.from(buttons).forEach(button => {
	button.addEventListener("click",() => console.log("true"))
});
//=> true
```



### 3. Array.prototype.find()

주어진 판별 함수를 만족하는 첫 번째 요소의 값을 반환

```javascript
const friends = [
"nico@gmail.com",
"lynn@naver.com",
"dal@yahoo.com",
"mark@hotmail.com",
"flynn@korea.com"
];
const target = friends.find(friend => friend.includes("korea"));
console.log(target);
//=> "flynn@korea.com"
```



### 4. Array.prototype.findIndex()

주어진 판별함수를 만족하는 배열의 첫 번째 요소에 대한 인덱스 반환 만족하는 요소 없으면 -1 반환

```javascript
const friends = [
"nico@gmail.com",
"lynn@naver.com",
"dal@yahoo.com",
"mark@hotmail.com",
"flynn@korea.com"
];
const target = friends.findIndex(friend => friend.includes("korea"));
console.log(target);
//=> 4
```



### 5. Array.prototype.includes()

배열이 특정 요소를 포함하고 있는지 판별

String.prototype.includes()랑 혼동 X 

```javascript
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true

console.log(pets.includes('at'));//String.prototype.includes는 true반환
// expected output: false
```

