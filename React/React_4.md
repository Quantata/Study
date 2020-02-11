# 2.4 향상된 비동기 프로그래밍 1: 프로미스
예전에는 콜백을 많이 썼는데 그거보다 좀 더 효율적인게 프로미스
## P74 프로미스(promise)
- pending : 요청하고 응답올때까지 기다리는 상태
- fulfill : 요청 성공
- reject : 요청 실패
- settled
	- fulfill(resolve) : then
		- 던저놓고 그거에 대한 처리
	- reject
		- then
			- 에러에 대한 처리
		- catch
- 그 이후 새로운 프로미스 생성해서 던저놓을 수 있다.(then 안에서)
**![](https://lh3.googleusercontent.com/iAVX7X1PvBevloLth4_YNwuIMGRVEgrkJM7McGmmog8O6MuGZAsuriJ-r95qvb_uM8f6zO9MStEOzciOxKEJ9KXKIZk1amFdjqZPL7mQy8OxS74RJnmxjLVTlQcfMcxGxcW_dyjX)**

### 프로미스 생성하는 방법
- new keyword 생성
```html
<script>
    const p1 = new Promise((resolve, reject) => {
        //  ...
        //  resove(data)
        //  or
        //  reject('error message')
    });
</script>
```

- new keyword 생성하지 않고 `Promise.reject` 또는 `Promise.resolve` 호출해서 거부됨 상태의 프로미스 생성
```html
<script>
   // new 키워드를 사용하지 않고, 
    //  Promise.reject를 호출하면 거부됨 상태의 프로미스가 생성
    const p2 = Promise.reject('error message');
 
    //  Promise.resolv를 호출해도 프로미스가 생성
    //  입력값이 프로미스이면 그 객체가 그대로 반환되고, 
    //  프로미스가 아니라면 이행됨 상태의 프로미스가 반환
    const p3 = Promise.resolve(param);
</script>
```
### fulfill 상태 Promise 리턴
```html
<script>
	//fulfill 상태의 promise 리턴
    const p1 = Promise.resolve(123);
    console.log(p1 === 123);    // false
    console.log(p1);            // Promise { <resolved>: 123 }

    const p2 = new Promise(
        resolve => { setTimeout(() => resolve('1초 경과'), 1000) },
        reject => { return "error"; }
        );    // setTimeout() 대표적인 비동기 함수
    // resolve 함수는 timeout을 수행
    // 뒤에 resolve는 resolve함수를 정의, 밑에 console에서 p2 넘겨주면 파라미터 (앞의 resolve) 가 setTimeout 수행
    console.log(p2 === Promise.resolve(p2));    // true //promise를 반환
    console.log(p2);              // Promise {<pending>}
    p2.then(data => { 
        console.log(p2);
        console.log(data);
        }
    );
</script>
```
**![](https://lh5.googleusercontent.com/6xoW08ua68eLBxDwcZkGREkLouz_X1ItW4zxPOue7VnVPdN7DIDxxrBNI8ncWVrhmRPYeE8smngzl1oWAbv1_NhuHaMf2J2wSITA7ZzwwW5FYaoHFFFRWd5a2lKqCcF_12nBsd-i)**

### reject 상태의 Promise 리턴
(question에 있음)
```html
<script>
    Promise.reject("error message")
    .then(() => console.log("#1"))
    .then(() => console.log("#2"))
    .then(
        () => console.log("#3-1"), 
        (data) => {
            console.log("#3-2", data);
            return "hello";
        }
    )
    .then((data) => console.log("#4-1", data), () => console.log("#4-2"));

    Promise.resolve("message")
    .then((data) => { console.log("#1", data); return "message2"; })
    .then((data) => console.log("#2", data))
    .then(
        () => console.log("#3-1"), 
        (data) => {
            console.log("#3-2", data);
            return "hello";
        }
    )
    .then((data) => console.log("#4-1", data), () => console.log("#4-2"));
</script>
```

### catch 문을 사용해야하는 이유
- error 처리하려고 하려면 then을 두번쓰는 방법 밖에 없는데 코드가 길어지고 가독성이 떨어지니 `catch` 구문을 씀
- Promise를 처리할때, 성공은 then으로 예외사항은 catch를 사용하는 것이 좋다.
```html
<script>
    //  예외 처리를 catch 구문을 이용해야는 이유 
    //  1. 가독성이 좋다
    Promise.reject("error1").then(null, data => console.log(data));
    Promise.reject("error2").catch(data => console.log(data));

    //  2. resolve 함수 내에서 발생하는 예외를 처리
    Promise.resolve("data")
        .then(
            (data) => { 
                console.log("#1", data);
                throw new Error("Error Occured");   // Uncaught (in promise) Error: Error Occured
            }, 
            (data) => { 
                console.log("#2", data);
            }
        );

        Promise.resolve("data")
        .then(
            (data) => { 
                console.log("#1", data);
                throw new Error("Error Occured");   
            }, 
            (data) => { 
                console.log("#2", data);
            }
        )
        .then(
            null, 
            (data) => {
                console.log("#3", data);
            }
        );

    console.log("--------------");
    Promise.resolve("data")
        .then(
            (data) => { 
                console.log("#1", data);
                throw new Error("Error Occured");   
            }
        )
        .catch(data => console.log("#4", data));

</script>
```

#### then과 catch 구문
- then과 catch는 계속 새로운 Promise를 만든다.
```html
<script>
    Promise.reject(10)
    .then(data => {
        console.log("then1", data);
        return 20;
    })
    .catch(data => {
        console.log("catch", data);     // catch, 10
        return 30;
    })
    .then(data => {
        console.log("then2", data);     // then2, 30
    });
</script>
```

#### finally 구문을 쓰면 Promise 생성 안함
p80
```html
<script>
    // p80 finally 메소드는 새로운 프로미스를 생성하지 않음
    function sendLogToServer(msg) {
        console.log("sendLogToServer", msg);
    }

    function requestData() {
        let url = "http://localhost:8080/es6.html";
        return fetch(url)   // url로 데이터를 가져옴
        // fetch가 url을 통해 갖고오고 promise return
        .then(resolve => {  // resolve에 url을 통해 가져온 정보들 들어가 있을 것
            console.log("#1", resolve);
            return resolve;
        })
        .catch(error => {
            console.log("#2", error)
        })
        .finally(() => {    // Promise 생성하지 않고 값 반환
            console.log("#3");
            sendLogToServer("requestData Finished");
        });
    }

    requestData().then(resolve => console.log("#4", resolve));
</script>
```
**![](https://lh6.googleusercontent.com/50OAXotpMHJc_1XpNRoM8YOWrXLAQFU1Bo3Ge-YGygHeLnPHlhqb54MwaVe0wTk31P8orsylR0MoR-0Uv3vSh-HCG1qTnyGEf8Sl3PC0HySC2_Ku0RYvl9kRNCMVf8hG8WieNBcO)**

### Promise.all
#### 의존 관계가 있는 업무는 순차적으로 비동기 처리
```html
<script>
	// 의존 관계가 있는 업무는 순차적으로 비동기 처리
	// RequestData1() 업무가 끝나야 requestData2() 업무를 처리할 수 있는 경우
	// 예) 데이터를 가져와야 데이터를 파싱할 수 있다.
    function requestData1() {
        return Promise.resolve("requestData1 called");
    }

    function requestData2() {
        return Promise.reject("reqeustData2 called");
    }

    requestData1()
    .then(data => {
        console.log("#1", data);
        return requestData2();
    })
    .then(data => {
        console.log("#2", data);

    }).catch(error => {
        console.log("ERROR", error);
    })
</script>
```
**![](https://lh6.googleusercontent.com/MINYAPxaDmjfYu_meMzyG8eiJHDtmW7cIAg4TxB249jDaUNjN8yYXA7LcPpFW1CfmaIckxsBkH1qjRupeRi9lVURsqqCVN0F_64Z4k0dNpxfkUKkgoA26Ew6xCV4j9gMNdd8cVh5)**
물건 검색 기능과 물건 배송 기능은 따로 만들어도 됨.
그럼 병렬로 처리하면 됨.
그래서 의존 관계없으면 위의 코드처럼 순차적으로 처리하면 안됨

#### 병렬로 처리
```html
<script>
    // 의존 관계가 없는 업무는 병렬로 처리
    function requestData1() {
        return Promise.resolve("requestData1 called");
    }

    function requestData2() {
        return Promise.reject("reqeustData2 called");
    }

    // 이렇게 하면 (거의) 동시에 두개가 실행
    requestData1().then(data => console.log("#1", data), error => console.log("#2", error));
    requestData2().then(data => console.log("#3", data), error => console.log("#4", error));
</script>
```

#### 병렬로 처리할게 많고 성공해야한다 하면은 promise.all
```html
<script>
    // 의존 관계가 없는 업무는 병렬로 처리
    function requestData1() {
        return Promise.resolve("requestData1 called");
    }

    function requestData2() {
        return Promise.reject("reqeustData2 called");
    }

    // 이렇게 하면 (거의) 동시에 두개가 실행
    requestData1().then(data => console.log("#1", data), error => console.log("#2", error));
    requestData2().then(data => console.log("#3", data), error => console.log("#4", error));

    // 업무를 던져 놓으면 결과가 날라옴.
    Promise.all([requestData1(), requestData2()]) // 이 전체가 성공하면 개별적으로 반환하는 놈들
    .then(([data1, data2]) => // data1, data2 는 서로 연관관계가 없음. 개별적으로 실행 // 안탐 왜? reject가 없어서
        console.log(data1, data2)
    )
    .then( // 실패한 케이스 여기로 옴
        () => console.log("모든 프로미스가 처리된 상태"),
        () => console.log("프로미스 중 하나 이상이 거부된 상태")
    );
</script>
```


> 책이 어려워서 이제 홈피이지를 통해 10단계 수련해보겠다.
## 리액트를 다루는 기술
저자가 운영하는 사이트
[https://velopert.com/3613](https://velopert.com/3613)

### create-react-app을 이용해서 프로젝트 생성
```
c:\react>create-react-app hello-react2
```
```
c:\react>cd hello-react2
```
```
c:\react\hello-react2>npm start
```
http://localhost:3000 ⇐ 브라우저를 통해서 확인

### **[`C:\react\hello-react2\src\App.js`]**
import는 다른 파일에서 모듈을 갖고 오는 것
`import React from 'react'` : react 파일에서 React라는 모듈 갖고옴. => React는 컴포넌트 일 것이야
import - 나중에 웹팩이 묶어줄때 해당하는 소스에 포함시켜줌. 캐싱관리도 해줌

#### 함수 형태로 컴포넌트 선언
```html
<script>
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
</script>
```
#### 클래스 형태로 컴포넌트 선언 -> render 함수를 포함
```html
<script>
import React from 'react';
import logo from './logo.svg';
import './App.css';

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}
</script>
```

 App 정의할때 함수형이나 class형으로 할 수 있음
**function(함수)형**는
사용자에게 보여주는 ui 화면만 return하는 경우 사용하면 단순하게 사용할 수 있다.
내가 화면도 보여주면서 화면에 출력해야하는 값을 유지하면서 값에 따라 화면 출력이 달라져야한다. 하면 **값(상태변수)을 가지고 있어야**함으로 **class 형으로 선언**

### JSX 사용
#### jsx에서는 열고 닫는 태그가 항상 **짝**을 이뤄야함
- `HTML` 에서는  닫는 태그가 존재하지 않는(필수가 아닌) 태그들이 존재
	```html
	<input type="text">
	<br>
	<hr>
	```

- `JSX`에서는 반드시 닫는 태그를 사용
	```html
	<input type="text" />
	<input type="text"></input>
	<br />
	<br></br>
	```
#### JSX에서는 반드시 하나의 태그(엘리먼트)로 감싸져 있어야 한다.
[잘못된 예]
```html
<div> ... </div>
<div> ... </div>
```
[올바른 예]
```html
<div>
	<div> ... </div>
	<div> ... </div>
</div>
```
#### 엘리먼트를 묶어줄 때 다른 태그(\<div>)를 사용하는 경우
묶어주는 용도로만 쓸때 이름을 빈 것으로 `<> ... </>` 넣어줘도 됨
[원래 코드]
```html
class App extends React.Component {
  render() {
    return (
      <div>
        <div>
          abc
        </div>
        <div>
          xyz
        </div>
      </div>
    );
  }
}
```
**![](https://lh6.googleusercontent.com/uZRVjqgGQPL8hM5IPwMOvkaw-EEx-MszuiqUXEfogioGazc1o4nBd4rd9kD5dAG9Q1M2Q-beJzqO0JSC9dCW6GM5-dytWh0g1pb7aYaPll9K4xuLM8zpYdhdpNmz-GUUyU74-jXQ)**

2개의 \<div> 엘리먼트를 묶어주는 역할의 \<div>가 생성 → 불필요한 DOM 객체가 사용(생성)

#### `<> .. .</>` 를 사용해서 엘리먼트를 묶을 수 있음
```html
class App extends React.Component {
  render() {
    return (
      <>
        <div>
          abc
        </div>
        <div>
          xyz
        </div>
      </>
    );
  }
}
```

![](https://lh5.googleusercontent.com/iDrwERaH_S85WHtSL39Zs1oDfDmskIc5KA-kocJptWE-wbV6Giw-ZXKDgR4G-eR8sjHZs_F-a-Q4hlJovplL4u4V-hlUgfFLD2tg8SlryZu28M_7BN2Cd52m6B_k5qrhc2gCNhVk)

불필요한 DOM 요소가 생성되지 않았음

#### <Fragment> 사용
```jsx
class App extends React.Component {
  render() {
    return (
      <Fragment>    {/* 또는 <>  */}
        <div>
            abc
        </div>
        <div>
            xyz 
        </div>     {/* 또는 </>  */}
      </Fragment>
    );
  }
}
```

#### JSX 에서 자바스크립트 사용할때 값 사용
render함수 안에 변수 지정
```js
import React from 'react';
import logo from './logo.svg';
import './App.css';

class App extends React.Component {
  render() {
      const name = 'react'
    return (
      <div> Hello {name}! </div>
    );
  }
}

export default App;
```

#### 연산식이 들어올 수도 있음
```js
class App extends React.Component {
  render() {
    const name = '리액트';
    return (
      <div>
        {
          name === 'react' ? 'Hello react' : '안녕 리액트'
        }          
      </div>
    );
  }
}

export  default  App;
```

#### 함수가 들어갈 수도 있음
```js
class App extends React.Component {
  render() {
    const value = 1;
    return (
      <div>
        {
          (function() {
            if (value == 1) return <div>하나</div>;
            if (value == 2) return <div>둘</div>;
          })()
        }          
      </div>
    );
  }
}
export  default  App;
```
 
 #### jsx 이용해서 style 적용하기 
jsx에서 정의한 변수의 값을 넘김(밑의 style에)
 **![](https://lh3.googleusercontent.com/f-3vS5mgGg7bEpowt75y_7opRNh7k70ak1RFS3fDjKHYkIip7g_8CC9Jcg2Wh-erurR9p9iZMlEy-vyzwLTJqZh9xGREZfQ76MOr0nupN-YQYYBoFhtTKTMWpGrj_65LbIVxZwry)**
```js
import React from 'react';
//import logo from './logo.svg';
//import './App.css';

class App extends React.Component {
  render() {
    let styles = {  //객체
      backgroundColor: 'black', 
      padding: '16px',
      color: 'white', 
      fontSize: '12px'
    };
    return (
      <div style={styles}>
        안녕하세요.
      </div>
    );
  }
}

export default App;
```
### jsx로 `App.css`를 이용해서 style 적용

클래스를 넣어줄때 `jsx` 이용할때는 `className`을 사용해야함.
rendering된 결과(내가 render라는 함수를 통해 return되는 값(JSX구문)이 다 해석되어서 나오는 최종 산출물)가 브라우저의 Elements에 보임.
이런 형태로 나타낸 것을 화면에 보여줌.

**[`C:\react\hello-react2\src\App.css`]**
```css
/* class 이름이 App 인 것 */
.App {  
  background: black;
  color: aqua;
  font-size: 20px;
  padding: 1rem;
  text-align: center;
}

.App-logo {
  height: 40vmin;
  pointer-events: none;
}

@media (prefers-reduced-motion: no-preference) {
  .App-logo {
    animation: App-logo-spin infinite 20s linear;
  }
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```
**[`C:\react\hello-react2\src\App.js`]**
```js

import React from 'react';
//import logo from './logo.svg';
import './App.css';

class App extends React.Component {
  render() {
    let styles = {  //객체
      backgroundColor: 'black', 
      padding: '16px',
      color: 'white', 
      fontSize: '12px'
    };
    return (
      <div>
        <div style={styles}>
          안녕하세요.
        </div>
        <div className="App">
          또 안녕하세요.
        </div>
      </div>

    );
  }
}

export default App;
```

### 주석
태그와 태그 사이에 주석을 넣을 때는
```js
class App extends React.Component {
  render() {
    let styles = {
      backgroundColor: 'black', 
      padding: '16px',
      color: 'white', 
      fontSize: '12px'
    };
    return (
      <>
        { /* 이것은 주석입니다. */ }
        { // 이것도 주석입니다. 
        }
        <div /* 이것도 주석입니다. */ 
          // 이것도 주석입니다. 
          style={styles}       
        >
          // 이것은 주석이 아닙니다.
          안녕하세요.
          /* 이것은 주석이 아닙니다. */
        </div>
      </>
    );
  }
}
```

## 컴포넌트 생성
`c:\react\hello-react2\src\MyName.js 파일을 생성`

**[c:\react\hello-react2\src\MyName.js]**
```js
/*
// React가 갖고 있는 컴포넌트를 쓰겠다.

import React, { Component } from 'react';

class MyName extends Component {
    
}
*/
import React from 'react';

class MyName extends React.Component {
    render() {
        return (    // 사용자에게 보여줄 화면을 return
            <div>
                안녕하세요.
                나는 { this.props.whoami }
            </div>
        );
    }
}

//화면에 나오려면 어떻게 해야하나? index.js에서 7번째쭐 처럼 App를 ReactDOM.ender함수에 넘겨줌.
export default MyName;
```
**[c:\react\hello-react2\src\index.js]**
myName 추가
```js
import MyName from './myName';
ReactDOM.render(<MyName />, document.getElementById('root'));
```

**[c:\react\hello-react2\src\App.js]**
```js

import React from 'react';
//import logo from './logo.svg';
import './App.css';
import MyName from './myName';

class App extends React.Component {
  render() {
    return (
      <>
      <MyName whoami="홍길동."></MyName>
      <MyName whoami="리액트."></MyName>
      <MyName whoami="땡땡땡 입니다."></MyName>
      </>
    );
    
  }
}

export default App;

```

props(자식 컴포넌트가 부모 컴포넌트로 부터 받은 값)는 자기를 호출하는 것

### default 값 적용
**[MyName .js]**
```js
/*
// React가 갖고 있는 컴포넌트를 쓰겠다.

import React, { Component } from 'react';

class MyName extends Component {
    
}
*/
import React from 'react';

class MyName extends React.Component {
    // 부모 컴포넌트에서 props 값이 전달되지 않았을 때
    // 사용할 기본값을 정의
    static defaultProps = {
        whoami: 'OOO'
    };


    render() {
        return (    // 사용자에게 보여줄 화면을 return
            <div>
                안녕하세요.
                나는 { this.props.whoami }
            </div>
        );
    }
}

//화면에 나오려면 어떻게 해야하나? index.js에서 7번째쭐 처럼 App를 ReactDOM.ender함수에 넘겨줌.
export default MyName;
```
MyName은 레고 블럭
이걸 필요로 하는 곳 (App)에서 이용하려면 import해서 사용

만약 이메일 입력하는 기능 만들었어
입력하려면은 입력한 값이 형식에 맞는지 확인 그런 컴포넌트 만들어 놔. 이메일이 유효한지 체크하는 인증방식. 이메일 주소로 test할 수 있는 검증용 문자를 보내는 것까지 만들어 놓으면 재사용 가능
이게 **컴포넌트**의 장점


## 함수형 컴포넌트
MyName.js 복사해서 붙여 넣기
class를 function으로 바꿔
함수형 컴포넌트 미세하게 빠름
**[MyName2]**
```js
import React from 'react';

// state(상태변수), LifeCycle 개념이 빠져 있음
// state는 해당 컴포넌트에서 갖고 있는 값
// LifeCycle 컴포넌트가 생성되고 소멸되기까지 과정이 있는데 얘는 그런 개념이 없음
// 값을 가지고 값에 따라 동작, LifeCycle이 필요하다 했을때 function 타입으로 하면 안됨
// Rendering할 내용을 return해주면 됨
// this라는 개념이 없고 function MyName2( {whoami})
//whoami는 객체 이름만 지금 객체 비구조화되고 있음
function MyName2 ({ whoami , age }) {
        return (    // 사용자에게 보여줄 화면을 return
            <div>
                안녕하세요.
                나는 <b> { whoami } </b>이고,
                나이는 <b> { age } </b>살 입니다.
            </div>
        );
    
}

// 파일명과 컴포넌트 명을 일치시키는게 좋음
// function 명과 export명이 같아야함 (파일명이랑은 사실 관련 없음)
export default MyName2;
```

**[App.js]**
```js

import React from 'react';
//import logo from './logo.svg';
import './App.css';
import MyName from './MyName';
import MyName2 from './MyName2';

class App extends React.Component {
  render() {
    return (
      <>
      <MyName whoami="홍길동."></MyName>
      <MyName whoami="리액트."></MyName>
      <MyName whoami="땡땡땡 입니다."></MyName>
      <MyName2 whoami="또길동" age = "23"></MyName2>

      </>
    );
    
  }
}

export default App;

```

#### 나이를 빨간색으로 하고 싶으면?
**[MyName2.js]**
```js
import './App.css';
나이는 \<b className="red"> {age} </b> 살입니다.
```
로 해도 됨.
이때는
**[App.css]**
```css
//추가
.red{		
	color: red;
}
```
또는
```js
// return 안에
import './App.css';
나이는 \<b sytle={{clolr:"red"}}> {age} </b> 살입니다.
```
또는
```js
//return 전에
let redColor = {
	color: 'red'
};

// return 안에
나이는 <b style={redColor}>{ age }</b>살 입니다.
```

### State(상태변수)에 대해서
**![](https://lh5.googleusercontent.com/95Vpim2zTuRnn11WDM1MtWucNXf3cGokoQBA-E9UIqssbWZFBaZXh09vjym9pv1lTIQqC98LeWT1L3_1YBqZvlczIojGLq1Jvsi-_T_CREqfB7SAIK3XKV6AjUcZ4hrQqmcyQS9N)** 와 같은 화면 만들려고 한다 이때

**jQuery 였다면** 다음과 같이 만들어야 했을 것
```js
$(function(){
	let count = 0;
	$('#add').click(function(){ 1. 전역변수 업데이트 2. 값부분에 전역변수 값 출력($('#value').text()) }
	}
);

$('#minus').click....(위와 같음)
```
값 업데이트하는 부분과 화면 입력하는 부분 불일치
값을 자동으로 처리해주면 얼마나 좋을까? 그게 React
화면 출력에 관여하는 그 컴포넌트가 갖고 있는 고유한 값 **State**

#### React를 이용해서 만들어 보자
`C:\react\hello-react2\src\Counter.js` 파일을 생성

**[App.js]**
```js

import React from 'react';
import Counter from './Counter'

class App extends React.Component {
  
  render() {
    
      return <Counter></Counter>
        
  }
}

export default App;

```
**[Counter.js]**
```js
import React from 'react'

class Counter extends React.Component {
    // state 값이 바뀌면 render()를 다시해줌
    // 값은 setState()라는 함수를 통해서 바뀜
    // Counter 클래스의 필드 문법을 이용해서 state를 정의
    // 아직 표준문법 아님. 하지만 곧 될거야
    state = {
        number: 0 // number라는 값을 가질 수 있고 초기값은 0
    
    };
    // 필드를 안쓴다고하면 해당하는 클래스 생성될때 사용할 수 있는 것이 있음. Constructor
    // props 부모 컴포넌트에서 자식 컴포넌트에게 주는 것
    /* 생성자에서 state 정의하는 것
    constructor(props) {
        super(props);
        this.state = {
            number: 0
        };
    }
    */
    
    // 컴포넌트에서 발생한 이벤트를 처리할 메소드를 정의
    // 일반적으로 함수 이벤트를 처리하는 이름은
    // onXXXXX = () =>
    // handleXXXX = () =>
    // 보통 이렇게 많이 씀
    onIncrease = () => {
        // 이 코드 처럼 상태 변수의 값을 변경할 때는 직접 변경하면
        // 값은 바뀔지라도 화면에 갱신(업데이트) 되지 않음
        // this.state.number = this.state.number +1;
        // 상태 변수의 값은 setState() 메소드를 이용해서 변경
        
        this.setState( { number: this.state.number + 1} ) // 객체라서 중괄호 안에 number안에 넣어줘야함
    };
    onDecrease = () => {

	    // 좀 더 간결하게 보임
	    const { number } = this.state;
		/*
		//만약 이러면
		// 객체 비구조화 가능
		// { } 안에 쓰면 this.state의 변수 number, name이 자동으로 뽑혀져 나감
		let { number, name } = this.state;
		
	    let number = this.state.number;
	    number += 1;
	    let name= this.state.name;
	    name += number;
	    this.setState({
		    number, name
	    });
		
	    */
	    this.setState({
		    number: number - 1
		});
    };
    render() {
        return (
            <div>
                <h1>카운터</h1>
                <div>값 : {this.state.number} </div>
                <button onClick={ this.onIncrease }>+</button>
                <button onClick={ this.onDecrease }>-</button>
            </div>
        );
    }

}

export default Counter;
```
만약 setState()를 이용하지않고 상태변수를 바꾸면 상태변수의 값은 바뀌지만 화면에 rendering은 되지 않음

**참고**
클래스가 있으면 클래스가 갖고 있는 변수 **필드**
클래스가 가지고 있는 함수 **메소드**

필드를 안쓴다고하면 해당하는 클래스 생성될때 사용할 수 있는 것이 있음. **Constructor**

#### 상태변수 할당 방법
**방법0**
```js
this.setState({ number: this.state.number + 1 });
```
**방법1**
```js
let number = this.state.number;
number += 1;
this.setState({ number: number });
```

**방법2. 객체 비구조화를 이용해서 상태변수의 값을 지역변수에 할당**
```js
let { number } = this.state;
number += 1;
this.setState({ number: number });
```

**방법3. 단축속성명을 이용해서 상태변수의 값을 변경**
이게 가장 세련된 방법ㅋㅋ
상태변수가 많을 수록 빛을 발한다
```js
let { number } = this.state;
number += 1;
this.setState({ number });
```

책에 있는 내용을 조금 해봅시다
p106
## UI 라이브러리를 사용하지 않는 코드
 `C:\react\hello-react2\todo.html 파일을 생성`
 `C:\react\hello-react2>npx http-server`
 http://localhost:8080/hello-react2/todo.html -> 실행 확인 
--> **UI 라이브러리를 사용하지 않으면 이렇게 복잡하게 짜야한다**를 보여줌

**[todo.html]**
```html
<html>
    <body>
        <div class="todo">
            <h3>할 일 목록</h3>
            <ul class="list"></ul>
            <input class="desc" type="text" />
            <button onclick="onAdd()">추가</button>
            <button onclick="onSaveToServer()">서버에 저장</button>
        </div>
        <script>
            let currentId = 1;
            const todoList = [];
            function onAdd() {
                const inputEl = document.querySelector('.todo .desc');
                const todo = { id: currentId, desc: inputEl.value };
                todoList.push(todo);
                currentId ++;
                const elemList = document.querySelector('.todo .list');
                const liEl = makeTodoElement(todo);
                elemList.appendChild(liEl);
            }
            function makeTodoElement(todo) {
                const liEl = document.createElement('li');
                const spanEl = document.createElement('span');
                const buttonEl = document.createElement('button');
                spanEl.innerHTML = todo.desc;
                buttonEl.innerHTML = '삭제';
                buttonEl.dataset.id = todo.id;
                buttonEl.onclick = onDelete;
                liEl.appendChild(spanEl);
                liEl.appendChild(buttonEl);
                return liEl;
            }
            function onDelete(e) {
                const id = Number(e.target.dataset.id);
                const index = todoList.findIndex(item => item.id === id);
                if (index >= 0) {
                    todoList.splice(index, 1);
                    const elemList = document.querySelector('.todo .list');
                    const liEl = e.target.parentNode;
                    elemList.removeChild(liEl);
                }
            }
            function onSaveToServer() {
                //  todoList 전송
            }
        </script>
    </body>
</html>
```

### p107 페이지 참고해서 동일한 기능을 React로 작성
`C:\react\hello-react2\src\MyComponent.js 파일을 생성`
**[App.js]**
```js

import React from 'react';
import MyComponent from './MyComponent'

class App extends React.Component {
  
  render() {
      
      return <MyComponent></MyComponent>
      
        
  }
}

export default App;

```
사용자 정의 속성을 렌더링해야 한다면 속성의 접두사로 data-를 사용

**[MyComponent.js] 설계**
```js
import React from 'react';

class MyComponent extends React.Component {
    state = {
        desc: '',
        currentId: 1,
        todoList: [],
    };
    onAdd = () => {
        
    };
    onDelete = e => {
        
    };
    onSaveToSrver = () => {
        //todoList 전송
    };
    onChangeDesc = e => {
        
    };
    render() {
        const { desc, todoList } = this.state;
        return (
            <div>
                <h3>할 일 목록</h3>
                <ul>
                   
                </ul>
                <input type="text" value={desc} onChange={this.onChangeDesc}></input>
                <button onClick={this.onAdd}>추가</button>
                <button onClick={this.onSaveToSrver}>서버에 저장</button>
            </div>
        )
    }
}

export default MyComponent;
```
**[MyComponent.js]**
```js
import React from 'react';

class MyComponent extends React.Component {
    state = {
        desc: '',
        currentId: 1,
        todoList: [],
    };
    onAdd = () => {
	    // id는 현재 값 들어가고
        // desc는 onChange에서 변환된 desc 값 들어감
        // 단축 속성명
        // desc는 desc: desc 단순하게 적은 것
        const { desc, currentId, todoList } = this.state;
        const todo = { id: currentId, desc };
        this.setState({
            currentId: currentId + 1,
            todoList: [...todoList, todo],
        });
    };
    onDelete = e => {
        const { todoList } = this.state;
        const id = Number(e.target.dataset.id); // Number?
        const newTodoList = todoList.filter(todo => todo.id !== id);    // id가 다른 것만
        this.setState({ todoList: newTodoList });
    };
    onSaveToSrver = () => {
        //todoList 전송
    };
    onChangeDesc = e => { // desc 바꿈 //입력창 들어가는 것
    // 컴포넌트 기반으로하다보니 값의 변화에 따라 나타냄
        console.log(e);
        // const desc; 하는 이유 상태 변수와 이름이 같으면 setState({ desc: desc }) 처럼 할 수 있음
        const desc = e.target.value;
        this.setState({ desc });
    };
    render() {
        const { desc, todoList } = this.state;
        return (
            <div>
                <h3>할 일 목록</h3>
                <ul>
                    { todoList.map(todo => (
                        <li key={todo.id}> 
                            <span> {todo.desc} </span>
                            
                            <button data-id={todo.id} onClick={this.onDelete}>
                                삭제
                            </button>
                        </li>
                    ))}
                </ul>
                <input type="text" value={desc} onChange={this.onChangeDesc}></input>
                <button onClick={this.onAdd}>추가</button>
                <button onClick={this.onSaveToSrver}>서버에 저장</button>
            </div>
        )
    }
}

export default MyComponent;
```

#### 강사님과 함께
**[MyComponent.js]**
-  in 화살표 함수, 반환하는 값이 객체 타입이면 () 로 묶어줘야한다
```js
import React from 'react';

class MyComponent extends React.Component {
    state = {
        desc: '',
        currentId: 1,
        todoList: [],
    };
    onAdd = () => {
        const { desc, currentId, todoList } = this.state;
        // id는 현재 값 들어가고
        // desc는 onChange에서 변환된 desc 값 들어감
        // 단축 속성명
        // desc: desc는 desc 의 원래 코드
        const  todo = { id:  currentId, desc }; // 내가 생성한 할일
        this.setState(
            //state 객체가 들어감
            {
                currentId: currentId + 1,
                todoList: [...todoList, todo],    // 기존 할일 + 내가 생성한 할일 
                desc: ""
            }
        );


    };
    onDelete = e => {
        const { todoList } = this.state;
        // data-id 해서 주면 dataset.id로 뽑아올 수 있음
        // Number() : 숫자로 변환
        const id = Number(e.target.dataset.id); 
        
        // 배열에서 filter라는 메소드는 뒤에 명시하고 있는 조건을 만족하는 것들로 다시 배열 만들때 사용
        const newTodoList = todoList.filter(todo => todo.id !== id );

        this.setState({
            todoList: newTodoList
        });
        
    };
    onSaveToSrver = () => {
        //todoList 전송
        console.log(this.state.todoList);
    };
    onChangeDesc = e => {   // desc 바꿈 //입력창 들어가는 것
        this.setState({ desc: e.target.value });
        
    };
    render() {
        const { desc, todoList } = this.state;
        return (
            <div>
                <h3>할 일 목록</h3>
                <ul>
                   { // <li> 들 중괄호에 return   
                        // map : 배열있으면 배열 요소 하나하나 가져와서 뒤에 지정해놓은 규칙에 따라 새로운 배열 만들어줌
                        // 배열의 각 요소 todo를 갖고오고 갖고오면 뒤에를 실행하라
                        // todo에는 id와 desc 갖고 있음
                        // todo => {} 안쓰고 todo => () 를 사용하는 이유
                        // in 화살표 함수, 반환하는 값이 객체 타입이면 () 로 묶어줘야한다
                        // 쓰려면 객체 안에서 반환해줘야함
                       todoList.map(todo => {
                           console.log(todo);
                           return (
                            <li key={todo.id}> 
                                    <span>{todo.desc}</span>
                                    {/* 어떤 애를 삭제해야하는지 알아야하니 data-id={todo.id} */}
                                <button data-id={todo.id} onClick={this.onDelete}>삭제</button>
                            </li>
                        );
                    })  
                   }
                </ul>
                <input type="text" value={desc} onChange={this.onChangeDesc}></input>
                {/* onChange눌리면 this.onChangeDesc 실행 */}
                <button onClick={this.onAdd}>추가</button>
                <button onClick={this.onSaveToSrver}>서버에 저장</button>
            </div>
        )
    }
}

export default MyComponent;
```

### 컴포넌트 상태값을 사용하는 코드
p109
#### 좋아요 버튼이 붉은색이면 파란색으로, 파란색이면 붉은색으로
**[App.js]**
```js
import React from 'react';

// 좋아요 버튼이 붉은색이면 파란색으로, 파란색이면 붉은색으로
class App extends React.Component {
  state = {
    color: 'red'
  };

  onClick = () => {
    let { color } = this.state; // 현재 색을 갖고옴
    color = color === 'red' ? 'blue' : 'red';
    this.setState({ color });
  }
  render() {
    return (
      <button style={{backgroundColor: this.state.color}} onClick={this.onClick}> 좋아요.</button>
    );
  }
}

export default App;
```
#### 좋아요 버튼을 클릭하면 배경색을 붉은색으로, 버튼 라벨을 "싫어요"로 변경하고, "싫어요" 버튼 클릭하면 배경색을 파란색으로 그리고 버튼 라벨을 "좋아요"로 변경
**[방법1] App.js**
```js
import React from 'react';

// 좋아요 버튼을 클릭하면 배경색을 붉은색으로, 버튼 라벨을 "싫어요"로 변경하고, "싫어요" 버튼 클릭하면 배경색을 파란색으로 그리고 버튼 라벨을 "좋아요"로 변경
class App extends React.Component {
  state = {
    text : '좋아요',
    color: 'blue'
  };

  onClick = () => {
    let { text, color } = this.state;
    text = text === '싫어요' ? '좋아요' : '싫어요';
    color = color === 'red' ? 'blue' : 'red';
    console.log(text);
    this.setState({ text, color });
  }
  render() {
    return (
      <button style={{backgroundColor: this.state.color}} onClick={this.onClick}>{ this.state.text}</button>
    );
      
  }
}

export default App;
```

**[방법2] App.js**
```js
import React from 'react';

// 좋아요 버튼을 클릭하면 배경색을 붉은색으로, 버튼 라벨을 "싫어요"로 변경하고, "싫어요" 버튼 클릭하면 배경색을 파란색으로 그리고 버튼 라벨을 "좋아요"로 변경
class App extends React.Component {
  state = {
    text : '좋아요',
    color: 'blue',
    liked: false,
  };

  onClick = () => {
    let { color, text, liked } = this.state;  // text, color는 안가져와도 되지만 setState를 위해 갖고옴
    liked = !liked;

    if(liked) {
      text = '좋아요';
      color = 'blue';
    }
    else {
      text = '싫어요';
      color = 'red';
    }
    console.log(text);
    this.setState({ text, color, liked });
  }
  render() {
    return (
      <button style={{backgroundColor: this.state.color}} onClick={this.onClick}>{ this.state.text}</button>
    );
      
        
  }
}

export default App;
```

### 부모 컴포넌트에서 속성값을 내려주는 코드
p110
Todo컴포넌트에서 Title 컴포넌트 호출
Title 컴포넌트에서는 Todo 컴포넌트에서 전달된 값을 보여줄 것임.
또한 Todo 컴포넌트는 '증가'버튼 갖고 있음.
증가버튼을 클릭하면 **현재 카운트는 OOO입니다.** Title 에서 출력
**[App.js]**
단일 컴포넌트 
```js
//function으로 만들어 보자
import React from 'react'

function Title(props) {
    if(props.count < 10 )
        return <p>{props.title}</p>
    else
        return <p style={{ color: "red"}}>{props.title}</p>
}

export default Title;
```
복수의 컴포넌트
```js
import React from 'react';
import Todo from './Todo';

class App extends React.Component {
  render() {
    return (
      <>
        <Todo />
        <Todo />
        <Todo />
        <Todo />
      </>
    );
  }
}

export default App;
```

**[Todo.js]**
```js
import React, { Fragment } from 'react';
import Title from './Title';

class Todo extends React.Component {
    state = {
        count: 0,
    };
    onClick = () => {
        this.setState({ count: this.state.count + 1 } );
    };
    render() {
        return (
            <Fragment>
                <Title count={this.state.count} title={`현재 카운트는 ${this.state.count} 입니다.`}></Title>
                {/* 왜 Title.js 를 만들어서 할까?
                    만약 카운트가 몇 이상 올라갔을 때 색을 바꿔주고 싶다.
                    이때 색을 바꾸는건 버튼과는 다른 기능. 이때 색을 바꿔주는 Component 만들고 적용하면 될듯.
                    여기서는 Title Component 이용해서 함 */}
                <div>
                    현재 카운트는 {this.state.count} 입니다.
                </div>
                <button onClick={this.onClick}>증가</button>
            </Fragment>
        );
    }
}

export default Todo;
```

**[Title.js]**
```js
//function으로 만들어 보자
import React from 'react'

function Title(props) {
    return <p>{props.title}</p>
}

export default Title;
```
