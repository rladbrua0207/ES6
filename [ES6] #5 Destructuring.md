### 1. Object Destructuring

큰 오브젝트에서 특정 변수나 그 안에 속한 작은 오브젝트에 접근할 수 있도록

```javascript
const settings = {
	notifications: {
		follow: true,
		alerts: true,
		unfollow: false
	},
	color: {
		theme: "dark"
	}
};
const {// 이 자체가 const 변수
	notifications: {follow = false},// follow가 있는지 찾아본 후 없다면 false
//const { notifications: {follow = false} = {} } = settings;
//const { color: {theme} } = settings;
//one-line-statement, if notifications가 존재하면 ...
	color
} = settings;
console.log(follow);
console.log(color);
// => true
// => {theme: "dark"}
```



### 2. Array Destructuring

가져온 정보를 조작 하지 않을 때 쓰기 좋다

ex) API로부터 응답받응 데이터를 array형태로 만들어야 하는 상황

```javascript
const days = ["Mon", "Tue", "Wed"];
const [mon, tue, wed, thu = "Thu" ] = days;
console.log(mon, tue, wed, thu);
//=> mon Tue Wed Thu

//함수로 사용
const days = () => ["Mon", "Tue", "Wed"];
const [mon, tue, wed, thu = "Thu" ] = days();
console.log(mon, tue, wed, thu);
//=> mon Tue Wed Thu
```



### 3. Renaming

Destructuring 코드들 이름바꾸기

```javascript
const settings = {
	color: {
		chosen_color: "dark"
	}
};
const {
	color: { chosen_color: chosenColor = "light"} //변수이름 바꾸기
} = settings;
console.log(chosenColor);

//이미 변수가 선언돼 있을 때
const settings = {
	color: {
		chosen_color: "dark"
	}
};
let chosenColor = "blue"
console.log(chosenColor);
({
	color: { chosen_color: chosenColor = "light"} //이미 있는 let 변수 찾아서 업데이트
} = settings);
console.log(chosenColor);
//=>blue, dark
```



### 4. function Destructuring

```javascript
function saveSettings(settings) {
    console.log(settings);
}

saveSettings({
    followAlert: true,
    unfollowAlert: true,
    mrkAlert: true,
    themeColor: "green",
});

function saveSettings2({ color: { theme } }) {
    console.log(theme);
}

saveSettings2({
    notifications: {
        follow: true,
        alert: true,
        mkt: false,
    },
    color: {
        theme: "blue",
    },
});
```

=> ![image-20220119002217973](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220119002217973.png)



### 5. Value Shourthands

```javascript
//변수 이름을 다르게 할 때
const isFollowing = checkIsFollowing();
const isAlertOn = checkIsAlertOn();

const settings = {
  notifications: {
    follow: isFollowing, 
    isAlertOn: isAlertOn, 
  },
};

//변수 이름을 같게해도 될 때
const isFollowing = checkIsFollowing();
const isAlertOn = checkIsAlertOn();

const settings = {
  notifications: {
    isFollowing, 
    isAlertOn,
  },
};
```



### 6. Swapping and Skipping

```javascript
let mon = "Sat";
let sat = "Mon";

[sat, mon] = [mon, sat];

console.log(mon, sat);
//=> Mon Sat

const days = ["mon", "tue", "wed", "thu", "fri"];
const [, , , thu, fri] = days;

console.log(thu, fri);
//=> thu fri
```
