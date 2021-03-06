### 1. String 안에 표현식

``로 문자열 안에 변수 쉽게표현 가능하고 줄바꿈도 가능함

```javascript
const sayHi1 = (aName = "anon") => "hello " + aName + "lovely to have You";
console.log(sayHi1());

const sayHi2 = (aName = "anon") => `hello ${aName} lovely to have you`;
console.log(sayHi2());
```



### 2. HTML Fragments

```javascript
//줄바꿈 가능 
//ex)
const wrapper = document.querySelector(".wrapper");

const addWelcome = () => {
    const div = `
<div class = "hello">
	<h1 class = "title">Hello</h1>
</div>`;
    wrapper.innerHTML = div;
}
addWelcome();

//목록 만들기
const wrapper = document.querySelector(".wrapper");
const friends = ["me", "lynn", "dal", "mark"];
const ul = document.createElement("ul");
friends.forEach(friend => ul.append(`<li>${friend}</li>`))
wrapper.append(ul);
//=> 텍스트로 <li>me</li><li>lynn</li><li>dal</li><li>mark</li> 나옴

//HTML Fragment 활용
const wrapper = document.querySelector(".wrapper");
const friends = ["me", "lynn", "dal", "mark"];
const list = `
<h1>People i love</h1>
<ul>
	${friends.map(friend => `<li>${friend}</li>`).join(" ")}
</ul>`;
//join()메소드: 배열의 각 요소를 구분할 문자열 지정
//리스트의 , 를 지우려고 사용
wrapper.innerHTML = list;
//=> People i love
//	-me
//	-lynn
//	-dal
//	-mark
```



### 3. Styled Components

리액트를 위한 라이브러리

JS에서 CSS랑 HTML 활용하게 해줌

=> 리액트 배우고나서 보는데 이거 왜 여기서 다루는거지? 

```javascript
const styled = css => console.log(css);

//styled() 에서 괄호를 빼면 String인 argument가 나옴 괄호를 쳐도 상관은 없다고 함
//=>function을 호출하는 새로운 방법
styled`border-radius:10px;
color:blue`; 
//=> 0번째 인덱스: "border-radius:10px color:blue"

//활용
const styled = aElement => {
    const el = document.createElement(aElement);
    retrun args => {
        const styles = args[0]; //"border-radius:10px color:blue"
        el.style = styles;
        return el;
    };
};
const title = styled("h1")` //h1태그 생성
border-radius: 10px; color: blue;`;//두번째 함수(위의 args)
console.log(title);
//=> <h1 style="border-radius: 10px; color: blue;"></h1>

```



### 4. String.prototype.includes()

찾고싶은 문자가 있는지

```javascript
const isEmail = email => email.includes("@");
console.log(isEmail("nico@nomadcoders.co"));
//=>true
```



### 5. String.prototype.repeat()

어떤문자든 반복

```javascript
const CC_NUMBER = "6060";
const displayName = `${"*".repeat(10)}${CC_NUMBER}`
console.log(displayName);
```



### 6. String.prototype.startsWith(), endsWith()

문자열이 뭐로 시작하는지

```javascript
const name = "MR. Nicolas";
console.log(name.startsWith("MR"));
console.log(name.endsWith("Nicolas"));
//=> true, true
```
