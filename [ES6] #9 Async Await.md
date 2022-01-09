## Async / Await

### 1. Async Await

> async / await

- Promise를 사용하는 코드를 더 좋게 보이게 하는 문법
- Promise 밖에서 값을 가져올 수 있는 방법
- await
  - async function 안에서만 사용할 수 있다.
  - Promise가 resolve되든 reject되든 상관없이 끝나길 기다린다.



> 이전 Promise와 비교

```javascript
const getMoviesPromise = () => {
  fetch("https://yts.mx/api/v2/list_movies.json")
    .then((response) => {
      console.log(response);
      return response.json();
    })
    .then((potato) => console.log(potato))
    .catch((e) => console.log(`✔${e}`));
};

const getMoviesAsync = async () => {
  const response = await fetch("https://yts.mx/api/v2/list_movies.json");
  console.log(response); //resolve value
  const json = await response.json();
  console.log(json);
};

getMoviesAsync();
```

=> async / await 가 더 깔끔



### 2. try catch finally

> try catch finally

- catch
  - try 안에서 일어나는 모든 error를 잡아낸다
- finally
  - 무조건 실행



```javascript
const getMoviesAsync = async () => {
  try {
    const response = await fetch("일부러 오류내는 URL");
    const json = await response.json();
    console.log(json);
  } catch (e) {
    console.log("❌", e);
  } finally {
    console.log("we are done");
  }
};

getMoviesAsync();
```

=> ![image-20220109195720708](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220109195720708.png)



### 3. Parallel Async Await

> Async Await with Promise.all

```javascript
const getMoviesAsync = async () => {
try {
const [moviesResponse, upcomingResponse] = await Promise.all([
fetch("https://yts.mx/api/v2/list_movies.json"),
fetch("https://yts.mx/api/v2/movie_suggestions.json?movie_id=100"),
]);

const [movies, upcoming] = await Promise.all([
moviesResponse.json(),
upcomingResponse.json(),
]);

console.log(movies, upcoming);
} catch (e) {
console.log(e);
} finally {
console.log("we are done");
}
};

getMoviesAsync();
```

