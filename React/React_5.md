모듈화한다 컴포넌트화 한다는 것은
쉽게 꽂을 수 있다. 필요한 것을

## 자식 컴포넌트는 부모 컴포넌트가 렌더링 될때 함께 렌더링 된다
111p
**"증가2"버튼을 클릭했을 때 자식 컴포넌트도 함께 렌더링 된다**-> **불필요한 렌더링 발생** -> 이를 방지하기 위해서는 **React에서 제공하는 `React.memo`나 `React.PureComponent` 사용한다**
cmd에서 해당 폴더에 가서 `npm start`

### 함수형 컴포넌트 
**[App.js]**
```js
import React from 'react';
import Todo from './Todo';

class App extends React.Component {
  render() {
    return <><Todo /></>
  }
}

export default App;
```

**[Todo.js]**
```js
import React, { Fragment } from 'react';
import Title from './Title';

class Todo extends React.Component {
    state = { count: 0, count1: 0 };
    onClick = () => {
        this.setState({ count: this.state.count + 1});
    };
    onClick2 = () => {
        this.setState({ count1: this.state.count1 + 1});
    };    
    render() {
        return (
            <div>
                <Title title={`현재 카운트: ${this.state.count}`}></Title>
                <p>{this.state.count1}</p>
                <button onClick={this.onClick}>증가</button>
                <button onClick={this.onClick2}>증가2</button>
            </div>
        );
    }
}

export default Todo;
```

**[Title.js]**
```js
import React from 'react';

function Title(props) {
    console.log(props);
    return <p>{props.title}</p>
}

export default Title;
```

#### 불필요한 렌더링을 줄이기 위해 Title.js 에 React.memo 사용
함수형 컴포넌트인 경우, React.memo를 이용해서 자식 컴포넌트의 **불필요한 렌더링**을 줄일 수 있음

// props 값이 변경되는 경우에만 호출되는 것을 확인할 수 있음

`export default React.memo(Title);`

**[Title.js]**
```js
import React from 'react';

function Title(props) {
    console.log(props);
    return <p>{props.title}</p>
}
export default React.memo(Title);
```


### Class 컴포넌트
#### React.PureComponent 사용
클래스형 컴포넌트인 경우,
React.PureComponet를 이용하면 자식 컴포넌트의 **불필요한 렌더링**을 줄일 수 있음

**[Title.js]** 클래스형으로 바꿈
```js
import React from 'react'
//PureComponent
class Title extends React.PureComponent {

    constructor(props) {
        super(props);
    }
    render() {
        console.log(this.props);
        return <p>{this.props.title}</p>
    }
}

export default Title;
```

함수형으로 하나 클래스형으로 선언하나 결과값은 똑같음
**![](https://lh5.googleusercontent.com/c2_IbbvpnH7GXmv2QtZrn19fs8hBvkTAyri-aHojDrNdUer2miYX1j7WvDNW090q0rchsu6FX-e8AtFJfjkZNpwzPULM4g2kW4ca9VdWvPmRion3kP2Fwkivd1eNnT0yPl9S3IRx)**
---
# 3장 중요하지만 헷갈리는 리액트 개념 이해하기
## 3.1 상태값과 속성값으로 관리하는 UI 데이터

### setState()
p112
클래스형 컴포넌트에서 상태값을 변경할때 호출하는 메소드
setState 메소드로 입력된 객체는 기존 상태값과 병합(merge)
**[App.js]**
```js
import React from 'react';
import Todo from './Todo';

class App extends React.Component {
   state = {
     count1: 0, count2: 0
   };
   onClick = () => {
      this.setState({ count1: this.state.count1 +1 });
   };

   render() {
     const { count1, count2 } = this.state;
     return (
       <div>
         <p> {count1}, {count2} </p>
         <button onClick={this.onClick}>증가</button>
       </div>
     )
   }
}

export default App;
```
**![](https://lh3.googleusercontent.com/7S3pcwoceaiFX-6jn7LWrCnwz_1z98v_Uk-hjwGGJbok91GJMlpnaSCkZLiGbZCaf-1go3nbaR1kgv95g3rZyUA2P4b9tT8IEK31KF3RMedRL-leI2Va357-WFBlF3Aqf9aT59YV)**

### setState 메소드를 연속해서 호출하면 발생하는 문제점
p113
**리액트는 효율적인 렌더링을 위해서 여러개의 setState 메서드를 배치로 처리 → state 변수와 화면(UI)간 불일치가 발생할 수 있음**

만약 onClick() 함수에 setState를 증가한다면?
리액트는 setState()를 모아서(batch, 일괄처리) rendering함
**setState() 는 비동기 함수**
그래서 `count1`이 현재 첫번째 setState, 두번째 setState, 세번째 setState 모두 `0` 
**[App.js]**
```js
//onClick()에 추가
 onClick = () => {
    this.setState({ count1: this.state.count1 +1 });
    this.setState({ count1: this.state.count1 +1 });
    this.setState({ count1: this.state.count1 +1 });
 };
```

#### 방법1. 호출 직전의 상태값을 매개변수로 받아서 처리
만약 하나의 컴포넌트 안에서 setState() 여러번 출력해야 한다면
`prevState` 이용!
**[App.js]**
```js
   onClick = () => {
      this.setState({ count1: this.state.count1 +1 });
      this.setState({ count1: this.state.count1 +1 });
      this.setState({ count1: this.state.count1 +1 });

      //prevState는 직전값을 받아올 수 있음
      this.setState(prevState => ({ count2: prevState.count2 + 1}));
      this.setState(prevState => ({ count2: prevState.count2 + 1}));
      this.setState(prevState => ({ count2: prevState.count2 + 1}));
   };
```
**![](https://lh3.googleusercontent.com/lOabppXQu0nHsquMkVTndmpZWjYOleQzST993njmHfk_Kx-uNdmo6jyPUk9QBDHtUwyYiTflB1s0bL81SQ6SDA4MHwOZeQlxhBIVX_n3n35-z8fZBf0PSHBmknwyik0fDAHbNbBf)**

#### 방법2. 상태값 로직을 분리해서 사용
**[App.js]**
```js
import React from 'react';
import Todo from './Todo';

const actions = {
  
  init() {
    return { count: 0 };
  },
  increment(state) {  // prevState 값이 state에 들어간 거임
    return { count: state.count + 1 };
  },
  decrement(state){
    return { count: state.count - 1 };
  }
}

class App extends React.Component {
  state = actions.init(); // state는 count가 0인 객체를 가지게 됨
  onIncremenet = () => {
    this.setState(actions.increment);
  };

  onDecremenet = () => {
    this.setState(actions.decrement);
  };
  render() {
    return(
      <div>
        <p>{this.state.count}</p>
        <button onClick={this.onIncremenet}>증가</button>
        <button onClick={this.onDecremenet}>감소</button>
      </div>
    );
  }
}

export default App;
```

#### setState 메소드는 비동기로 처리되지만 호출순서는 보장된다
p114
**[App,js]**
```js
import React from 'react';
import Todo from './Todo';


class App extends React.Component {
 state = { count1: 0, count2: 0 };

 onClick = () => {
  // 방법1
  // this.setState({ count1: this.state.count1 + 1 });
  // this.setState({ count2: this.state.count2 + 1 });

  // 방법2
  let { count1, count2 } = this.state;
  count1 += 1;
  count2 += 1;

  //일괄처리 방식이지만 순서는 지켜주기 때문에 count1이 count2보다 항상 크거다 같다
  this.setState({ count1 });
  this.setState({ count2 });
 };
 render() {
   const { count1, count2 } = this.state;
   const result = count1 >= count2;
   return (
    <div>
      <p>{count1} >= {count2} </p>
      <p>{String(result)} </p>
      <button onClick={this.onClick}>증가</button>
    </div>
   );
 }
}

export default App;
```
**![](https://lh4.googleusercontent.com/MLqBtpPUOlRfPvUpCWUZ0KgUzx_ku022IwQU3JF-GoBUi0KqUyQtm1bPFH-cwnVyVWEHSAfYvmNN-o6WsJ2MYgaWLb0YMPAEx_68I2W5OELkb83yaBYK5dfuNZL7n4tZJSOyamSI)**

### setState 메소드의 두번째 매개변수는 처리가 끝났을 때 호출되는 콜백 함수
p115
**setState 메소드의 두번째 매개변수는 처리가 끝났을 때 호출되는 콜백 함수**
**(componentDidUpdate()의 사용을 권장)**

렌더링이 되고 나서 실행되는 콜백 함수
두번째 매개변수를 사용하면 쓸 수 있음

바뀌었는지 그때그때 알고 싶을때 있음
그럼 setState()의 두번째 매개변수에 함수 넣어줄 수 있음
```js
//App.js의 onClick 함수에
  this.setState({ count1 }, () => console.log(`count1 = ${count1}`));
  this.setState({ count2 }, () => console.log(`count1 = ${count2}`));

render() {
	console.log("render is called");
	...
}
```
나오는 시점은 바뀐 것을 화면에 반영하고 나면 나옴.
실행하면 rendering 먼저 실행되고 count 변화됨.
**![](https://lh5.googleusercontent.com/7T6unCdUGjPHo2vkqRAjwan8Hpxu5OMYH97cicH3NIEp9ChOCCIGeyGXiw5NWP9r9d2P0BCJ49YvlcRA023glg27t-e9uGMLnsOolML2E5oUgZnZ4_AmMYLx5oU5H-OxIg75AxZH)**

## 3.2 리액트 요소와 가상돔
p116
**`요소`** = element = tag
**`가상돔`** = react에서 element의 변경을 찾을때 가상돔을 이용
(element의 변경사항을 반영할때 사용)
> 가상돔
> 렌더링 성능을 위해 가상 돔을 활용
> 빠른 렌더링을 위해 돔변경을 최소화 해야하는데 메모리에 가상 돔을 올려놓고 이전과 이후의 가상 돔을 비교해서 변경된 부분만 실제 돔에 반영하는 전략을 React에서 사용

p7
`createElement( [문자열], [데이터 상태(객체로 들어감)], [컴포넌트 값 또는 서브 element])`
이거 쓰면 가독성이 너무 떨어짐(복잡)
그래서 `jsx`를 이용하자

p116_**코드 3-17 리액트 요소의 구조**
key는 element 빠르게 찾을때 사용. 빠르게 접근 가능
ref는 화면에 직접적인 접근을 하려고 할때(입력창 포커스 바꾸기와 같은)

p117_**코드 3-18 리액트 요소의 구조**
```js
const element = <h1>제 나이는 {20 + 5}세 입니다.</h1>
{
	type: 'h1'
	props: {
			children: [ '제나이는 ', 25, '세 입니다.'],
	}
	...
}
```
\<h1> 태그 사이에 잘라서 children 항목으로 분할해서 들어간다.

**[App.js]**_3-16,17,18 코드
```js
import React from 'react';

class App extends React.Component {
  render() {
    const code3_16 = <a href="http://www.google.com">click here</a>;
    console.log(code3_16);
    const code3_17 = <a key="key1" style={{width:100}} href="http://google.com">click here</a>;
    console.log(code3_17);
    const code3_18 = <h1>제 나이는 {20+5} 세입니다.</h1>;
    console.log(code3_18);
    return(<div></div>);
  }
}

export default App;
```

### 리액트 요소가 돔 요소로 만들어지는 과정
119p
렌더링 단계를 거칠때 가상돔을 이용한다.
**가상돔이란**
가상돔 요소들을 분석해서
type
ref
key
이렇게 만들어 놓은 것을 분석 및 비교해서 변경사항 반영하는 것

[in React]
- **렌더 단계(render phase) **
	- 데이터 변경에 의한 화면 업데이트
	- 실제 돔에 반영할 변경 사항 파악하는 단계
	- **변경사항을 파악하기 위해 이 단계에서 가상 돔을 이용**
- **커밋 단계(commit phase)**
	- 파악된 변경 사항을 실제 돔에 반영하는 단계


**[Todo.js]**
```js
import React from 'react';
import Title from './Title';

class Todo extends React.Component {
    state = { priority: 'high' };
    onClick = () => {
        let { priority } = this.state;
        priority = priority === 'high' ? 'low' : 'hgih';
        this.setState({ priority });

    };
    render() {
        // Title의 부모 컴포넌트가 title과 desc 줄거임
        const { title, desc } = this.props;
        const { priority } = this.state;
        // 원래 element return안에 넣었었는데 element에서 지정하고 return에 넘겨주겠다.
        const element = (
            <div>
                <Title title={title} />
                <p>{desc}</p>
                <p>{priority === 'high' ? ' 우선순위 높음' : '우선순위 낮음'}</p>
                <button onClick={this.onClick}>우선순위 변경</button>
            </div>
        );
        console.log(element);
            
        return element;
    }
}

export default Todo;
```

**[App.js]**
```js
import React from 'react';
import Todo from './Todo';

class App extends React.Component {
  render() {
    const element = <Todo title="리액트 공부하기" desc="실전 리액트를 열심히 읽는다."></Todo>
    console.log(element);

    return (element);
  }
}

export default App;
```

**[Title.js]**
얘는 pureComponent
```js
import React from 'react'

class Title extends React.PureComponent {

    constructor(props) {
        super(props);
    }
    render() {
        const { title } = this.props; // Todo.js에서 호출
        const element = <p style={{color:'blue'}}>{title}</p>;
        console.log(element);
        return element;
    }
}

export default Title;
```
**![](https://lh3.googleusercontent.com/vaEeQMQXOHOFM3tTZJVNHdKjbWGw3N4MVjkgShL5yehhDfZRwxmZ0S8S_suVUPgMwEzB5KwHK68-HJBmiaEmfirbZ83pz9cTDVL9FFRG6R2waGwWqDhU9FnqaML05tDC2WoH_wMR)**
리액트 요소 트리가 실제 돔으로 만들어지기 위해서는 **모든 리액트 요소의 type 속성값이 문자열** 이어야함.

화면에 무엇을 찍어주기 위해서는 타입이 모두 문자열이여야함. 그래서 child component들을 호출호출호출 함.
전체가 문자열이 되면 render함수를 거쳐서 화면에 출력해줌

**실제 돔을 만들 수 있는 리액트 요소 트리를** **`가상돔`** 이라고 한다.
최초의 리액트 트리로부터 가상 돔을 만들고 이전 가상돔과 비교해서 실제 돔에 반영할 내용을 결정하는 단계를 **렌더단계** 라고 한다.

엄밀히 말하면 react 요소는 **fiber**라는 구조체로 변환

---
## 요약
식별자
변수
함수

변수 - 객체가 갖고 있는 변수를 속성이라고 함

Math.max() : 이거는 메소드
max() : 는 함수
자바스크립트의 식별자 유형

주석문은 실행에 포함되지 않는 코드다

자바스크림트에서 문자열
따옴표로 묶여있는 데이터
'abc', "abc", \`abc`

console.log(100<200<300);		// true
console.log(300>200>100);		// false
->300>200 = true = 1

Boolean(밑에거)
null / undefined / '' / 0 / NaN => false 반환

[this를 쓴다]
```html
<script>
    let score = {
        korean: 90,
        math: 100,
        science: 80,

        sum : function() {
            return this.korean + this.math + this.science;
        },
        average: function() {
            return this.sum() / 3;
        },
    };

    console.log(`총점: ${score.sum()}, 평균: ${score.average()}`);
</script>
```

외부 패키지 갖고와야하는데 어려움.
그래서 React에서 초기 진입이 쉽도록 만들어 놓은 것이 `create-react-app`

```js
<html>
    <head>
        <div id="xyz"></div>
    </head>
    <body>
        <script>
            class Hello extends React.Component {
                render {
                    return <h1> Hello React!!! </h1>

                };
            }

            ReactDOM.render(
                <Hello/>,   // Hello라는 render된 결과가 들어갈 것
                document.getElementById('xyz') // 문서에서 id가 xyz인거 찾아내겠다.(head에 있음)
            )

        </script>
    </body>
</html>
```

create-react-app
npm start : 내가만든 react 앱을 개발모드로 실행
npm run build : 내가 만든 react 앱을 빌드(배포할 수 있는 형태로 transcompiling하고 webpack으로 ..
npm run ejact : 
(20~25p)

```js
//JSX 구문
<h1> Hello React!!! </h1>
React.createElement(
	'h1',
	{},
	"Heelo Wold;
);
```
```js
//jsx구문 쓸때 사용안됨
<input type="text">
//반드시 닫아야 함
<input type="text"/>
```

```js
Class Car extends React.Component {
	render() {
		return <div>It's ___ color.</div>;
	}
}
ReactDOM.render(<Car color="red"/>, document.getElementById("root"));

* ___에 무엇을 넣어야할까?
{ this.props.color } : Car color가 전달하는 red 값을 전달하기 위해서는 this.props : 부모 컴포넌트로부터 전달된 값을 찍어줄때는 props

```

```js
class Car extends React.Component {
	render() {
		//return <h2> {this.props.brand.model} </h2>
		return <h2> {		} {			} </h2> //여기서 전달된 값으로 출력할 거임
		-> { this.props.brand.name } { this.props.brand.model}
	}
}

class Garage extends React.Component {
	render() {
		const carinfo = { name: "SM5", model: "2019" };
		return (
			<div>
				<Car brand = {carinfo} />
				
		);
	}
}

ReactDOM.render(<Garage />, document.getElementById("root"));

// 이런 출력을 난 원함
<div><h2>SM5 2019년식</h2></div>
```

Hello [입력창] 에 따라 바뀌는 코드
**[App.js]**
```js
import React from 'react';
import Todo from './Todo';

class App extends React.Component {
  state = {
    name: '',
  };

  changeHandler = (event) => {
    const name = event.target.value;
    this.setState({ name });
  };
  render() {
    const element =
    (
      <form>
        <h1>Hello {this.state.name}</h1>
        <p style={{color: 'blue', backgroundColor: 'yellow'}}>Enter your name:</p>
        <input type="text" onChange={this.changeHandler}></input>
      </form>
    );

    return (element);
  
  }

}

export default App;
```
**![](https://lh6.googleusercontent.com/W9wJn-dOHmIWqjun5HXeOX4RNEorVV_mqZZx3F-RP3bJolhIqNOM1HChsdjonUkgNH16eY7uM9HaipO2pLo1fqH1iHVeg6AP-71F6Lfo8OnrCGN9mlY_ZZuShw3wrP3L-F8Lys8-)**

**문제는 w3schools**에서 **React Tutorial**에서 다 냈습니다.
실기 문제는 제공되는 코드를 이용하여 다음과 같은 기능을 완성하시오


## 3.3 생명주기 메소드
p124
**[http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)**

그림으로 볼 수 있도록

Render 단계
- 생성되고 props부터 state가 만들어지고(부모로 부터 전달된 내용이 자식에게 설정되는 단계)
- 그다음 Render함수가 호출

Pre-Commit
- 돔을 읽을 수 있는 단계
- 돔이 업데이트

Commit
- 돔에 변경된 내용 추가
**![](https://lh6.googleusercontent.com/v_LKNagQuAnGPfEuG9yx5A4Bud5O2ZbLLbjvI_9B5qrdSYk6i2tXfTXE_1W_umWxtTctwbkMyo8_bI0JqB1zZOMBfOCG7iVy9-GKDzsnU5olVEYVG7ap4meBLF7LgE8fUuLt_lAn)**

**[App.js]**
```js
import React from 'react'

class Counter extends React.Component {
    state = { number: 0};
    onIncrease = () => {
        this.setState({ number: this.state.number + 1});
    }

    constructor(props){
        // P126 constructor 메소드 내부에서는 반드시 super 함수를 호출해줘야 한다.
        // 초기화
        super(props);
        console.log("constuctor");
    }
    static getDerivedStateFromProps(props, state){
        console.log("getDerivedStateFromProps");
    }

    render() {
        console.log("render");
        return (
            <div>
                <h1>Counter</h1>
                <div>Value : {this.state.number}</div>
                <button onClick={this.onIncrease}>+</button>
            </div>
        );
    }
    componentDidMount(){
        console.log("componentDidMount");
    }

}

export default Counter;
```
**![](https://lh6.googleusercontent.com/2kMU8cTBx8zJOroV04XEyNTDNsriJmfk8Qd55zFSrb7E4sHacscj2lcnq-RMx1JUh86OIpkr6NKSyWcozVqF2ssvCy3bG-itW16EZ3HIutaQPKCaCEoT309v6iws5Z2AbgLlX1FC)**

이런걸 어디에 써먹나요?
우리 책에 몇개 나와있음. 일단 `Box.js` 를 만들겠다.
### componentDidMount 메서드
#### 해당하는 Box의 width가 400보다 작으면 빨간색, 크면 파란색
137p
`C:\react\hello-react2\src\Box.js` 생성
컴포넌트가 생성이 완료되면(componentDidMount() 호출되면) 보여짐과 동시에 width를 알게 됨.

**[App.js]**
```js
import React from 'react';
import Box from './Box';

class App extends React.Component {
  render() {
    return <Box />
  }
}

export default App;
```

(중요한 부분)
// 실제 width 가져와야함
// 그러기 위해서는 Box에서 실제 돔요소를 직접 access해야함
// key 엘리먼트에 배열이 있을때 쉽게 접근
// ref 돔 요소 직접 access 하기위해서 접근(렌더링된 화면, 거기에는 브라우저에서 보여지는 html로 다 바뀐 결과가 보임. 거기에 직접적으로 접근하기 위해서는 ref필요)

**[Box.js]**
```js
// 해당하는 Box의 width가 400보다 작으면 빨간색, 크면 파란색
import React from 'react';

class Box extends React.Component {
    state = {
        boxWidth: 0
    };

    divRef = React.createRef(); // Reference 하나 만듦

    // rendering이 다되면 componentDidMount()가 실행됨
    // 그럼 걔의 width를 알 수 있음
    componentDidMount() {
        const rect = this.divRef.current.getBoundingClientRect();
        this.setState({ boxWidth: rect.width });
    }
    render() {
        // 중괄호로 갖고 오는 것 다른 객체(state)에서 갖고오는 것
        const { boxWidth } = this.state;
        const backgroundColor = boxWidth < 400 ? 'red': 'blue';
        return (
            // 실제 width 가져와야함
            // 그러기 위해서는 Box에서 실제 돔요소를 직접 access해야함
            // key 엘리먼트에 배열이 있을때 쉽게 접근
            // ref 돔 요소 직접 access 하기위해서 접근(렌더링된 화면, 거기에는 브라우저에서 보여지는 html로 다 바뀐 결과가 보임. 거기에 직접적으로 접근하기 위해서는 ref필요)
            <div ref={this.divRef} style={{width: '100%', height: '100px', backgroundColor}}>box</div>
        );
    }
}

export default Box;
```
`divRef = React.createRef(); // Reference 하나 만듦`
이 부분 중요

### getSnapshotBeforeUpdate 메소드
render 함수를 통해 변경된 DOM을 Update하기 직전에 호출되는 함수

p140
여기서는 **반영할지 말지 정할 수 있음**
**[Box.js]**
```js
import React, { Fragment } from 'react';
class Box extends React.Component {
    state = {
        items: []
    };
    divRef = React.createRef();

    //render 함수를 통해 변경된 DOM을 Update하기 직전에 호출되는 함수
    getSnapshotBeforeUpdate(prevProps, prevState ) {    // 돔 업데이트 전에 snapshot 가져온다
        console.log('getSnapshotBeforeUpdate()');

        const { items } = this.state;
        if (prevState.items.length < items.length ){    // update되기 전의 상태 // items.lenght는 바뀔 값
            // 기존의 값(prevState)보다 배열이 크다면 바뀌는 것임
            const rect = this.divRef.current.getBoundingClientRect();
            console.log("getSnapshotBeforeUpdate() 반환값", rect.height );
            return rect.height; // snapshot, componentDidUpdate의 세번째 매개변수로 들어감
            // rect의 height
        }
        return null;
    };
    componentDidUpdate(prevProps, prevState, snapshot){
        console.log('componentDidUpdate()');

        if (snapshot !== null ){
            const rect = this.divRef.current.getBoundingClientRect();   // 크기같은 상태정보
            console.log(rect.height);
            if (rect.height !== snapshot){
                console.log("새로운 줄이 추가되었습니다.");
            }
        }
    };
    componentDidMount() {
        console.log('componentDidMount()');

        const rect = this.divRef.current.getBoundingClientRect();

        this.setState({ boxWidth: rect.width });
    };
    onClick = () => {
        console.log('onClick()');
        const { items } = this.state;
        this.setState({ items: [...items, `${items.length+1}'s itmes`] });
    };
    render() {
        console.log('render()');

        const { items } = this.state;
        const { boxWidth } = this.state;
        // const backgroundColor = boxWidth < 400 ? 'red' : 'blue';
        return (
            <Fragment>
                <button onClick={this.onClick}>추가하기</button>
                <div ref={this.divRef} style={{ width: '100%' }}>
                    {
                        items.map(item => <p stytle={{ height: 50 }}>{item}</p>)
                    }
                </div>
            </Fragment>
        );
    }
}
export default Box;

```

바뀐 값만 갖고 있으면 되지 화면에 꼭 안보여줘도 될때 
**shouldComponentUpdate 메소드** 사용
날씨, 버스 조회 (그래픽 부분) 등

### shouldComponentUpdate 메소드
render함수를 호출할건지 말건지 결정
얘가 false 반환하면 rendering안함

**[Box.js]**
```js
import React, { Fragment } from 'react';
class Box extends React.Component {
    state = {
        items: []
    };
    divRef = React.createRef();
    
    // render함수를 호출할건지 말건지 결정
    // 얘가 false 반환하면 rendering안함
    // 짝수번째에 렌더링
    shouldComponentUpdate(nextProps, nextState){
        return nextState.items.length % 2 === 0;
    }

    //render 함수를 통해 변경된 DOM을 Update하기 직전에 호출되는 함수
    getSnapshotBeforeUpdate(prevProps, prevState ) {    // 돔 업데이트 전에 snapshot 가져온다
        console.log('getSnapshotBeforeUpdate()');

        const { items } = this.state;
        if (prevState.items.length < items.length ){    // update되기 전의 상태 // items.lenght는 바뀔 값
            // 기존의 값(prevState)보다 배열이 크다면 바뀌는 것임
            const rect = this.divRef.current.getBoundingClientRect();
            console.log("getSnapshotBeforeUpdate() 반환값", rect.height );
            return rect.height; // snapshot, componentDidUpdate의 세번째 매개변수로 들어감
            // rect의 height
        }
        return null;
    };
    componentDidUpdate(prevProps, prevState, snapshot){
        console.log('componentDidUpdate()');

        if (snapshot !== null ){
            const rect = this.divRef.current.getBoundingClientRect();   // 크기같은 상태정보
            console.log(rect.height);
            if (rect.height !== snapshot){
                console.log("새로운 줄이 추가되었습니다.");
            }
        }
    };
    componentDidMount() {
        console.log('componentDidMount()');

        const rect = this.divRef.current.getBoundingClientRect();

        this.setState({ boxWidth: rect.width });
    };
    onClick = () => {
        console.log('onClick()');
        const { items } = this.state;
        this.setState({ items: [...items, `${items.length+1}'s itmes`] });
    };
    render() {
        console.log('render()');

        const { items } = this.state;
        const { boxWidth } = this.state;
        // const backgroundColor = boxWidth < 400 ? 'red' : 'blue';
        return (
            <Fragment>
                <button onClick={this.onClick}>추가하기</button>
                <div ref={this.divRef} style={{ width: '100%' }}>
                    {
                        items.map(item => <p stytle={{ height: 50 }}>{item}</p>)
                    }
                </div>
            </Fragment>
        );
    }
}
export default Box;
```

### componentWillUnmount()
143p
componentDidMount에서 이벤트에 대해 설정해 놨다가
이벤트가 발생했을때 특정 메소드를 호출할 수 있도록 해라
```js
class MyComponent extends React.Component {
	componentDidMount(){
		const domNode = documnet.getElementById('someNode');
		domNode.addEventListener('change', this.onChange);
		domNode.addEventListener('dragstart', this.onDragStart);

	}
	componentWillUnmount(){
		const domNode = documnet.getElementById('someNode');
		domNode.removeEventListener('change', this.onChange);
		domNode.removeEventListener('dragstart', this.onDragStart);

	}
}
```
문제 이벤트 설정해 놓고 해제를 안해줄 때가 있음
이런걸 예방하기 위해서 **React Hook(리액트 훅)** 이란걸 씀

### getDerivedStateFromError, componentDidCatch 메서드
145p
자식 컴포넌트에서 발생한 예외를 부모 컴포넌트에서 처리하려면 어떻게 해야할까?

145p_**코드 3-52**
`C:\react\hello-react2\src\ErrorBoundary.js` 파일생성

**[ErrorBoundary.js]**
```js
// p145 코드 3-52 참조
import React from 'react';

class ErrorBoundary extends React.Component {
    state = { 
        error: null
    };

    render(){
        const { error } = this.state;
        if (error) {
            return <div>{error.toString()}</div>
        }

        return this.props.children;
    }
}

export default ErrorBoundary;
```

**[App.js]**
```js
import React from 'react';
import ErrorBoundary from './ErrorBoundary';
import Counter from './Counter';
class App extends React.Component {
  render() {
    return <ErrorBoundary><Counter></Counter></ErrorBoundary>
  }
}

export default App;
```
**![](https://lh5.googleusercontent.com/h3n1xRAYBZe-uFJIbFNk6qZtdG96sSO3CuhwS1ylsr8aWqDyatJIgZCgvLfQZWs_W2fb1ucnpT7kKwYydQ6lbdreV-PU9-B0liMp2QHoHP0A_Wj0zASykSUpbi2S76_408xVGo0S)**

Virtual DOM으로 나올때
type
- 문자열인 경우 : html 태그
- class ErrorBoundary 처럼 : 컴포넌트
key
- 
ref
props
- 여러개 객체 들어가는데 children 배열
- 값이나 하위 element
- 위의 애는 children[Counter] 있음

자식 컴포넌트의 error을 담을 변수를 ErrorBoundary의 state에 선언
그게 값이 있으면 error 값을 반환. 아니면 children(여기서는 Counter.js) 호출

**[ErrorBoundary.js]** 에 추가
```js
// p145 코드 3-52 참조
import React from 'react';

class ErrorBoundary extends React.Component {
    state = { 
        error: null
    };

    // p144
    // 에러 정보를 상태값에 저장해서 화면에 출력하는 용도로 사용
    static getDerivedStateFromError(error){
        console.log("getDerivedStateFromError", error);
        return { error };   // 여기서 설정된 에러는 state = { error: null }에 가는거
    }

    // 에러 정보를 서버로 전송하는 용도로 사용
    componentDidCatch(error, info) {
        console.log("componentDidCatch", error, info);
    }
    render(){
        const { error } = this.state;
        if (error) {
            console.log("boundary rendering error2")

            return <div>{error.toString()}</div>
        }
        console.log("boundary rendering children")

        return this.props.children; // this.props == ErrorBoundary의 props / 의 children
    }
}

export default ErrorBoundary;
```

**[Counter.js]**
```js
import React from 'react'

class Counter extends React.Component {
    state = { number: 0};
    onIncrease = () => {
        this.setState({ number: this.state.number + 1});
    }

    constructor(props){
        // P126 constructor 메소드 내부에서는 반드시 super 함수를 호출해줘야 한다.
        // 초기화
        super(props);
        console.log("constuctor");
    }
   
    render() {
        const { number } = this.state;
        if (number >= 3) {
            throw new Error("에러 발생!!");
        }   
        return <div onClick={this.onIncrease}>{`클릭하세요. (${number}번째 클릭입니다.)`}</div>
    }

}

export default Counter;
```
**![](https://lh5.googleusercontent.com/5CNOafOv0il7BVOnLT76gVUFEfoot4mKud3yVNcpGU_IYIFqc76imwL8mkJ6la1908QWuu_ZzBqwMiwajUJ6iCUQ-RVa3y0X8rXtzVfgqGdvZWoTKvEhPe2oqLZVHqR7tHSu3eqM)**


## 3.4 컨텍스트 API
p148
상위 컴포넌트에서 하위에 있는 모든 컴포넌트로 직접 데이터 전달이 가능
\<App> 에서 갖고 있는 어떤 값을
\<Greeting />에 주려고하면 어떻게 해야할까?
App가 username이라는 상태변수 갖고 있어
이 username을 Greeting에 username님 안녕하세요를 찍고 싶어


**![](https://lh3.googleusercontent.com/gT1RiQHuRuwi4pglar6Swsd6clnJsX22vCCWamfnPdKCq2xSvDgRc3eKpfetLhCBr3JltAMsRFvpvxzQj-8iwGg2CVASMamQWKjorghmKmQFreI0vUo7WLaffL6-XPYoOcjxVUhM)**
### 컨텍스트 API를 사용하지 않으면 속성값(pros)로 전달
**[App.js]**
```js
import React from 'react';

class App extends React.Component {
  render() {
    return (
      <div>
        <div>상단 메뉴</div>
        <Profile username="홍길동"/>
        <div>하단 메뉴</div>
      </div>
    );
  }
}

function Profile({username}) {
  return (
    <div>
      <Greeting username={username}/>
    </div>
  );
}

function Greeting({username}) {
  return (
    <p>{`${username}님 안녕하세요.`}</p>

  );
}

export default App;

```

### 컨텍스트 API를 사용

ContextAPI 상위 컴포넌트로 직접 전달

**[App.js]**
```js
import React from 'react';

//정의하고
//'unknown'은 UserContext의 기본값이 됨
const  UserContext = React.createContext('unknown');

class App extends React.Component {
  render() {
    return (
        <div>
          {/* 데이터를 제공해주는 쪽에서 provider라는 것을 지정 */}
          {/* 묶어주고 */}
          {/* 기본값이 UserContext.Provider가 정의되지 않으면 <Consumer>에서 사용하는 값
              그냥             
            <div>상단 메뉴</div>
            <Profile/>
            <div>하단 메뉴</div>
            이렇게만 되어있을대
          */}
            <div>상단 메뉴</div>
            <Profile/>
            <div>하단 메뉴</div>
        </div>
    );
  }
}

function Profile() {
  return (
    
    <Greeting />
  );
}

function Greeting() {
  return (
    // 소비자
    // Consumer로 쓴다.
    // 중간에 Profile과 같은 컴포넌트가 값을 전달하는데 개입되지 않아도 됨
    <UserContext.Consumer>
      {
        username => <p>{`${username}님 안녕하세요.`}</p> 
      } 
    </UserContext.Consumer>
    
  )
}
export default App;

```
중간에 Profile과 같은 컴포넌트가 값을 전달하는데 개입되지 않아도 됨

### 중요한 점은 중간에 위치한 컴포넌트의 shouldComponentUpdate 메소드에서 거짓을 반환해도 Consumer 컴포넌트는 다시 렌더링 된다
why? 중간에 Provider 컴포넌트가 없어도 되어서.
Consumer 컴포넌트는 데이터를 찾기위해 상위로 올라가면서 가장 가까운 Provider 컴포넌트 찾음. 만약 최상위에 도달할때까지 Provider 컴포넌트 찾지 못해도 **기본값 사용**
그래서 **중간 컴포넌트가 없어도 랜더링이 됨**

즉, **중간 컴포넌트의 렌더링 여부에 상관없이 Provider 컴포넌트의 값이 바뀌면 Consumer 컴포넌트가 렌더링을 수행하는 것을 보장**
 
**[App.js]**
```js
import React from 'react';

//정의하고
//'unknown'은 UserContext의 기본값이 됨
const  UserContext = React.createContext('unknown');

class App extends React.Component {
  state = { username: '' };
  onChange = e => {
    const username = e.target.value;
    this.setState({ username });
  };
  render() {
    const { username } = this.state;
    return (
        <div>
          <UserContext.Provider value={this.state.username}>
            <div>상단 메뉴</div>
            <Profile/>
            <div>하단 메뉴</div>
          </UserContext.Provider>
          <input type="text" value={username} onChange={this.onChange} />
        </div>
    );
  }
}

// 생명주기 메소드 쓰려면 Class g형
// LifeCycle 형, state 변수 사용하려면 Class형으로 바꿔야함
class Profile extends React.Component {
  // 얘가 false를 반환해도 호출이 된다.
  shouldComponentUpdate() {
    return false;
  }
  render() {
    console.log("Profile's render() called");
    return <div><Greeting /></div>;
  };
}

function Greeting() {
  console.log("Greeting's render() called");

  return (

    <UserContext.Consumer>
      {
        username => <p>{`${username}님 안녕하세요.`}</p> 
      } 
    </UserContext.Consumer>
    
  )
}
export default App;
```

### 여러 콘테스트를 중첩해서 사용하기
p150
{ theme => (	// 어떤 객체를 가져오고 그 값을 사용하는 구문

**[App.js]**
```js
import React from 'react';

const UserContext = React.createContext('unknown');
const ThemeContext = React.createContext('dark');

class App extends React.Component {
  state = { username: '' };
  onChange = e => {
    const username = e.target.value;
    this.setState({ username });
  };
  render() {
    const { username } = this.state;
    return (
      <div>
        <ThemeContext.Provider value="light">
          <UserContext.Provider value={username}>
            <div>상단 메뉴</div>
            <Profile />
            <div>하단 메뉴</div>
          </UserContext.Provider>
        </ThemeContext.Provider>
        <input type="text" value={username} onChange={this.onChange} />        
      </div>
    );
  }
}

class Profile extends React.Component {
  shouldComponentUpdate() {
    return false;
  }
  render() {
    console.log("Profile's render() called");
    return <div><Greeting /></div>;
  }
}

function Greeting() {
  console.log("Greeting() called");
  return (
    <ThemeContext.Consumer>
      { theme => (
        <UserContext.Consumer>
          { 
            username => (
              <p style={{ color: theme === 'dark' ? 'gray' : 'green' }}>{`${username}님 안녕하세요.`}</p>
            ) 
          }
        </UserContext.Consumer>
      ) }
    </ThemeContext.Consumer>
  );
}

export default App;
```

대빵 복잡한 구조 이런걸 해결하기 위해 나온게 **리덕스** 등이 있음
ref : 내가 직접 돔 요소를 핸들링할 때 사용
그래서 createRef() 하고 해당하는 Dom element에다가 해당하는 속성으로 달아줌.
그럼 여기에 나온 div를 this.divRef 이렇게 하면 직접 핸들링할 수 있음(ex. this.divRef.current.getBoundingClientRext())


