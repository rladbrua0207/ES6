## #10 Classes

코드를 보고 이해하자

### 1. Introduction to Classes

> Class

- object의 공장, blueprint(청사진)이다
- instance
  - 살아있는 클래스

```javascript
class User {
  constructor() {
    this.username = "Nicolas";
  }
  sayHello() {
    console.log("Hello");
  }
}

//instance
const sexyUser = new User();
const uglyUser = new User();

sexyUser.sayHello();
uglyUser.sayHello();

const baseObject = {
  username: "nicolas",
  sayHi: function () {
    console.log("hi nicolas");
  },
};

const sexyBase = baseObject;
const uglyBase = baseObject;

sexyBase.sayHi();
uglyBase.sayHi();

class SayName {
  constructor(name) {
    this.name = name;
  }
  SayNamefunc() {
    console.log(`My name is ${this.name}`);
  }
}

const callFunc = new SayName("Joey");
callFunc.SayNamefunc();
```



### 2. Extending Classes

> this

- 클래스 안에서 볼 수 있고, 클래스 자체를 가리킨다.
- 클래스로부터 어떤것을 불러오고 싶을때 사용

```javascript
class User {
  constructor(name, lastname, email, password) {
    this.username = name;
    this.lastname = lastname;
    this.email = email;
    this.password = password;
  }
  sayHello() {
    console.log(`Hello, my name is ${this.username}`);
  }
  getProfile() {
    console.log(`${this.username} ${this.email} ${this.password}`);
  }
  updatepassword(newpassword, currentpassword) {
    if (currentpassword === this.password) {
      this.password = newpassword;
    } else {
      console.log("can't change password");
    }
  }
}
class Admin extends User {
  // constructor(superadmin) {
  // this.superadmin = superadmin;
  // } =>constructor를 정의해주므로 User의 constructor을 잃어버림
  deleteWebsite() {
    console.log("Boom!");
  }
}

const sexyUser = new User("Nico", "serrano", "nico@com", "1234");

console.log(sexyUser.password);
sexyUser.updatepassword("new password", "123a4");
console.log(sexyUser.password);
const sexyAdmin = new Admin("Nico", "serrano", "nico@com", "1234");
sexyAdmin.deleteWebsite();
console.log(sexyAdmin.email);
```

=> ![image-20220109212333651](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220109212333651.png)



### 3. super

> super

- constructure의 원시 클래스 호출

```javascript
class User {
  constructor({ username, lastname, email, password }) {
    this.username = username;
    this.lastname = lastname;
    this.email = email;
    this.password = password;
  }

  getProfile() {
    console.log(`${this.username} ${this.email} ${this.password}`);
  }
  updatepassword(newpassword, currentpassword) {
    if (currentpassword === this.password) {
      this.password = newpassword;
    } else {
      console.log("can't change password");
    }
  }
}
const sexyUser = new User({
  username: "Nico",
  lastname: "serrano",
  email: "nico@com",
  password: "1234",
});

class Admin extends User {
  constructor({ username, lastname, email, password, superadmin, isActive }) {
    super({ username, lastname, email, password });
    this.superadmin = superadmin;
    this.isActive = isActive;
  }
  deleteWebsite() {
    console.log("Boom!");
  }
}

const admin = new Admin({
  username: "Nico",
  lastname: "serrano",
  email: "nico@com",
  password: "123456",
  superadmin: true,
  isActive: true,
});

//super 덕분에 admin으로 getProfile 접근 가능
admin.getProfile();
```

=> ![image-20220109222618139](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220109222618139.png)



```html
//index.html
<body>
    <span id="count">0</span>
    <button id="add">+</button>
    <button id="minus">-</button>
    <script src="index.js"></script>
</body>
```

```javascript
//index.js
class Counter {
  constructor({ initialNumber = 0, counterId, plusId, minusId }) {
    this.count = initialNumber;
    this.counter = document.getElementById(counterId);
    this.plusBtn = document.getElementById(plusId);
    this.minusBtn = document.getElementById(minusId);
    this.addEventListeners();
  }
  addEventListeners() {
    this.plusBtn.addEventListener("click", this.increase);
    this.minusBtn.addEventListener("click", this.decrease);
  }
  increase() {
    this.count = this.count + 1;
    this.repaintCount();
  }
  decrease() {
    this.count = this.count - 1;
    this.repaintCount();
  }
  repaintCount() {
    this.counter.innerText = this.count;
  }
}

new Counter({ counterId: "count", plusId: "add", minusId: "minus" });

```

=> 오류, 다음시간에 해결 

![image-20220109223459513](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220109223459513.png)



### 4. WTF is this

> this

- addEventListener에서 그 이벤트를 호출하면 자바스크립트는 this를event target을 가르키도록 변경한다.
- 이를 방지하려면 arrow function을 사용

```javascript
class Counter {
  constructor({ initialNumber = 0, counterId, plusId, minusId }) {
    this.count = initialNumber;
    this.counter = document.getElementById(counterId);
    this.plusBtn = document.getElementById(plusId);
    this.minusBtn = document.getElementById(minusId);
    this.addEventListeners();
  }
  addEventListeners = () => {
    this.plusBtn.addEventListener("click", this.increase);
    this.minusBtn.addEventListener("click", this.decrease);
  };
  increase = () => {
    this.count = this.count + 1;
    this.repaintCount();
  };
  decrease = () => {
    this.count = this.count - 1;
    this.repaintCount();
  };
  repaintCount = () => {
    this.counter.innerText = this.count;
  };
}

new Counter({ counterId: "count", plusId: "add", minusId: "minus" });
```

=> 

![image-20220109224721911](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220109224721911.png)

