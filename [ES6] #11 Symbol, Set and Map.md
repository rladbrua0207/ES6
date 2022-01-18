## #11 Symbol, Set and Map

### 1. Symbols

> Symbol

- 매우 고유한 data type
- 일반적은 app에서는 사용하지 않을거같고 보통 라이브러리 제작자들이 사용하는거 같다.

```tsx
const hello = Symbol("hello");
const bye = Symbol("hello");
```

![image-20220118124219200](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220118124219200.png)

예제

```javascript
const symbol1 = Symbol();
const symbol2 = Symbol(42);
const symbol3 = Symbol('foo');

console.log(typeof symbol1);
// expected output: "symbol"

console.log(symbol2 === 42);
// expected output: false

console.log(symbol3.toString());
// expected output: "Symbol(foo)"

console.log(Symbol('foo') === Symbol('foo'));
// expected output: false
```

별로 중요하게 안다룸 니꼬도 잘 모른다고했다



### 2. Sets

> Sets

- 어떤 타입의 고유한 value든 저장할 수 있게 해준다.
- unique한 value를 저장하는 것이다.
- `new Set(iterable)` – 셋을 만든다. 
  - `이터러블` 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어준다.
- `set.add(value)` – 값을 추가하고 셋 자신을 반환한다.
- `set.delete(value)` – 값을 제거한다
  -  호출 시점에 셋 내에 값이 있어서 제거에 성공하면 `true`, 아니면 `false`를 반환한다.
- `set.has(value)` – 셋 내에 값이 존재하면 `true`, 아니면 `false`를 반환한다.
- `set.clear()` – 셋을 비운다.
- `set.size` – 셋의 사이즈를 반환한다.
- 

### 3. WeakSet

> WeakSet

- set과의 차이점

  - object만 저장 할 수 있다.

  - 사용할 수 있는 메서드가 4개밖에 없다

    ![image-20220118133922729](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220118133922729.png)

- WeakSet에 집어넣는 모든 것들은 약하게 붙들려 있다

  - weak set에 넣은 objects를 가르키는 것이 없다면 지워진다.
  - ex) WeakSet.add({hello:true}); 후 아무에 아무런 참조를 안한다면 garbagecollector가 오면(메모리가 부족할 때) 이걸 가져간다

- 대부분 사용 안한다.



### 4. Map 

> Map

- set과 비슷하지만 key-value를 사용할 수 있게 해준다

- `new Map()` – 맵 생성.
- `map.set(key, value)` – `key`를 이용해 `value`를 저장한다.
- `map.get(key)` – `key`에 해당하는 값을 반환합니다. `key`가 존재하지 않으면 `undefined`를 반환한다.
- `map.has(key)` – `key`가 존재하면 `true`, 존재하지 않으면 `false`를 반환한다.
- `map.delete(key)` – `key`에 해당하는 값을 삭제한다.
- `map.clear()` – 맵 안의 모든 요소를 제거한다.
- `map.size` – 요소의 개수를 반환한다.