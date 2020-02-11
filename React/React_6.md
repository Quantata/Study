## 부모와 자식 state 공유
**[App.js]**
```js
import React from 'react';
import Parent from './Parent'

class App extends React.Component {
   render() {
     return <Parent></Parent>
   };
}

export default App;
```
**[Parent.js]**
```js
import React from 'react'
import Child from './Child'

class Parent extends React.Component {
    state = { // 상태변수는 객체
        name: ''
    };

    onChange = e => { // e ==> evnet, 즉 입력값이 있다.
        let {name} = this.state;
        name = e.target.value;
        this.setState({ name });
    }
    render() {
        return (
            <>
                <h1>My Name is {this.state.name}</h1>
                <Child name={this.state.name} onChange={this.onChange} />
            </>
        );

    }
}
export default Parent;
```

**[Child.js]**
```js
import React from 'react'

function Child({ name, onChange }){
    return (
        <div>
            <input type="text" value={name} onChange={onChange} />
        </div>
    )
}

export default Child;
```


## creat-react-app 구조를 바꾸고 싶다면
`> create-react-app project`
`> npm start` 대신에
`> npm run eject`

원래 `>npm start`하면 react-script가 원래 구조대로 App.js, indes.js 실행 시킴

그러고 싶지 않다면 p1폴더를 만든 후 거기 들어가서
`> npm run eject`	// 구조를 풀어버리고
하고나서 폴더를 복사붙여넣기해서(?)
`> npm start` 하면
그게 뜸
그리고 만약 이렇게 되면 p1폴더에 어떤 라이브러리가 들어갔는지 알려줘야함
`npm install [package.json] --save`
package.json에 기술되지 않은 것 빼고 깔아줌
몰라몰라

---
eject 하면 일반적인 node 프로젝트로 바꿔줌 
config
- babel
- webpack
script 
	- build.js
	- start.js
	- test.js
생김
			
[https://react-md.mlaursen.com/](https://react-md.mlaursen.com/)
