## [실습1] 웹 퍼블리셔를 위한 프론트엔드 기초

제공되는 코드를 이용하여 다음과 같은 기능을 완성하시오.
```html
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.4.1.js"></script>
    <script>
        $(function() {
            //  TODO #1 "Welcome to ABC News" 텍스트의 색깔을 darkgreen으로 설정
            
            //  TODO #2 뉴스 링크를 클릭하면 해당 뉴스 내용만 표시되도록 기능 추가
            //     <a href="#news1">뉴스1</a> 링크를 클릭하면 
            //     <article id="news1" class="news"> ... </article> 내용만 화면에 표시
            
            //  TODO #3 문서가 로딩되면 뉴스1 메뉴를 클릭하는 코드 추가

        });
    </script>
    <style>
        header h1 { font-size: 32px; }
        .menu { background: limegreen; }
        .menu ul { margin: 0; padding: 0; list-style: none;}
	.menu li { float: left; width: auto; }
	.menu ul:after { content: ""; display: block; clear: both; }
	.menu li a { display: block; padding: 5px 20px; color: #000; text-decoration: none; }
        .news { margin: 30px 10px; }
	.news h1 { font-size: 24px; }
	.copyright { border-top: 1px solid darkgreen; padding-top: 10px; }          
    </style>
</head>
<body>
    <header>
        <h1>Welcome to ABC News</h1>
    </header>
    <nav class="menu">
        <ul>
            <li><a href="#news1">뉴스1</a></li>
            <li><a href="#news2">뉴스2</a></li>
            <li><a href="#news3">뉴스3</a></li>            
        </ul>
    </nav>
    <section id="content">
        <article id="news1" class="news">
            <h1>첫번째 뉴스 제목</h1>
            <p>첫번째 뉴스 내용</p>
        </article>
        <article id="news2" class="news">
            <h1>두번째 뉴스 제목</h1>
            <p>두번째 뉴스 내용</p>
        </article>
        <article id="news3" class="news">
            <h1>세번째 뉴스 제목</h1>
            <p>세번째 뉴스 내용</p>
        </article>
    </section>
    <footer class="copyright">Copyright 2020. All rights reserved.</footer>
</body>
<html>
```
#1 최초 접속 시 뉴스1의 내용을 출력

![](https://lh6.googleusercontent.com/s71NFNmCf5wFX0tpTqJ5yKxtAuJ_rLF_Lk5uYNpuAU4WvrSW9-x6qIX5SaaeVdI0f_b4HLOju0fFo7FQDM6k9CtJRzGoZwAdQfkMOy9q8xTwDUNK_OJvacnOf9Kxn5iV7yEZdXt8)

  

#2 메뉴 클릭 시 해당 메뉴의 내용을 출력

![](https://lh3.googleusercontent.com/wC_849czn9H5mEuK2jtYltJP3b1mfjHHb6pWoYxZ-z2IbdlE00G0XhnP6cFhe04RkwQP9Hzlz9nI8JDsTaKUb18P2UBg0Z5xJXNq0E9qTDV56td18O4495BNR6_9eqEK6ip44f2-)

## [실습2] 리액트 프로그래밍

지금까지 배운 내용을 기반으로 아래의 조건을 만족하는 프로그램을 완성하시오.

동작확인 ⇒ http://59.29.224.11:3001/  
참고 ⇒ [https://velopert.com/3480](https://velopert.com/3480)

  

#1 프로그램 로딩 시 보유하고 있는 할 일 목록의 내용을 아래와 같은 형식으로 출력

![](https://lh5.googleusercontent.com/lO1AnpbctmIqBsO-gXqvacklQOu3alAVt6iRzvu0RLyzR-r5TEJseptuZapP2Stla0aQCk2Yr-c-tZGe72W-CPQZ-_uOBuCOcKQfnZTFkMuYPYJkhm-UN2O8CT7AAsvN875Jv0Rn)

#2 할 일을 입력하고 (+) 버튼을 클릭하면 할 일이 목록에 추가

#3 할 일 목록에서 (-) 버튼을 클릭하면 해당 일정을 삭제

#4 할 일 목록에서 체크 박스를 클릭하면 해당 할 일을 비활성화(disable) 처리


### 실습 1 풀이
```html
<!DOCTYPE html>
<html>
<head>
    <script src="./node_modules/jquery/dist/jquery.js"></script>

    <script>
        $(function() {
            //  TODO #1 np"Welcome to ABC News" 텍스트의 색깔을 darkgreen으로 설정
            $('header').css('color', 'darkgreen');

            //  TODO #2 뉴스 링크를 클릭하면 해당 뉴스 내용만 표시되도록 기능 추가
            //     <a href="#news1">뉴스1</a> 링크를 클릭하면 
            //     <article id="news1" class="news"> ... </article> 내용만 화면에 표시
            

            $('.menu').on('click', 'a', function() {
                $('.news').hide();
                $(".menu a ").removeClass("menu_click")              

                let href = $(this).attr('href');
                //let content = $('.news'+href).text();
                //$(this).css('background', 'darkgreen');
                
                $(this).addClass("menu_click")

                $('.news'+href).show();
                
                // console.log("href: " + href);
                // console.log("content: " + content);
            });

            //  TODO #3 문서가 로딩되면 뉴스1 메뉴를 클릭하는 코드 추가
            $('.menu > ul > li > a').eq(0).click();

            
        });
    </script>
    <style>
        header h1 { font-size: 32px; }
        .menu { background: limegreen; }
        .menu_click { background:darkgreen;}
        .menu ul { margin: 0; padding: 0; list-style: none;}
	.menu li { float: left; width: auto; }
	.menu ul:after { content: ""; display: block; clear: both; }
	.menu li a { display: block; padding: 5px 20px; color: #000; text-decoration: none; }
        .news { margin: 30px 10px; }
	.news h1 { font-size: 24px; }
    .copyright { border-top: 1px solid darkgreen; padding-top: 10px; }        
    </style>
</head>
<body>
    <header>
        <h1>Welcome to ABC News</h1>
    </header>
    <nav class="menu">
        <ul>
            <li><a href="#news1">뉴스1</a></li>
            <li><a href="#news2">뉴스2</a></li>
            <li><a href="#news3">뉴스3</a></li>            
        </ul>
    </nav>
    <section id="content">
        <article id="news1" class="news">
            <h1>첫번째 뉴스 제목</h1>
            <p>첫번째 뉴스 내용</p>
        </article>
        <article id="news2" class="news">
            <h1>두번째 뉴스 제목</h1>
            <p>두번째 뉴스 내용</p>
        </article>
        <article id="news3" class="news">
            <h1>세번째 뉴스 제목</h1>
            <p>세번째 뉴스 내용</p>
        </article>
    </section>
    <footer class="copyright">Copyright 2020. All rights reserved.</footer>
</body>
<html>
```

### 실습2 풀이
폴더에서 `>create-react-app [폴더명]`
**[App.js]**
```js
import React from 'react';
import './App.css';
import TodoList from './TodoList'
import Form from './Form'
import TodoItemList from './TodoItemList'

class App extends React.Component {
  id = 0;
  state = {
    content: '',
    todos: []
  }
  
  onChange = e => { // input 값 받는 것
    const content = e.target.value;
    this.setState({ content });
  }

  onCreate = () => {  // todos 배열 생성
    const { content, todos } = this.state;
    console.log([...todos, content]);
    this.setState({
      todos: todos.concat({
        id: this.id++,
        text: content,
        checked: false
      }),
      content: ""
    });
  }

  // 체크 or 체크 풀기
  // TodoItem.css
  onToggle = (id) => {
    const { todos } = this.state;
    const index = todos.findIndex(todo => todo.id === id);
    const selected = todos[index];
    const nextTodos = [ ...todos ];

    nextTodos[index] = {
      ...selected,
      checked: !selected.checked
    };

    this.setState({
      todos: nextTodos
    });
  }

  onRemove = (id) => {
    const { todos } = this.state;
    this.setState({
      // id가 다른것만 복사
      todos: todos.filter(todo => todo.id !== id)
    });
  }

  render() {
    const { content, todos } = this.state;
    const { onChange, onCreate, onToggle, onRemove} = this;

    return (
      <>
        <TodoList form={
          <Form 
            value={content} 
            onChange={onChange} 
            onCreate={onCreate}/>}>
          <TodoItemList todos={todos} onToggle={onToggle} onRemove={onRemove}></TodoItemList>
        </TodoList>
      </>
    );
  }
}
export default App;
```

**[Form.js]**
```js
import React from 'react';
import './Form.css';

const Form = ({value, onChange, onCreate, onKeyPress}) => {
  return (
    <div className="form">
      <input value={value} onChange={onChange}/>
      <div className="create-button" onClick={onCreate}>
        추가
      </div>
    </div>
  );
};

export default Form;
```
**[Form.css]**
```js
.form {
    display: flex;
  }
  
  .form input {
    flex: 1; /* 버튼을 뺀 빈 공간을 모두 채워줍니다 */
    font-size: 1.25rem;
    color: rgb(235, 235, 235);
    outline: none;
    border: none;
    /* border-bottom: 1px solid #c5f6fa; */
    background: rgb(99, 100, 10);

  }
  
  .create-button {
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
    padding-left: 1rem;
    padding-right: 1rem;
    margin-left: 1rem;
    background: #22b8cf;
    border-radius: 3px;
    color: white;
    font-weight: 600;
    cursor: pointer;
  }
  
  .create-button:hover {
    background: #3bc9db;
  }
```

**[TodoList.js]**
```js
import React from 'react';
import './TodoList.css';

const TodoList = ({form, children}) => {
  return (
    <main className="todo-list">
      <div className="title">
        일정 관리
      </div>
      <section className="form-wrapper">
        {form}
      </section>
      <section className="todos-wrapper">
        { children }
      </section>
    </main>
  );
};

export default TodoList;
```

**[TodoList.css]**
```js
.todo-list {
    background: white;
    width: 512px;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23); /* 그림자 */ 
    margin: 0 auto; /* 페이지 중앙 정렬 */
    margin-top: 4rem;
  }
  
  .title {
    padding: 2rem;
    font-size: 2.5rem;
    text-align: center;
    font-weight: 100;
    background: #22b8cf;;
    color: white;
  }
  
  .form-wrapper {
    padding: 1rem;
    border-bottom: 1px solid #22b8cf;
    background: rgb(99, 100, 10);

  }
  
  .todos-wrapper {
    min-height: 5rem;
    
  }
```

**[TodoItemList.js]**
```js
import React from 'react';
import TodoItem from './TodoItem'
class TodoItemList extends React.Component {
  render() {
    const { todos, onToggle, onRemove } = this.props;

    // todos 배열을 컴포넌트 배열로 변환
    const todoList = todos.map(
        ({id, text, checked}) => (
          <TodoItem
            id={id}
            text={text}
            checked={checked}
            onToggle={onToggle}
            onRemove={onRemove}
            key={id}
          />
        )
      );
    return (
      <div>
        {todoList}
      </div>
    );
  }
}

export default TodoItemList;
```

**[TodoItem.js]**
```js
import React from 'react';
import './TodoItem.css';
import { MdCheckCircle } from 'react-icons/md'
import { IoIosCloseCircleOutline } from 'react-icons/io'

class TodoItem extends React.Component {
    
  render() {
    const { text, checked, id, onToggle, onRemove } = this.props;

    return (
      <div className="todo-item" onClick={() => onToggle(id)}>
        <div className="remove" onClick={(e) => {
          e.stopPropagation(); // onToggle 이 실행되지 않도록 해주는 함수
          onRemove(id)}
        }><IoIosCloseCircleOutline size="24"></IoIosCloseCircleOutline></div>
        
        <div className={`todo-text ${checked ? 'checked' : '' }`}>
          <div>{text}</div>
        </div>
        {

          checked && (<div className="check-mark"><MdCheckCircle></MdCheckCircle> </div>)
        }
      </div>
    );
  }
}

export default TodoItem;
```

**[TodoItem.css]**
```js
.todo-item {
    padding: 1rem;
    display: flex;
    align-items: center; /* 세로 가운데 정렬 */
    cursor: pointer;
    transition: all 0.15s;
    user-select: none;
  }
  
  .todo-item:hover {
    background: #e3fafc;
  }
  
  /* todo-item 에 마우스가 있을때만 .remove 보이기 */
  .todo-item:hover .remove {
    opacity: 1;
  }
  
  /* todo-item 사이에 윗 테두리 */
  .todo-item + .todo-item {
    border-top: 1px solid #f1f3f5;
  }
  
  
  .remove {
    margin-right: 1rem;
    color: #e64980;
    font-weight: 600;
    opacity: 0;
  }
  
  .todo-text {
    flex: 1; /* 체크, 엑스를 제외한 공간 다 채우기 */
    word-break: break-all;
  }
  
  .checked {
    text-decoration: line-through;
    color: #adb5bd;
  }
  
  .check-mark {
    font-size: 1.5rem;
    line-height: 1rem;
    margin-left: 1rem;
    color: #863bdb;
    font-weight: 800;
  }
```

