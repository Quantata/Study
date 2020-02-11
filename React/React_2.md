
# React
- Facebook에서 만든 **UI 라이브러리**
- JavaScript 기존에 라이브러리 얼마 없었음. 
- UI에 특화되어 있음(개발자가 할게 많아짐)

## Create-React-App
- 리액트의 진입 장벽을 낮추기 위해 제공


## 환경설정
- `C:\react` 생성
- 그 다음 `Visual Code`실행
	- `C:\react`를 open Folder로 하기
- cmd창에서
  ``` 
  C:\react>npm install -g create-react-app
   ```
- 이후
	```
	C:\react>create-react-app hello-react
	```
	- javaScript 기반으로 react-app 이름이 hello-react(작업 디렉토리)
	- create-react-app 이용하면 디렉토리 설정안해도 됨

## 시작
21p
### 주요 명령어(이렇게 시작해라)
- npm start
	- 개발 환경 실행
	- 개발 서버로 실행
	> **bootstrap**
	> 뭔가를 하려고 할때 기본이 되는 요소들, 환경들을 잡아주는 작업을 bootstrap한다 함. (마중물)
	> 파일 생성, 디렉토리 생성 등을 하는 것
- npm run build
	- javascript 빌드
	- 원래 javascript는 브라우저같은데에서는 로딩되서 실행되는 것. react에서는 javascript 버전이 있는데 이 버전을 상위버전 썼을때 실행환경에서 안먹힐 수 있음. 이걸 바꿔주는 프로그램(trans compiler, ex) 바벨) 이 있는데 build라는 명령어로 이걸 실행해줌
- npm test
- npm run eject
	- eject는 분리. 파일이 크면 파일을 다 내려받아서 로딩하는데 시간 많이 걸림. 필요한만큼 나누는 작업

### Create-React-app을 사용하면 좋은 점
- 디렉토리 구조도 만들어주고 react resource도 다 들어가있음. 개발에 들어가기 좋은 sample code(src디렉토리 밑)도 만들어줌

#### npm start
[npm start 명령어 실행]
**![](https://lh4.googleusercontent.com/Fm3uZrY8ISy9hckrA3G2x1hKtqaz2-53e41z6FpfvMn69o43W6o1yLIzSDA08_Eu6hfP21agjBRzplt5PKLgY50R9fhWLQ3mh7M1dq-jm80iy4mAv7Y9riY26rWB4_RNwtCHs3Yv)**

[chrome]
**![](https://lh6.googleusercontent.com/YhI-dOTzafxqeABaRTmo3tdiIW2ky8uAih9jWFGskAeXO2R2a-t1kiY-_Evu1cv0ORS8k8E0us9s9NReCeFwtcg40WQTiwUtCRx5e-tSo-fmf9lIcjXm0dm-zUu3RCzAByzQAfM1)**

[visual-code]
**![](https://lh5.googleusercontent.com/U0RdIeTDUlPcfw_mVpK77rvHXJN96H8aBM4fXMnLM3PcvWIAxR0l-l39oe3Wj-fUhwR473YNtKIkfFWE6Rtd7aHNfBOohsu0DaHbW1EjjWXo5Fh6doRTL1dFGglzoj5gUOyElrFq)**

jsx 기반으로 표기법을 이용해서 만들어진 코드 
- html코드 안에 {} 같은 것도 보임 이런걸 `jsx`기반으로 만들어진 코드라고 함
**![](https://lh3.googleusercontent.com/O5w0RXbI16iHTKjJHUCjYcntDjqVz4ZTMVLsg_NdYPPkbRI-7pJm-HwpyQu_qvV796Q5EhRz16cXmeqbXGI5QoIDjQwPIPRGnLQALnesaUfFbdqY7uNLhCyZ7b4793Vsu2vlfVrV)**

화면에 보여지기 위한 어떤 값이 있는데 값이 바뀌었을때 보여주는게 상태가 바뀜. 이런걸 쉽게 바꾸어주는 기능을 하는 것이 `React`

### React 기능
- 가상돔 : 전체 문서에서 변경된 부분만 적용해서 변경.
	- 문서 전체를 바꾸는 것보다 빠르고 효율적으로 바꿔줌

## React 개발환경 직접 구축 -> 외부 패키지 사용하지 않고 리액트 웹페이지 제작 
p3

### #1 작업 디렉토리 생성
- [다른이름으로 저장] 경로는 `C:\react\hello-world`

### #2 리액트 라이브러리 다운로드
1.  [https://unpkg.com/react@16.12.0/umd/react.development.js](https://unpkg.com/react@16.12.0/umd/react.development.js)
2. [https://unpkg.com/react@16.12.0/umd/react.production.min.js](https://unpkg.com/react@16.12.0/umd/react.production.min.js)
3. [https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js](https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js)
4. [https://unpkg.com/react-dom@16.12.0/umd/react-dom.production.min.js](https://unpkg.com/react-dom@16.12.0/umd/react-dom.production.min.js)


이 과정에서 불편함을 느껴야 `Create-React-app`에 대해 편함을 느낌

-   **development** ⇒ 개발 환경에서 사용하는 파일 → 에러 메시지 확인이 가능
    
-  **production** ⇒ 실행(배포) 환경에서 사용하는 파일
    
-  **react** ⇒ 플랫폼 구분 없이 공통으로 사용되는 파일 (리액트 코어)
    
-  **react-dom** ⇒ 웹 환경에서 사용되는 파일

결과
**![](https://lh5.googleusercontent.com/KusU6FmmZTg1bIqqkJcRYz2o37bxd5DfYykE-OCIhqufLYl-04zvbW7CzLo6j9XayBmJJ61LbicGPc1Glu_SS70DM8jICwIwbMkiRRJuIRTokYwfWUJWpB8RG_fOi0FAKptrkxXg)**

### #3 `c:\react\hello-world\sample1.html`, `c:\react\hello-world\sample1.js` 생성
**![](https://lh3.googleusercontent.com/em1hfUjr6l3iXyBamAu9DG7LiNa_P6S0N5xSRhuDM_38U682T8Pg26VUYuYFdZL7bwoqC_chA3EUX6GwIwTtScqNKGUI9p1AwXaFZxGBWhtsgzTXwz08lY9JDxfPxWMgFNAN2Bhw)**

### #4 아래 화면과 같은 출력을 제공하는 sample1.html 작성
**![](https://lh6.googleusercontent.com/fbCUx-XY2CUG8iy7DcOaV7j4VCCuLN-wzl-RfHCcJo1qvz11XdDaJl_vu2oHg07MuROwRjCg9N6DXH1NZNRs7OaUhaboEHK1lqVmuFUCHSymLlWJnNcIV0Q6T3quolrBdEpo1gR1)**
- "좋아요" 버튼 누르면 "좋아요 취소"로 변경
p5_code1-1
```html
<!-- PS 코드1-1 -->
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 눌러주세요</h2>
        <div id="react-root"></div>
        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script src="sample1.js"></script>
    </body>
</html>
```
#### #4-1 리액트를 사용하지 않고 처리
- 버튼 하나 넣고 서버 실행
``` npx http-server```
- chrome에서 실행
[http://localhost:8080/hello-world/sample1.html](http://localhost:8080/hello-world/sample1.html)
```html
<!-- PS 코드1-1 -->
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 눌러주세요</h2>
        <div id="react-root"></div>
            <button>좋아요</button>
        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script src="sample1.js"></script>
    </body>
</html>
```
- React 안쓰고 jquery로 구현
	- jQuery 다운로드
		- [https://developers.google.com/speed/libraries#jquery](https://developers.google.com/speed/libraries#jquery)
```javascript
<!-- PS 코드1-1 -->
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 눌러주세요</h2>
        <div id="react-root"></div>
            <button>좋아요</button>
<!--         
        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script src="sample1.js"></script> -->
        <!-- jQuery 기반으로 구현 -->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <script>
            $(function() {
                $('button').click(function() {
                    let x = $(this).text();
                    if(x === '좋아요')
                        $(this).text('좋아요 취소');
                    else
                        $(this).text('좋아요');
                });
            });
            
        </script>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/bmNXIjhMWvj3uJKzlXawlN3GH4uNc3Z4ZxZMVeRJp30Jrf81uhFM2op-jurYeToj18WhIu06ELHrLuBiBfR8WfEzfimmnn7P8uqoyqb2ZtAYtNXHtEfroOCY1MZUyZBNf0mxQkj9)**
**![](https://lh5.googleusercontent.com/zJwz-1vKLvozyLMPZzC214vLKeJss2IpsrviPPmxZw7dxOqVXxWdgw-eU_9vACFo04aCVjREFKj_71yj-nYNjE257_gqqoNks0OnyjdW-_lOTeh8GySVPMttF-2NNGVC8xcLj1yg)**
- liked 변수로 같은 기능 구현하기
	- `$('button').trigger('click')` 은 화면이 다 로딩된 후 button 태그를 클릭하게 해줌.
	- 상태와 화면이 다른 것을 `render`라고 함.(지금 내가좋아요인데 liked = false)
	- 이런걸 맞춰주기 위해 trigger 사용
```javascript
<!-- PS 코드1-1 -->
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 눌러주세요</h2>
        <div id="react-root"></div>
            <button></button>
<!--         
        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script src="sample1.js"></script> -->
        <!-- jQuery 기반으로 구현 -->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <script>
            $(function() {
                // liked 변수의 값이 false면 좋아요 취소
                //                   true 이면 좋아요
                // 버튼을 클릭하면 liked 변수의 값은 토글
                let liked = false;
                $('button').click(function() {
                    liked = !liked;

                    if(liked){
                        $(this).text('좋아요');
                    }
                    else{
                        $(this).text('좋아요 취소');
                    }
                });
                // 저문서가 열리면 클릭하도록 함.
                $('button').trigger('click');
            });
            
        </script>
    </body>
</html>
```

#### #4-2 React 이용해서 사용
- LikeButton이란 클래스 만듦
	- liked라는 상태 갖고 있음
	- state (상태변수) 가 liked를 갖고 있고 이 상태변수를 바꿔주는 것이 render() 함수
	- 데이터와 데이터 처리를 하나로 묶어 놓는 것이 `컴포넌트` 여기에서는 class를 이용해서 해당 컴포넌트 이용
	- LikeButton이 컴포넌트로 사용하려고 하면 정의해놓은 것을 받아와서 바꿔야함. (상속) 정의는 `React.Component`에 있음. React에서 제공하는 Component 클래스에 정의되어 있음. 
	- `constructor` 는 생성자
		- `React.createElement(likeButton)` 코드로 버튼이 실행되면 버튼이 최초로 실행됨
		- `super(props)` extend 한 React.Component를 초기화 시켜 놓음. 그래놓고 `state`변수 정의
		- 변수
			- property : 부모로 부터 전달받은 값
			- state : 자기 자신이 갖고 있는 값
		- Likebutton클래스는 liked라는 값을 갖고 있음. default로 false값을 가지도록 되어 있음
	- `render()`사용자 화면에 보여주는 함수
		- `React.createElement` 는 React에서 태그(요소)를 만들어 주는 것
			- 첫번째 파라미터는 그 element : 'button'
			- 두번째는 7p에 나와있음.  : `객체 인자` 들어갈 수 있음
				- 컴포넌트가 click을 당하면 해당 기능을 수행해라
				- `onClike`은 `createElement`의 두번째인자의 `메소드`
				- 상태변수 바꾸어 줄테는 `setState()` 함수 사용해줘야함
				- `onClick`은 객체의 속성이고 onClick의 끝의 소괄호까지는 객체의 값. `this.setState`부터 `})` 까지 `함수 본문`
				- 
			- 세번째(`text`)는 버튼이라는 element에 들어갈 하위 element. (좋아요, 좋아요 취소가 들어갈 것) 
			
	- 해당하는 문서에서 `#react-root`(아이디가 react-root)인거 갖고 와라. 해당하는 div id가 react-root에 LikeButton이라는 것을 집어 넣어라
	- 화면에 보여줄때는 `ReactDOM`이 필요
		-` React.createElement()`를 통해 태그를 만들어줌. 해당 함수의 첫번째는 `태그`가 되거나 `리액트 컴포넌트`(like 여기서 LikeButton). 이건 필수.
		- 두번째와 세번째는 선택임
```javascript
<!-- PS 코드1-1 -->
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 눌러주세요</h2>
        <div id="react-root"></div>
        
        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <!-- <script src="sample1.js"></script> -->
        
        <script>
            //p6 코드1-2
            //LikeButton이란 클래스 만듦
            class LikeButton extends React.Component {
                constructor(props) {
                    super(props);
                    this.state = {liked: false };
                }
                render() {
                    const text = this.state.liked ? '좋아요 취소' : '좋아요';
                    return React.createElement (
                        'button',
                        // { onClick: () => this.setState({ liked : true}) },   // 이거하면 좋아요-> 취소 한번만 됨
                        { onClick: () => this.setState({ liked : !this.state.liked }) },
                        text,
                    );
                }
            }
            const domContainer = document.querySelector('#react-root');
            ReactDOM.render(React.createElement(LikeButton), domContainer);
        </script>
    </body>
</html>
```
우리는 이제 값을 바꾸려고 했을때 `상태 변수 값`만 바꿔주면 상태변수에 따라서 사용자 화면에 `좋아요 변수`가 달라지는 것을 볼 수 있음.
옛날에는 값을 보여주는 부분과 바꿔주는 부분이 달랐음. 오류가 나타날 수 있고 이를 방지하기 위한 코드를 더 넣었어야 하는데 `React`는 상태값만 관리해서 더 좋음. 

### #5 http-server를 실행해서 확인

### #6 여러개의 돔 요소를 렌더링
**![](https://lh4.googleusercontent.com/j6n4pIDUfZveQsUOVrPXenD283NWLB4SkVQv6bqP__YqWeFhPgYFSltVetzd3nm4l1YN7pQD8V7r3FvpqfH7zJkBGRWzizDY6skQE6YYp3nwKwRfA8vEXCU87GWYs6uZ7frX9Z0f)		![](https://lh6.googleusercontent.com/-Id2LfXXbp8VeP4vW4l_aGEKA-UVZfU5v4t6NQnN3LkcpbLFSV8yY9jgrtEiCiqCqbJeumJ4QYR74K0W_piR38HGC2Q-1fYVxSW_I9L4oW9xIuiZtC3b-JZHzmTUwx6sN9cyesz2)**
- 이거 jQuery로 만들려면 \<div>에 버튼 세개 올리고 각각에 id 올리고 갱신해줘야함

#### #6-1 '4-1'코드를 응용해서 jQuery를 이용한 구현
```javaScript
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 클릭해 주세요</h2>
        <div id="react-root">
            <button id="btn1">좋아요</button>
            <button id="btn2">좋아요</button>
            <button id="btn3">좋아요</button>
        </div>

        <!-- jQuery 기반으로 구현 -->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <script>
            $(function() {
                //  liked 변수의 값이 false 이면 좋아요 취소
                //                   true 이면 좋아요 
                //  버튼을 클릭하면 liked 변수의 값은 토글
                let liked1 = false;
                let liked2 = false;
                let liked3 = false;
                $('button#btn1').click(function() {
                    liked1 = !liked1;
                    if (liked1) $(this).text('좋아요');
                    else $(this).text('좋아요 취소');
                });
                $('button#btn2').click(function() {
                    liked2 = !liked2;
                    if (liked2) $(this).text('좋아요');
                    else $(this).text('좋아요 취소');
                });
                $('button#btn3').click(function() {
                    liked3 = !liked3;
                    if (liked3) $(this).text('좋아요');
                    else $(this).text('좋아요 취소');
                });
                    
                $('button#btn1').trigger('click');
                $('button#btn2').trigger('click');
                $('button#btn3').trigger('click');
            });  
        </script>
    </body>
</html>
```
**![](https://lh3.googleusercontent.com/k5HKGgvkEyUMk5-Mwx2CIiMkAaK8OcEylEAO6HFG1Rn1pUL11KQmKjYeHJH66e2Flvpz8U9KEN53Rz7WaWOoJypFHFe1d38KvzCxPxM83L7bzA2YTBPoUCO7l38o3RF-jXO1TNkt)**

#### #6-2 React를 이용한 구현
- 기능은 이미 Likebutton클래스에 있음. 버튼 3개만 만들어주면 됨.
```javascript
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 클릭해 주세요</h2>
        <div id="react-root1"></div>
        <div id="react-root2"></div>
        <div id="react-root3"></div>

        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script>
            class LikeButton extends React.Component {
                constructor(props) {
                    super(props);
                    this.state = { liked: false };
                }
                render() {
                    const text = this.state.liked ? '좋아요 취소' : '좋아요';
                    return React.createElement(
                        'button',
                        { onClick: () => { 
                            console.log(this.state.liked); 
                            this.setState({ liked: !this.state.liked }); 
                        } },
                        text,
                    );
                }
            }
            ReactDOM.render(React.createElement(LikeButton), document.querySelector('#react-root1'));
            ReactDOM.render(React.createElement(LikeButton), document.querySelector('#react-root2'));
            ReactDOM.render(React.createElement(LikeButton), document.querySelector('#react-root3'));
        </script>
    </body>
</html>
```

## 바벨(babel) 사용
p9
- 성경에 나오는 바벨
- 응용들이 표준에 맞도록 바꿔주도록 한다면은 표준에 맞는 실행환경만 있으면 됨
- 어떤 표준 javacscript 포맷이 있으면 뭐가지고 표현하기 어려운 것들을 표준에 맞도록 바꿔줌
- 현재 사용하고 있는 js 버전이 너무 낮아. 그래서 버전이 높은 걸로 만들었을때 낮은 버전에서도 돌 수 있도록 해주는게 바벨
- 런타임(실행환경)에 맞도록 바꿔주는 것을 **바벨**이라고 함
**![](https://lh3.googleusercontent.com/E7SbY3W-QIOcmGpScWIZzXeA_xL5I0DE3pYXAlRPNGqSDm3cIxnZUyQYAP8Z1aaVTuamVCYu0UWNeqbVFyXprt0K1nwIXCQ9BxdawlpLm7fABIzYg4tgRe-5Hi-HqSlOK1nftWgX)**
C나 C++ 코드가 binary로 바꿔지는 것을 Compile한다고 함.
소스코드는 JavaScript. 실행환경 코드도 JavaScript 이때는 형태를 바꾸는 컴파일이다라고 함.
소스코드 JavaScript 높은 버전 ex)ES6, ES7 같은 것들을 실행환경의 ES5와 같은 것에서 돌아갈 수 있도록 함.
이때 불필요한거 제거할 수 있음. 
- 공백, 주석, 식별자들(아주 긴 이름의 함수명, 변수명 등)

이런 형태로 바꿔줄때 **바벨**을 이용해서 바꿔줌

React를 가지고 소스를 만드는데 그때 JSX문법 만들음. 이때 JSX를 사용할 수 있는 Plugin(Preset)이라고 함.

**바벨** - trans compiler이라고도 함.

바벨을 이용해서 좀 더 복잡한 형태의 화면을 만들어 볼 것이야
### #1 증가, 감소 버튼으로 count 상태값을 변경하는 코드를 작성
**![](https://lh5.googleusercontent.com/ZmUWkJxQPhyFe80IFngV5k7VypFCWo-FNyoFBma75pZMCmN9yIzDLKonXZN8pTs7qcqtYx9ezGcb8OpfKqGd-4z4LZXgKFf2OTI06BjtUam49fWmkqEFVXAJ8x-ieYn6w7njyy2n)![](https://lh5.googleusercontent.com/6eDOVPK3AqXbDHJp8PGqA5T8TE9Mh0IdPvYOYWSC8D3dUJnaNfePk0iX46PQcxP7MSOXrMIRnuFWQSVcMA2XgzVZQgElguiDzLgEg0BD67bvwUjOX4Thl3FwMd3pftgqNKDqeN2c)**
9p에 있는 내용
- [sample3.html] 생성
	- 초기값
```javascript
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 클릭해 주세요</h2>
        <div id="react-root"></div>

        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script>

        </script>
    </body>
</html>
```

- 결과 코드
```javascript
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 클릭해 주세요</h2>
        <div id="react-root"></div>

        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <script>
            class LikeButton extends React.Component {
                constructor(props) {
                    super(props);
                    this.state = { liked: false };
                }
                render() {
                    const text = this.state.liked ? '좋아요 취소' : '좋아요';
                    return React.createElement(
                        'button', 
                        { onClick: () => this.setState({ liked: !this.state.liked }) },
                        text,
                    );
                }
            }
            // P9 코드1-6 참조
            class Container extends React.Component {
                constructor(props) {
                    super(props);
                    this.state = { count: 0 };
                }
                render() {
                    return React.createElement(
                        'div',
                        null, 
                        React.createElement(LikeButton), 
                        React.createElement(
                            'div',
                            { style: { marginTop: 20 } }, 
                            React.createElement('span', null, '현재 카운트: '),
                            React.createElement('span', null, this.state.count), 
                            React.createElement(
                                'button', 
                                { onClick: () => this.setState({ count: this.state.count + 1 })},
                                '증가',
                            ),
                            React.createElement(
                                'button', 
                                { onClick: () => this.setState({ count: this.state.count -1 })},
                                '감소',
                            ),
                        ),
                    );
                }
            }

            ReactDOM.render(
                React.createElement(Container), 
                document.querySelector('#react-root')
            );
        </script>
    </body>
</html>
```

위 코드 html 버전으로
```html
<div id="react-root">
	<H1>좋아요 버큰을 클릭해 주세요.</H1>
	<div>
		<button …> … </button> ⇐ LikeButton
		<div>
			<span>현재 카운트: </span>
			<span>0</span>
			<button>증가</button>
			<button>감수</button>
		</div>
	</div> ⇐ Container
</div>
```
html보다 react로 구현한게 알아보기 어려움.
그래서 html 문법으로 내가 만들어 놓으면 표준코드 형태로 바꾸면 되는거 아닌가??
- React
	- html 태그를 이용해서 화면이 어떻게 돌아갈 것인가 만들어놓으면 React로 자동으로 코드를 변환시켜줌

### #2 jsx 버전으로 변경
#### 초기 설정
- `c:\react\hello-world\sample04.html` 코드 생성
```javascript
<html>
    <body>
        <h2>프로젝트가 마음에 들면 좋아요 버튼을 클릭해 주세요</h2>
        <div id="react-root"></div>

        <script src="react.development.js"></script>
        <script src="react-dom.development.js"></script>
        <!-- 바벨을 이용해서 ./src/sample4.js 파일의 컴파일 결과로 생성
        지금은 같은 디렉토리에 없음. -->
        <script src="sample4.js"></script>
    </body>
</html>
```
- `C:\react\hello-world\src\sample4.js (수정전: #1-2 코드 일부를 이전)`
```javascript
class LikeButton extends React.Component {
    constructor(props) {
        super(props);
        this.state = { liked: false };
    }
    render() {
        const text = this.state.liked ? '좋아요 취소' : '좋아요';
        return React.createElement(
            'button', 
            { onClick: () => this.setState({ liked: !this.state.liked }) },
            text,
        );
    }
}
// P9 코드1-6 참조
class Container extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
    }
    render() {
        return React.createElement(
            'div',
            null, 
            React.createElement(LikeButton), 
            React.createElement(
                'div',
                { style: { marginTop: 20 } }, 
                React.createElement('span', null, '현재 카운트: '),
                React.createElement('span', null, this.state.count), 
                React.createElement(
                    'button', 
                    { onClick: () => this.setState({ count: this.state.count + 1 })},
                    '증가',
                ),
                React.createElement(
                    'button', 
                    { onClick: () => this.setState({ count: this.state.count -1 })},
                    '감소',
                ),
            ),
        );
    }
}

ReactDOM.render(
    React.createElement(Container), 
    document.querySelector('#react-root')
);
```
**![](https://lh3.googleusercontent.com/FIhSHAxqzTMD9Q_2flgiHth5rwN1xG_4C--japXoSn6u87c0G7Go9gOGBuNqHPHjsU9DJ0p3R6ygAGm3kXa7sCuLwp1kj2hZR0oBCo0yRjOBzSoJTuCD1MyJ8a4mDdAyYhoyyYyq)**

#### 작성
P11. 코드 7을 참조
[`./src/sample4.js`]
- render() 함수 안에 내용 삭제
```javascript
class LikeButton extends React.Component {
    constructor(props) {
        super(props);
        this.state = { liked: false };
    }
    render() {
        const text = this.state.liked ? '좋아요 취소' : '좋아요';
        return React.createElement(
            'button', 
            { onClick: () => this.setState({ liked: !this.state.liked }) },
            text,
        );
    }
}
// P9 코드1-6 참조
class Container extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
    }
    render() {
        return (
            <div>
                <LikeButton/>
                <div style={{ marginTop: 20}}>
                    <span>현재 카운트: </span>
                    <span>{this.state.count}</span>
                    <button onClick={() => this.setState({ count: this.state.count + 1})}>증가</button>
                    <button onClick={() => this.setState({ count: this.state.count - 1})}>감소</button>

                </div>
            </div>
        )
    }
}

ReactDOM.render(
    React.createElement(Container), 
    document.querySelector('#react-root')
);
```
이거 그대로 실행하면 브라우저는 실행을 못함.
내가 만들기 좋은 소스코드 만들면 브라우저가 이해할 수 있는걸로 만들어주는게 trans compiler(바벨)
설치해야함

### #2 바벨 패키지 설치하고 자바스크립트를 변환(컴파일)
13p 위에
- cmd(hello-world 디렉토리에서)
	```shell
	C:\react\hello-world>npm install @babel/core @babel/cli @babel/preset-react
	```
`core` : 바벨 기능
`cli` : cmd같은 곳에서 바벨 사용할 수 있도록
`preset` : 변환할때 이 소스가 되는 문법을 이해할때 미리 이해할 수 있도록 미리 만들어 놓은 부분. 우리는 react 문법을 해석할 수 있도록 만들어놓은 babel preset을 만들어 놓음

- cmd
	```
	C:\react\hello-react>npx babel --watch ./src --out-dir ./ --presets @babel/preset-react
	```		
- [http://localhost:8080/hello-world/sample4.html](http://localhost:8080/hello-world/sample4.html) 들어가기

`npx` : npm 레지스트리의 패키지 사용 경험을 파악하기 위한 도구입니다  
  
현재 들어있는 ./src디렉토리에 변화가 생기면 컴파일을 해라. 컴파일 결과는 현재 디렉토리(hello-world)에 옮겨라. 이 과정에서 babel preset react를 이용해라
**![](https://lh5.googleusercontent.com/LscwHQ7NQAUv6NbdYgmzqQmzVZCCWBIxL2spPeqDbJe9yxC5EZLvk6aeeWHZBXcm_nRjG5x-yARDzkrhC4-I8sAoQR-_iXnJULr0Vh1Szb5YarVEWU1ToNSYCHVWZcR3rSbyPeJA)**
-> 두개의 sample4.js 내용을 비교해보면 babel이 어떤 역할 하는지 알 수 있음. 

## 웹팩(Webpack)
14p

css, javascript 등 묶어주는 것. 효율적으로 리소스를 전달하기 위해서
내가 원하는 시점에  원하는 파일 불러올 수 있음

16p
내가 필요로하는 것들을 뭉쳐서 제어할 수 있음 그것이 **웹팩**
이러기 위해서는 **모듈**이라는 개념 필요
 
**모듈** - 파일 단위로 묶을 수 있는 기능. ES6부터 **언어차원**으로 제공
ES6 이전에는 모듈을 쓰고 싶다는 갈망이 있음. 이런 모듈 기능을 제공해주는 라이브러리가 있는데 그게 `common.js`

**웹팩**은 이런 **모듈을 기반**으로 묶어줌
소스를 분석해서 like button 구현하는 js 파일과 container 구현하는 js파일과 묶어주는 것


>**cache**
> 서비스하는 입장에서는 좋음
> 개발을 할때는 수시로 내용을 바꿈. 근데 안바뀌어 이때 해당하는 홈페이지가 캐싱하지 않도록 할 수 있음 **npx http-server -c -1**
> 근데 이건 html 문서에 대해서만 **cache control**할 수 있음
> 왜냐? http가 구려서 뒤에가서는 잘 안쓸거임


15p
**ESM** : ES6의 **모듈 시스템**
- ESM 문법 익히기

**`[file1.js]`**
- 하나의 js 파일에 function이 두개 있고 variable이 2개 있음
```javascript
// file1.js
export default function func1() { … }
export function func2() { … }
export const variable1 = 123;
export let variable2 = 'hello';
```
.js 파일에서 갖고 있는 값이나 함수들을 다른 파일에서 쓸 수 있도록 내보내고 가져올 수 있는 것을 **모듈**이라고 함
외부에서 내 것들을 사용할 수 있도록 하기 위해서는 **export** 사용

**export default**는 하나만 사용할 수 있음

**`[file2.js]`**
```javascript
// file2.js
import myFunc1, { func2, variable1, variable2 } from './file1.js';
```
 가져온다 from './file1.js'로 부터
 file1.js 이 제공하고 있는 func2, variable1, variable2을 사용하겠다.
 그리고 **myFunc1**은 default이기 때문에 중괄호 사용없이 자동으로 사용할 수 있고 func1이라는 것을 myFunc1이라는 것으로 자동으로 사용할 수 있음

**`[file3.js]`**
```javascript
// file3.js
import { func2 as myFunc2 } from './file1.js';
```
원래는 file3.js 처럼 `원래 이름 as 새이름` 으로 해야하는데 default라 myFunc1로 사용할 수 있음

**이제 웹팩 사용할 것임**

### #1 작업디렉토리 생성
- 작업 디렉토리 생성
	```shell
	C:\react>mkdir webpack-test
	```
- npm init : 노드 기반 프로젝트 만들때 프로젝트 템플릿 만들어주는 것
	```shell
	C:\react\webpack-test>npm init -y
	```
- webpack-test 아래에 src 폴더 생성
	```shell
	C:\react\webpack-test>mkdir src
	```
- webpack-test 아래에 `index.html` 생성
- webpack-test/src에 `Button.js`, `index.js` 생성
**![](https://lh3.googleusercontent.com/qjdrNJ23wcFdwLfTfuXo5odO7KAdAgmSMyW6D9CIEJmT5oeV4RxRZdivzJIiINeiGkOcQDBDIBl7BmAwhesu3WYVVeTSLIqOLFwpXInmmNeDgW_Hs77S-3rBiJUpEuyJnzwH7YgS)**

### #2 외부 패키지를 설치
```shell
C:\react\webpack-test>npm install webpack webpack-cli react react-dom
```
 
### #3 코드 작성
#### #3-1 `C:\react\webpack-test\index.html`
```html
<html>
    <body>
        <h2>좋아요 버튼 클릭해 주세요</h2>
        <div id="react-root"></div>
        <!-- dist/main.js : 이건 웹팩을 통해 자바스크립트 파일을 결합하면 생성 --> 
        <script src="dist/main.js"></script>

    </body>
</html>
```
#### #3-2 `C:\react\webpack-test\src\index.js`
```javascript
// 중괄호를 안쓴거 보면 default 갖고 온거임
import React from 'react';
import ReactDOM, { render } from 'react-dom'
import Button from './Button.js';

 //함수형 컴포넌트, 생성자가 없고 state 변수가 없음
function Container() { 
    return React.createElement(
      'div',
      null,
      React.createElement('p', null, '버튼을 클릭하세요'),
      React.createElement(Button, {label: '좋아요'}),
      React.createElement(Button, {label: '싫어요'}),
      /*
      <div>
        <p>버튼을 눌러주세요.</p>
        <Button> </Button>
        <Button> </Button>
      </div>
      */
            
    );
}

ReactDOM.render(
    React.createElement(Container),
    document.querySelector('#react-root')
);
```
#### #3-3 `C:\react\webpack-test\src\Button.js`
```javascript
import React from 'react';

function Button(props){
    return React.createElement('button', null, props.label);

}

export default Button;
```

`index.js` 보면 React와 ReactDOM이 있고, div로 싸여있는 React element를 return. 얘가 호출되는 곳에서. createElement에 하는 것
Button이 호출되면 'button'이라는 element가 만들어져라(`Button.js`)

`props` = 속성 = 부모 컴포넌트가 전달하는 값
`state` = 상태 = 자기(해당 컴포넌트)가 보유하고 있는 값

`props` 는 부모 컴포넌트가 자식컴포넌트에 값을 전달해주면
해당 컴포넌트를 호출해주는 곳에서 객체 형태로 전달해주고 받는 곳(자식 컴포넌트)에서는 `props.[값]` 을 통해 사용

아까는 Button과 Container 한 파일에 넣었음. 
코드도 먼저 like 버튼을 만드는 등 의존성이 있었음
코드의 중복이나 dependency를 해결해주는 것 리소스들을 하나로 뭉쳐서 효율적으로 사용할 수 있도록 하는게 **webpack**

### #4 웹팩을 이용해서 두개의 자바스크립트 파일을 하나로 결합
```shell
C:\react\webpack-test>npx webpack
```
- dist 폴더와 main.js 생성됨
**![](https://lh3.googleusercontent.com/_lJ4u4ez8pLhiIy5pKBrxdS6ItKmELMIEHJKVUUMy_3G_YoAHJI2WnwkpQ8mQVA4wcC5cwoPPXwmDg62Pjbosnyjdm1zVgMygWuIlNb9a4qafH2dW8BsOXTbyPu9HrabMzVoHoAw)**
우리는 브라우저에서 엑세스할 파일은 index.html 파일 하나밖에 없음. 엑세스 해보자!
[http://localhost:8080/webpack-test/index.html](http://localhost:8080/webpack-test/index.html) - 클릭
	
	**![](https://lh5.googleusercontent.com/PI4RK7uJqSNBd-a2ClLuB-U1Nnozyuu_ALAyZmxZIwR38-ewyJdm6ZseICC0Vmw97qUaNNEPMaViMbKN17vu1g1QD8u6ry_LTbTS4sNqc0X5-ABI9nr9ZiSwXTBQ1CvXXaq_7Ws1)**
main.js 자세히 보면 react.js, reactDOM, 내가 만든 button 컴포넌트 있음

jsx문법쓰려면 바벨쓰고 웹팩으로 돌려야함. 근데 create-react-app 이용하면 이런거 전혀 신경 안써도 쉽게 쓸 수 있음

# Create-react-app
## Create-react-app 으로 시작하기
18p
- React로 웹 애플리케이션을 만들기 위한 환경을 제공
- 바벨과 웹팩도 포함
- 테스트도 용이함
- HMR(Hot-Module-Replacement)
- ES6+ 문법, CSS 후처리 등을 제공

>**HMR**
>코드 수정했을때 바벨은 watch해서 특정 디렉토리 보고 있다가 변경되면 자동으로 컴파일 해줌. 
>웹팩은 내가 새로 묶어줘야함
>근데 변경될때마다 묶어주고 새로 올리고 하는거 번거로움. 이런거 자동으로 해주는게 **HMR**
### #1 개발 환경 설정
- 모듈은 이미 깔음
- cmd
	```shell
	C:\react>npx create-react-app cra-test
	```
	이거 깔면 react를 사용할 수 있도록 bootstrap 해줌. 디렉토리 구조 만들어주고 기본적인 파일들 만들어 줌.
	```shell
	C:\react>cd cra-test
	```
### #2 개발 서버 실행
``` shell
C:\react\cra-test>npm start
```
브라우저가 자동으로 http://localhost:3000/ 접속
**![](https://lh3.googleusercontent.com/sOSR_ol-_DN4ojClsrnta_KYvpBEIWzJFqKNZlqYnMHBRmEmDfK9lXrE2BPYFOBWOBdssT7UEZJSIHb-ye1EF0wOT9wz_GaRfjsC5g-dq5oev5zMe2ZWbOc4Y9nfaZIMHWX8OB2x)**
**![](https://lh4.googleusercontent.com/-GlSH5wiZ8mttF0LCIa26cyIrMtdSjGrRyMwZ4Yg3orW3E6FNFHqLKbO1E-TUKGIxRxJtKZ_hFNTjfXcjwOkTeobvPExV5ZcNuSQE919FHkT2POFwrzal40lqaBV-fDXrXZ7dImJ)**
- `cra-test/src` 의 `App.js` 열어서 
**![](https://lh6.googleusercontent.com/lTQvr-1fhIe0JS9a0OqH3KEGA1QnVDlFVViljDFsVRiDybXcp0ZuoOPJ1m6GiSWFDhr-5UrbH3oUOBgd0dPmTVT6m9YrrE5ujlP5pzXaDy1kpgoXNWDGqOM19OMUnyvXeFCd9F7Q)**
이거 그냥 저장하면 바로 브라우저에서 내용이 바뀜. Reload하지 않아도.
**![](https://lh4.googleusercontent.com/WDba-nJFWqY6bmUVfEQjykgomBf2r2m9SwcS2Q_NeCwfAX2n2WAJLGd2kAkPttfmsBa-iP3IeINlx4T4RlQB1jkwEqyqgP2O_T6daCy939tcwwMbu7s_zntUqZvIxbIMWHBwU8yM)**
- `cra-test\src\App.js`
**![](https://lh4.googleusercontent.com/DzWCS74rZnywXKhS4ezzD-7E6oOUohO6cTMto08cjpWouX2tM3pJ7zneh71Hl-bQzu3lHylaejE6sjBWFZJwdMJaRfh1fu1gjvK8kXMB9x3TrZ15hf66gvyynxaDPLZFxxt-rT4l)**
그리고 **자바스크립트 파일**이나 **CSS파일**은 link나 script 태그 이용해서 index.html에 포함시킬 수 있지만, 특별한 이유가 없다면 **src폴더 밑**에서 **import** 키워드를 이용해서 포함시키는게 좋음. 왜?
	1.	자동으로 압축
	2.	캐싱효과
		- 이미지파일이나 폰트 파일의 경우 **웹팩**에서 **해시값**을 이용해서 url을 생성해주기 때문에 파일의 내용이 변경되지 않으면 **브라우저 캐싱효과**볼 수 있음

### #3 빌드 해보기
```bash
C:\react\cra-test>npm run build
```
	
**![](https://lh4.googleusercontent.com/SybxFFk5P3pnoDrjUJ2gIikTFe6hDXd55uqiYTlx-7SZSitbwCH7mx8E6m9f5NAERGLRKPBE7oF1HygbJ9pf4nXmXu0B-h_oNvlLp_r6l3-1BhQ6sLUa35EjUumWdJcyGEVd6trT)**
빌드하면 다음과 같은 파일 나옴

`\<link href=".....css"> 이렇게 말고 import from "...css" 이렇게 사용`
	자바스크립트 파일에서 import 키워드를 이용해서 가져온 CSS 파일 -> **build/static/css/main.{해시값}.chunk.css 파일**에 모두 저장
	파일 내용에 변경이 생기면 해시값도 바뀜(입력이 바뀌면 출력이 바뀌니) 그럼 **파일명이 바뀌고** **내려받는 파일명도 바뀜** 
	**기존 파일은 재사용 가능**
`React 기반으로 만들때는 .css 파일, .js파일 import로 사용해라`

자바스크립트 파일에서 import 키워드를 이용해서 가져온 폰트, 이미지 등의 리소스 파일 → build/static/media 폴더에 저장
	(이때, 10k 이하의 작은 파일은 **data url 형식**으로 자바스크립트 파일에 저장) -> 부하를 막기 위해 작은 이미지파일 로컬에 저장

> **해시(Hash)란?**
> 1) 임의 크기 입력 -> 고전 크기 출력
> 2) 유일성 보장(a != b -> H(a) != H(b))
> 		(임의의 크기를 가지고 고정된 크기의 유일성을 보장)
>3) 단방향성
>		임의의 값을 가지고 해시값을 뽑을 수 있지만 해시값을 가지고 원래 값을 찾을 수 없다.
>		* 양방향성
			p(평문) -> A(key) -> E(암호문)
>		 같은 키를 가지고 암호화, 그럼 복호화도 가능
>		* 단방향성
			a -> H(a) 는 가능, H(a) -> a 불가능
>4) 좋은  해시 알고리즘은 **빠른 연산**
>		입력이 다름에도 같은 출력이 나옴. 이걸 **충돌난다**
>5) 좋은 해시 알고리즘은 **충돌 회피**
>		입력이 다름에도 같은 출력이 나올 수 있으나 빈번하면 안된다!

> **해시의 사용**
> 1. **무결성 보장**(유일성에서 나옴)
>		- 무결이란?
>			- 해당하는 내용은 권한을 가지고 있는 사용자가 인가된 절차에 의해 바뀐 것을 보장하는 것
>		- 보장은 어떻게 하냐?
>			- 이 데이터의 해시값을 같이 뽑아서 시간이 흘렀을 때 전달받은 데이터와 뽑았던 해시값이 일치하는지 확인하면 **전달 과정이나 사용과정에서 원본과 동일함을 보장**
>			- Data( H(Data) ) ----> Data ( (H(Data) ) / Data로 H(Data) 만들어서 기존 H(Data)랑 확인
> 2. **인증정보 저장 처리**(Authentication) 
>		- 인가는 Authorization
>		- 식별, 식별하기 위해 내 아이디를 시스템에 제공
>		- 이 아이디가 맞는지 아닌지 식별하는 것
>		- Type1 : 지식 기반
				- id / pw
>		- Type2 : 소유 기반
				- 나만 가지고 있는 것. (ex) 공인인증서, otp, 스마트폰, 주민등록증 등)을 제시함으로써 내가 맞다는 것을 인증
>		- Type3 : 특징
				- 생체 특징(정맥, 지문 등) = 바이오 인증
				- 서명 
>		- 이렇게 Type 확인해서 인증되면 **인가**해줘야 함


> **Data URL 형식**
> 
#### #3-1 이미지 저장하고 import로 불러와보기
여기에 들어간 resource import로 불러오면 알아서 효율적으로 사용할 수 있도록 바꿔줌.
cache control 얘가 해줌

`C:\react\cra-text\src`에 이미지 두개 저장(a.png, b.png)

**![](https://lh5.googleusercontent.com/XafsBj01ndYq1_qtFcfTmp_kafjIsgHoCmcZscEqWN5mEjbPjymDeNuxCn3QeUrlYnNVMuFleITH0scMGGLNIeXawnnTnpfk7-5aPop-h_oYmnyS6wNKuhNd33EmAtrkZbOQ8Ugg)**

## 코드 분할하기
p27
앞에서는 웹팩을 가지고 코드를 뭉침(js, img 파일 등)
해당하는 사이트 전체가 있는데 js 파일 100개 있는데 모든 페이지에 쓰이지 않음. 이걸 다 뭉쳐버리면 첫페이지 들어갈때 100개 뭉쳐놓은게 다 메모리에 올라가야함 동작 -> 첫페이지 로딩 느려짐
필요한 시점에 해당하는 js 파일이 참조될 수 있도록 하는 것이 필요함 -> **분할**

내일할 거임
보통 jsx 문법 사용하고
state, props 를 이용해서 컴포넌트 만들고
컴포넌트 상태 변화
이벤트 전달
부모로부터 전달 받는거 할거임


