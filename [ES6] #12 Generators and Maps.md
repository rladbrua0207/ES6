## #12 Generators and Proxies

별로 안중요해서 니콜라스가 신경을 많이 쓰지 않은 챕터

### 1. Generators

> Generator

- 기본적으로 pause할 수 있는 함수

- 몇 가지 규칙을 따라야 한다.
  
  - function* : function에 *을 넣으면, 한 단어를 해제하게 된다.
  - yield: return과 같다
  
- generator function 호출
  - ```javascript
    function* listPeople() {
      yield "Dal";
      yield "Flynn";
      yield "Mark";
      yield "Godkimchi";
      yield "Japan Guy";
    }
    
    const listG = listPeople();
    ```

![image-20220118212903126](https://raw.githubusercontent.com/rladbrua0207/image_repo/main/img/image-20220118212903126.png)

=> done: generator가 끝나지 않았음을 의미

- usecase가 많지않다



### 2. Proxies

> proxy

- object 앞에 있는 filter
- parameter
  - filter를 하고 싶은 object
  - object handler: trap들을 가지고있는 프로퍼티들이 함수인 객체
- 프록시로 생성된 객체를 통해 오브젝트의 프로퍼티에 접근할 수 있다
- trap: 프로퍼티에 접근할 수 있는 메소드. 운영체제에서 trap 이라는 컨셉과 유사
  - get: 프로퍼티에 접근할 때 호출
    - argument
      1. target: 실제 object를 가리킨다
      2. prop: user가 요청한 property data를 logging
      3. receiver: 요청된 object의 prop을 가진 proxy object 
  - set: 새로운 프로퍼티를 생성할 때 호출



### 3. Should you learn proxies or generators

proxy를 배워야 할까 Generator를 배워야 할까?

- 라이브러리에 관여하는 프로그래머가 아닌 이상 별 사용성이 없을거다.

- 라이브러리 에서의 사용성
  - ex) react라이브러리를 만드는 누군가는 react 내에 있는 object의 property를 누가 삭제하기를 원하지 않는다. 그들은 아마도 react를 proxy로 export할거다 내가 아무리 Object로 부터 뭔가를 삭제하려고 노력해도, 할 수 없도록 만든다.
- proxy
  - 프로그램-사용자/유저 간에서는 적용이 되지 않는다, 프로그래머 와 프로그래머의 관계에서만 그 프로그래머가 코드를 망치는걸 원하지 않을때 사용할 만한 거다 그 외에는 별 사용성이 없다고한다.
- generator도 똑같이 라이브러리에서 사용되므로 proxy와 비슷하다
