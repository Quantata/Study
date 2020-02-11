## Base64
- 6bit 단위로 data 잘라서 0부터 63번까지 숫자 만들 수 있음(2^6)
- 총 64개 글자로 만들어 주는 것이 base 64
- 이미지가 작은 것은 파일에 직접 들어가고 크면 `파일명.{해시값}.png`
	- 작은 이미지 와 큰이미지**![](https://lh3.googleusercontent.com/VE4lXY5c2HqGjnII1P3XvsCUMKMLY2crbdGrzak7YT_EJ9tErifqsMk8gpBe1L6jY4dTSnMGG15nR5hsDvo3kZstozzv-CMNFYJyhW3JrKJ5G9SBm8AHhreH0rxB3PXixgEQvqZq)**
## 코드 분할하기(code splitting)
- 전체 사이트에서 사용하는 코드를 다 합치면 첫페이지에 다 로딩되어야 함. 그래서 로딩시간이 길어짐
- 그리고 1-10페이지까지 있다고 할때 1-3페이지만 왔다갔다 할 수 있음

p27
- 디렉토리 생성
	```shell
	 C:\react\cra-test\src\Todo.js
	 ```
	```shell
	 C:\react\cra-test\src\TodoList.js
	 ```
	**![](https://lh3.googleusercontent.com/uatPSsVdQ0aP6-Cc20y-FBcav2VDj_K_-UZoV0PWBLv89J5ariZdOLY26_KhVlRK_GX5AKoUw6wWx2m0e2AlmgpFLo6QvGGCkne9HI0XytkD7C_81RZEY3b_CCNqSy1fTVhIv4Zq)**


**[실습]**
**"할일추가" 버튼을 클릭하면 할일+일련번호가 추가**
**![](https://lh5.googleusercontent.com/qem00lnlDXRTJVjQj0u2Rq2WxFmzNyo4dqNumEv5kP6AgifkpD6s6El6J9owm6-bfOYoHo19ShLobMrIalsmlHmfLvCO60lMp04UfyqQuDtAz7OEaE9SZY5hhhYXiMBwTwpTDYHZ)

### #1 코드를 분할하지 않고 사용
- Todo.js
```javascript
// p27 코드1-20
import React from 'react'; //default로 선언해 놓으면 그냥 쓸 수 있음

// 앞에 export 없으면 그냥 함수
// 컴포넌트 선언할 때, Class해서 선언하는게 있고, function 하는게 있음
// 상태변수 필요로하지 않고 단순하게 화면 출력을 위한 용도는 function으로 출력
// 다른 모듈에서 이 Todo 쓰게 하고 싶음 -> 선언과 동시에 export 가능
// title은 property 다른 모듈에서 전달
export function Todo({ title }) {
    return <div>{title}</div>;
} 
```
- TodoList.js
```javascript
// P27 코드 1-21
// React와 Component 를 쓰겠다
// React는 default로 선언 되어 있다. Component는 defualt 아님
import React, { Component } from 'react'
import Todo from './Todo.js';

class TodoList extends Component {
    // state는 상태 변수 = 해당 컴포넌트 내에서 사용(유지) 되는 값, 정의된 변수
    state = {   //state는 객체, todos라는 값 갖고 있고
        todos: [],  // todos 배열 갖고 있음
        

    };

    doClick = () => {     //함수인데 function이라는 키워드 없다. 화살표 함수다
        const { todos } = this.state;
        const position = todos.length + 1;  //몇 번째 할일인지 확인
        const newTodo = <Todo title={`할일 ${position}번째`} />
        this.setState({ todos: [ ...todos, newTodo ] }); //...은 배열 갖고 오고 맨마지막에 todos를 붙여줘라
    };
    //todos는 지역변수
    render(){
        // = this.name 이런식으로 하면 name값만 쏙 들어감
        const { todos } = this.state;
        return (
            <div>
                {/* button 눌렀을 때 this.doClick 함수를 실행하라 */}
                <button onClick={this.doClick}>할일 추가</button>
                {todos}
            </div>
        );
    }

}

export default TodoList;
```
- App.js
```javascript
import React from 'react';
import TodoList from './TodoList'



function App() {    // 함수형 Component, 

  return (
    <div className="App">
      <TodoList />
    </div>
  );
}

export default App;
```
아주 큰 파일, 불필요한 파일을 가져오지 않고 꼭 필요한 시점에만 갖고올 수 없는가?

### #2 코드 분할을 통해서 동적으로 자바스크립트 파일을 로딩 
`import('./Todo.js').then(() => {});`
- TodoList.js 수정
```javascript
// P27 코드 1-21

import React, { Component } from 'react'
//import Todo from './Todo.js'; // doClick함수에 추가

class TodoList extends Component {
    // state는 상태 변수 = 해당 컴포넌트 내에서 사용(유지) 되는 값, 정의된 변수
    state = {   //state는 객체, todos라는 값 갖고 있고
        todos: [],  // todos 배열 갖고 있음
        

    };

    doClick = () => {   
        //Todo.js 를 불러오고 리턴이 되면 그 다음(then)을 수행해라
        import('./Todo.js').then(({ Todo ) => {
            const { todos } = this.state;
            const position = todos.length + 1;  //몇 번째 할일인지 확인
            const newTodo = <Todo title={`할일 ${position}번
            째`} />;
            this.setState({ todos: [ ...todos, newTodo ] });    //...은 배열 갖고 오고 맨마지막에 todos를 붙여줘라
        });
    };

    //todos는 지역변수
    render(){
        // = this.name 이런식으로 하면 name값만 쏙 들어감
        const { todos } = this.state;
        return (
            <div>
                {/* button 눌렀을 때 this.doClick 함수를 실행하라 */}
                <button onClick={this.doClick}>할일 추가</button>
                {todos}
            </div>
        );
    }

}

export default TodoList;
```
**⇒ main.chunck.js 파일에 Todo.js 파일의 본문이 포함되지 않음**
→ "할일추가" 버튼을 클릭하면 `2.chunck.js` 파일(Todo.js 파일의 본문 내용을 포함)이 내려옴
→ 2.chunck.js 파일은 **최초 한번만 다운로드** (그 이후에는 caching을 이용)
**![](https://lh5.googleusercontent.com/LkT96o1axAtGFZaLSnqWtljNYazPVZJDVrIjP3ZHEjiikwyiotZgxvxUhTrZO0SUHpyoH17HsJKO5zClBo16pgMArHh5biSWH4_P99rIVa3b1gskKoKP_hJogrKImTPNAtXSpGIB)**

# ES6+
var는 최상위로 올라가서 깨질 수 있다.
가급적이면 let이나 const 사용해라 (hosting 문제)

**57p**
## 2.2 객체와 배열의 사용성 개선
### 단축 속성명(shorthand property names)
p58
실습하면서 알아보도록 합시다
-  `C:\react\es6.html` 생성
- `C:\react>npx http-server` 생성
- http://localhost:8080/es6.html 주소로 결과 확인

- 객체를 정의할때 이름을 다르게 가져갈 이유가 없으면 간단하게 써라
**[es6.html]**
	```html
	<script>
	    // 단축 속성명
	    const name = 'mike';
	    const obj_new = {
	        age: 21,
	        name,   //원래 name : 'aaa' 이런식으로하는데
	        // 객체의 속성값이 변수로 존재하면 간단하게 변수 이름만 기재할 수 있음

	        getName() { return this.name; },
	    };

	    console.log(obj_new.getName());

	    // 단축 속성명 사용하지 않은 코드와 사용한 코드를 비교
	    {
	        function makePerson_old(age, name){
	            return { age: age, name: name};
	        }
	        console.log(makePerson_old(12, 'mike'));

	        function makePerson_new(age, name){
	            return { age, name};
	        }
	        console.log(makePerson_new(12, 'mike'));

	    }
	</script>
	```
	**![](https://lh5.googleusercontent.com/SbaQyMN-wK0Uf8ZY2j9sC7eaw_jWjzhoTs-N2kKW9OXOEqn6Yu3i-x1p1NcrNDmyjsEZwA2d5xOf6G-ohhO26UseCove9aqFRBcVHTmvt4W-D7qFPPNSRUkj0DRO0iFfZtLg2k7W)**
	**es6.html** 추가
	```html
	// 콘솔 로그 출력시 단축 속성명 활용
	{
	    const name = 'John';
	    const age = 21;
	    console.log('name = ', name, ', age =', age);
	    console.log({name, age});   // 괄호 안 만이아니라 {}도 넣어줘야함
	}
	```
	**![](https://lh5.googleusercontent.com/ZVj9wS3vaOlIY9imv0Qq59R3mQzwdFxNpKQCmUxHrdQ-7w1RO5BxTt3HixnSD3pkokb02hZwFLpxFAnuGih0nOKcX2mVFIT7-rjUnXeZBzNwdLU83mq6F6BLQ4Me25iDcVgQWRvE)**
### 계산된 속성명(shorthand property names)
p59
- 속성명을 동적으로 지정

**[es6.html]**
```html
<script>
{
    function makeObject_unused(key, value) {
        const obj = {};
        obj[key] = value;
        return obj;
    }
    console.log(makeObject_unused("name", "John"));
    
    // 계산된 속성명 = 객체의 속성명을 동적으로 결정
    function makeObject_used(key, value) {
        return { [key] : value}; // 이때 key의 속성명이 "name"이됨
    }


    console.log(makeObject_used("name", "John"));
	
	//옛날에는
	/*
		obj[val0] = 1; 이런식으로 함
	*/
    let i = 0;
    let obj = {
        ["val" + i++ ] : i,
        ["val" + i++ ] : i,
        ["val" + i++ ] : i,
    };
    console.log(obj.val0, obj.val1, obj.val2)   // 1 2 3
}

</script>
```
**![](https://lh4.googleusercontent.com/OsWbCNHeVH33zGMOvPH1w_Vs-_W4xOLXXaHSR-HanCBL0bCvLBvJKbWKhRJ-sqZ8MKC-h9zeh8VZeZHTmaY17rnvxjE6OKgEoh_MxDfclUWZ3T-YBDCh7FOn-eskcNkaLRQ9n7j-)**

**[es6.html]**
```html
<script>
    let param = 'size';
    let config = {
        [param]: 12,
        ["mobile" + param.charAt(0).toUpperCase() + param.slice(1)]:4
    };
    console.log(config);
    /*
        slice는 숫자만큼 문자 자른후 가져옴
        { size: 12, mobileSize: 4 }
    */
</script>
```

```javascript
state = {
	count1: 0,
	count2: 0,
	count3: 0,
};

onClick = index => {	//몇번째 버튼 클릭했는지
	const key = `count${index}`; // key값 속성이름 넘어옴
	const value = this.state[key];	
	this.setState({ [key] : value + 1 });	
};
```
count0, count1 과 같은 반복되는 버튼이 있고 특정한 버튼을 클릭했을 때 해당 버튼에 값을 넣어주는 코드를 짠 거임.
key에 속성값이 들어감

### 전개 연산자
p60
#### 전개 연산자를 이용해서 함수의 매개변수 입력
**[es6.html]**
```html
<script>
// 전개 연산자를 이용해서 함수의 매개변수를 입력
{
    console.log(Math.max(1, 3, 7, 9));

    const numbers = [ 1, 3, 7, 9 ];
    //Math.max(numbers) 이건 안됨. max는 배열을 인자로 못받음
    console.log(Math.max(...numbers));   // 배열의 항목들을 하나씩 ',' 로 분리된 구조로 됨
}
</script>
```
**![](https://lh6.googleusercontent.com/IjqsqBPkFY9-uJbs7QkF9BL9sIA6g7ueo2L5ZOo9t_9XvG7XK8AS8GXIQ7xQWZoJZp6Vc-NPsqJpUT4GHtHDzdaR7apjIyw0lsROULc-c8wxoGR12BpPJGiAI8FxG-Z3r5zlFyGA)**



#### 전개 연산자를 이용해서 함수의 매개변수 입력
**[es6.html]**
```html
<script>
// 전개 연산자 이용해서 배열과 객체를 복사
{
    let arr1 = [ 1, 2, 3 ];
    let arr2 = [...arr1]; //arr1을 그대로 복사
    let arr3 = arr1;
    console.log(arr1);
    console.log(arr2);
    console.log(arr3);
    
    arr1[0] = 10;
	console.log(arr1); // [10, 2, 3]
	console.log(arr2); // [ 1, 2, 3]
	console.log(arr3); // [10, 2, 3]
    
    // age, name
    let obj1 = { age: 23, name: "Mike" };
    let obj2 = { ...obj1 };
    let obj3 = obj1;

    console.log(obj1);
    console.log(obj2);
    console.log(obj3);

    obj1["age"] = 30;
	console.log(obj1); // {age: 30, name: "Mike"}
	console.log(obj2); // {age: 23, name: "Mike"}
	console.log(obj3); // {age: 30, name: "Mike"}
}

</script>
```
**![](https://lh4.googleusercontent.com/Pg_xjomap6-dzdd5DvoLEVi23xTMX5tEsa9bdaZ8dIEVCp1H-0nOOTskPBDA3Ci3sulwTZPykp_o0yNhUEHIgHZ5GhMm5jdcCGc5ekYeVnsw0ppQd_JZBylaBHd-uxlasJbmAlRi)** 	**![](https://lh3.googleusercontent.com/K7DfePArCvFxb5Ua3jpyNhmrYjrtYWM-b3Lxr5wQULes0UQOvXFiipETpP85sd5oYD8OMxem-euZ-XG73D99mAGJXQgN16IjDUwFUEW60DGf3erweGDVyWK3OkbM-8ktj0TbQYJa)**

날짜
**[es6.html]**
```html
<script>
// 배열에서 전개 연산자를 사용하면 배열 요소의 순서가 유지
{
    console.log([1, ...[2, 3], 4 ]);    // [1, 2, 3, 4]
    console.log(new Date(...[2020, 0, 12]));
    console.log(new Date(2020, 0, 12));

    let today = [ 2020, 0, 12];
    console.log(new Date(today[0], today[1], today[2])); //이렇게 할 필요가 없다
    console.log(new Date(...today));
}
</script>
```
**![](https://lh3.googleusercontent.com/kEjuLdg956kezkUjFFpYQDpQqdLWNn5EbzRis5-Wf84OmSCNdRBtSLlU_I4Ec2uBjC7W6o0u1xyfvauDZJk6vQgljplAJEpOoP6HH9KVVhzAxfif5YBEjUKr8dblIupElsQ-nLbB)**

#### 전개 연산자를 이용한 두 객체 병합
```html
<script>
//전개 연산자를 이용한 두 객체 병합
{
    const obj1 = { age: 21, name: "Mike"};
    const obj2 = { hobby : 'soccer'};
    const obj3 = { ...obj1, ...obj2 };
    console.log(obj3);
    // 이건 안됨
    // console.log(obj1 + obj2);
}
</script>
```

#### 객체 리터럴에서 중복된 속성명 사용이 가능
**[es6.html]**
- obj1 에서 y 값만 바꿀때 사용
	- y가 있으면 값을 바꾸고
	- y가 없으면 값을 추가
```html
<script>
//객체 리터럴에서 중복된 속성명 사용이 가능
{
    const obj1 = { x: 1, x: 2, y: 'a' };
    console.log(obj1);

    obj1["x"] = 3;
    obj1["z"] = 4;
    console.log(obj1);   // { x: 3, y: "a", z: 4 }

    const obj2 = { ...obj1, y: 'b' };   // obj1 에서 y 값만 바꿀때
    console.log(obj2); // { x : 3, y: 'b', z: 4 }
}
</script>
```

### 배열 비구조화(array destructuring)
p61

#### 배열 비구조화를 이용한 변수 값 할당
```html
<script>
// 배열 비구조화
// 배열 비구조화를 이용한 기본값 설정
{
    const arr = [ 1 ];
    const [ a = 10, b ] = arr;
    console.log(a); // 1
    console.log(b); // undefined

    const [ c = 10, d = 20 ] = arr;
    console.log(c); // 1
    console.log(d); // 20
}
</script>
```
배열 요소를 쪼개서 배열 변수에 넣음
**![](https://lh4.googleusercontent.com/7qD8b8F7Y1KJPJKWX5AdoQPq4MwMPLfON-YILfOneK2mpoEzOURXuuQA3q7eu_plt0LtByN49f4Q1BF45Ba05UVPuLNRyT7VwN5un0kcIXiMGjGyJHrAlb4nFxqF7_unCpzmVk-z)**

#### 배열 비구조화를 이용한 값 교환
```html
<script>
	// 배열 비구조화를 이용한 값 교환
	{
	    let a = 10;
	    let b = 20;
	    console.log(a,b);

	    // a, b의 값을 교환
	    // let temp = a;
	    // a = b;
	    // b = temp;
	    // console.log(a,b);

	    [ a, b ] = [ b, a];
	    console.log(a, b);
	}
</script>
```

#### 쉽표를 이용해서 일부 속성값을 건너 뛸 수 있음
```html
<script>
    
// 쉼표를 이용해서 일부 속성값을 건너뛸 수 있음
{
    const arr = [ 1, 2, 3, 4 ];
    // let a = arr[0];
    // let b = arr[2];
    const [ a, , b ] = arr; // index로 매핑
    console.log(a);     // 1
    console.log(b);     // 3
}
</script>
```

#### 나머지 값을 별도의 배열로 만들기
```html
<script>
    
// 나머지 값을 별도의 배열로 만들기
{
    const arr = [ 1, 2, 3 ];

    const [ first, ...rest ] = arr;
    console.log(first);     // 1
    console.log(rest);      // [ 2, 3 ] // 남아있는 값을 배열로 가져옴

    const [ a, b, c, ...rest2 ] = arr;
    console.log(rest2);     // []
 
}
</script>
```

### 배열 비구조화(Object destructuring)
p63 - 객체의 여러 속성값을 변수로 쉽게 할당할 수 있는 문법
#### 객체 비구조화에서 `속성이름` 이 중요
```html
<script>
	// 객체 비구조화에서는 속성이름이 중요
	{
	    const obj1 = { age: 21, name: "Mike" };
	    const obj2 = { age: 22, name: "John" };

	    const { age, name } = obj1;
	    console.log(age);       // 21
	    console.log(name);      // Mike

	}
	{
	    const obj1 = { age: 21, name: "Mike" };
	    const obj2 = { age: 22, name: "John" };

	    const { name , age } = obj1;
	    console.log(age);       // 21
	    console.log(name);      // Mike

	}
	{
    const obj1 = { age: 21, name: "Mike" };
    const obj2 = { age: 22, name: "John" };

    const { a , b } = obj1;
    console.log(a);       // undefined
    console.log(b);      // undefined
	}
</script>
```

#### 객체 비구조화에서 별칭사용
```html
<script>
	// 객체 비구조화에서 별칭 사용
	{
	    const obj1 = { age: 21, name: "Mike" };
	    
	    const { age: a , name:b } = obj1;
	    console.log(a);       // 21
	    console.log(b);      // Mike

	}
</script>
```

#### 객체 비구조화에서 기본값 설정
```html
<script>
// 객체 비구조화에서 기본값 설정
{
    const obj = { age: undefined, name: null, grade: 'A' };
    const { age = 0, name = 'noname', grade = 'F' } = obj;
    console.log(age);       // 0
    console.log(name);      // null
    console.log(grade);     // A

}
</script>
```

#### 기본값과 별칭을 동시에 사용
```html
<script>
// 기본값과 별칭을 동시에 사용
{
    const obj = { age: undefined, name: "Mike" };
    const { age: newAge = 0, name } = obj;
       
    console.log(newAge);    // 0
    console.log(age);       // error, 별칭을 부여(newAge)하고 기본값 부여할때 age: newAge = 0; 으로 쓴다
}
</script>
```

#### 함수를 이용한 기본값
```html
<script>
// 함수를 이용한 기본값
{
    function getDefaultAge() {
        return 0;
    }

    const obj1 = { age: 21, grade: 'A' };
    const { age = getDefaultAge(), grade } = obj1;
    console.log(age);       // 21
    console.log(grade);     // A

    const obj2 = { age2: undefined, grade2: 'A' };
    const { age2 = getDefaultAge(), grade2 } = obj2;
    console.log(age2);       // 0
    console.log(grade2);     // A
}

</script>
```

#### 객체 비구조화에서 나머지 속성들을 별도의 객체로 생성
```html
<script>
// 객체 비구조화에서 나머지 속성들을 별도의 객체로 생성
{
    const obj = { age: 21, name: "Mike", grade: "A" };
    const { age, ...rest} = obj;
    console.log(rest);  // { name: "Mike", grade: "A" }

    const { name, ...rest2} = obj;
    console.log(rest2);  // { age: 21, grade: "A" }
}

</script>
```

#### for문에서 객체 비구조화를 활용
```html
<script>
// for 문에서 객체 비구조화를 활용
{
    const people = [
        { age: 21, name: "Mike" },
        { age: 22, name: "John" },
    ];

    // 방법1
    // for ( i of people ){
    //     console.log(i.age, i.name);
    //     console.log(i["age"], i["name"]);
    // }

    // 방법2
    for ( { age, name } of people ){
        console.log(age, name);
    }
}
</script>
```

#### 중첩된 객체의 비구조화
**심화학습1**
```html
<script>
// 중첩된 객체의 비구조화
{
    const obj = { name: "Mike", mother: { name: "Sara" } };
    const {
        name,
        mother: { name: motherNmae },
    } = obj;
    console.log(name);          // Mike
    console.log(motherNmae);    // Sara
}
{
    const obj = { name: "Mike", mother: { name: "Sara" } };
    const {
        name,
        mother,
    } = obj;
    console.log(name);          // Mike
    console.log(mother["name"]);    // Sara
}
{
    const obj = { name: "Mike", mother: { motherName: "Sara" } };
    const {
        name,
        mother: { motherName },
    } = obj;
    console.log(name);          // Mike
    console.log(motherName);    // Sara
}
</script>
```

#### 비구조화에서 기본값은 변수 단위가 아니라 패턴 단위로 적용
**심화학습2**
```html
<script>
// 비구조화에서 기본값은 변수 단위가 아니라 패턴 단위로 적용
{
    // [ a, b ] = [ 1, 2 ] // a,b는 변수 1,2는 값
    // [ a ] = [] // 값이 없는 거임, 값이 없을 때는 초기화 구문({prop:123})이 동작
    const [ { prop: x1 } = { prop: 123 }]  = [];
    console.log(x1);    //123
}
{
    // [ a, b ] = [ 1, 2 ] // a,b는 변수 1,2는 값
    // [ a ] = [{}] // 객체는 있는데 비어있음. 값이 있기 때문에 초기화 구문 동작하지 않음
    const [ { prop: x1 } = { prop: 123 }]  = [{}];
    console.log(x1);    // undefined
}
</script>
```

#### *객체 비구조화*에서 계산된 *속성명*을 사용
**객체 비구조화에서 계산된 속성명을 사용할 때는 반드시 *별칭*을 입력해야 함**
```html
<script>
// 객체 비구조화에서 계산된 속성명을 사용
// 객체 비구조화에서 계산된 속성명을 사용할 때는 반드시 별칭을 입력해야 함
{
    const index = 1;
    //계산된 속성명 [`key${index}`] 이렇게 만들어진 것을 속성으로 쓰겠다. {}  안에 넣음
    //계산된 속성명 그냥 못쓰고 alias 써줘야함
    const {[`key${index}`]:valueOfTheIndex } = { key1: 123 };
    console.log(valueOfTheIndex);       // 123
}
</script>
```

#### 별칭을 이용해서 다른 객체와 배열의 속성값 할당
```html
<script>
// 별칭을 이용해서 다른 객체와 배열의 속성값 할당
{
    const obj = {};
    const arr = [];
    //obj.prop : obj의 속성이 있으면 update, 없으면 prop이라는 새로운 속성 추가
    const res = { foo: obj.prop, bar: arr[0] } = { foo: 123, bar: true };
    console.log(obj);   // {prop : 123}    
    console.log(arr);   // [true]

}
</script>
```

## 2.3 강화된 함수의 기능
### 매개변수 기본값
#### 매개변수 기본값 설정
```javascript
<script>
// 매개변수 기본값 설정
{
    function printLog(a = 1 ) {
        console.log(a);
        console.log({ a });
    }

    printLog();     // 1        <= 매개변수의 기본값이 사용
                    // { a: 1 }
    printLog(2);    // 2
                    // { a: 2 }
}
</script>
```

#### 매개변수 기본값으로 함수를 호출
```html
<script>
// 매개변수 기본값으로 함수를 호출
{
    function getDefault() {
        return 1;
    }
    function printLog(a = getDefault()) {
        console.log({ a });
    }
	printLog(); // { a: 1 }
	printLog(2); // { a: 2 }
}
</script>
```

####  매개변수 기본값을 이용해서 필수입력 여부를 표현
```html
<script>
//  매개변수 기본값을 이용해서 필수입력 여부를 표현
{
    function required() {
        throw new Error('필수입력입니다.');
    }
    function printLog(a = required()) {
        console.log({ a });
    }
	printLog(2); // { a: 2 }
	printLog(); // Uncaught Error: 필수입력입니다.
}
</script>
```

#### 나머지 매개변수를 사용하는 코드
```html
<script>

// 나머지 매개변수를 사용하는 코드
{
    function printLog(a, ...rest) {
        console.log({ a, rest });
    }
    printLog(1, 2);         //  {a: 1, rest: [2]}
    printLog(1, 2, 3);      //  {a: 1, rest: [2, 3]}
    printLog(1, 2, 3, 4);   //  {a: 1, rest: [2, 3, 4]}

}
</script>
```

#### arguments 키워드를 이용해서 구현
```html
<script>
// arguments 키워드를 이용해서 구현
{
    function printLog() {
        let a = Array.from(arguments).slice(0, 1);
        let rest = Array.from(arguments).slice(1);
        console.log({ a, rest });
    }
    printLog(1, 2);         //  {a: 1, rest: [2]}
    printLog(1, 2, 3);      //  {a: 1, rest: [2, 3]}
    printLog(1, 2, 3, 4);   //  {a: 1, rest: [2, 3, 4]}

}
</script>
```

### 명명된 파라미터
p69
#### 명명된 매개변수의 사용 여부에 따라서 가독성이 달라짐
```html
<script>
// 명명된 매개변수의 사용 여부에 따라서 가독성이 달라짐
{
    const numbers = [ 10, 20, 30, 40 ];

    const result1 = getValues(numbers, 5, 25 );
    //5보다 크고, 25보다 작은 수를 추출해 주는 구나 ==> 가독성이 향상된다
    const result2 = getValues({numbers, greaterThan: 5, lessTen: 25});
}
</script>
```

#### 명명된 매개변수를 사용하면 사용하지 않는 매개변수를 생략하는 것도 가능
```html
<script>
// 사용하지 않는 매개변수를 생략하는 것도 가능
{
    const result1 = getValues(number, undefined, 25);
    const result2 = getValues({ number, greaterThan: 5 });
    const result3 = getValues({ number, lessThan: 25 });
}
</script>
```

### 화살표 함수(arrow function)
p70
#### 함수 표현식을 이용한 함수 정의 (익명 함수)
#### 화살표 함수
#### 화살표 함수에서 중괄호로 감싸지 않으면 화살표 오른쪽의 계산 결과를 반환
```html
<script>
{
	// 함수 표현식을 이용한 함수 정의 (익명 함수)
	const add1 = function (a, b) { return a + b; };

	// 화살표 함수
	const add2 = ( a, b ) => {return a + b; };

	// 화살표 함수에서 중괄호로 감싸지 않으면 화살표 오른쪽의 계산 결과를 반환
	const add3 = (a, b) => a + b;

	console.log(add1(1,2));
	console.log(add2(1,2));
	console.log(add3(1,2));
}
</script>
```

#### 매개변수가 하나이면 매개변수를 감싸고 있는 소괄호도 생략이 가능
```html
<script>
{
	// 매개변수가 하나이면 매개변수를 감싸고 있는 소괄호도 생략이 가능
	const  add5 = a  =>  a +5; // 매개변수 => 반환값 // 화살표 나오면 함수라는걸 알아야함
	console.log(add5(10));
}
</script>
```

#### 객체를 반환하는 경우 소괄호로 감싸야 함
```html
<script>
    // 객체를 반환하는 경우 소괄호로 감싸야함
    const addAndReturnObject = (a, b) => ({ result: a + b});

    //호출할 때
    console.log(addAndReturnObject(10, 20));    // { result: 30 }
    console.log(addAndReturnObject(10, 20).result);    // 30

</script>
```

#### 화살표 함수의 코드가 여러 줄인 경우
전체를 중괄호로 묶고, 반환값에는 return 키워드를 사용
```html
<script>
    // 화살표 함수의 코드가 여러 줄인 경우
    // 전체를 중괄호로 묶고, 반환값에는 return 키워드를 사용
    {
        const add = ( a, b ) => {
            if ( a <= 0 || b <= 0) {
                throw new Error("양수만 입력하세요.");
            }
            return a + b;
        };
        console.log(add(10,20));        // 30
    }
</script>
```
#### 화살표 함수에서 나머지 매개변수를 사용
화살표 함수는 일반 함수와 달리 this와 arguments가 바인딩되지 않음
```html
<script>
{
    // 화살표 함수에서 나머지 매개변수를 사용
    // 화살표 함수는 일반 함수와 달리 this와 arguments가 바인딩되지 않음
    const obj = {
        value1 : 1,
        value2 : 1,
        increase: function() {
            console.log(this);
            if (this.value1 !== undefined)
                this.value1++;
            else
                this.value1 = 1;
        },
        add: () => {    // 화살표 함수
            console.log(this);

            if (this.value2 !== undefined)
                this.value2++;
            else    
                this.value2 = 10;
        }
        
    };

    obj.increase();
    console.log(obj.value1);        // 2

    const increase = obj.increase;      // 함수 변수
    
    increase();
    console.log(obj.value1);        // 2    // 위의 obj.value1 그대로
    console.log(globalThis.value1); // 1    //이때는 this가 브라우저 객체(window)로 올라감

    obj.increase();
    console.log(obj.value1);        // 3

    console.log('-----------------');
    
    console.log(obj.value2);            // 1
    console.log(globalThis.value2);     // undefined

    obj.add();
    console.log(obj.value2);            // 1
    console.log(globalThis.value2);     // 10

    const add = obj.add;
    add();
    console.log(obj.value2);            // 1
    console.log(globalThis.value2);     // 11

    obj.add();
    add();
    console.log(obj.value2);            // 1
    console.log(globalThis.value2);     // 13


    //add라는 함수는 화살표 함수
    // 화살표 함수는 바인딩 안됨. 그땐 this가 화살표 안의 scope가 아니라 window임
    // **화살표 함수 this** == **window**

}

    
</script>
```
**![](https://lh4.googleusercontent.com/K4nWOb152mIPctbDDFBfe4nNCWyqAx9L1oBza_ltjclD1qO70-rsSOqo5urUzXsGFJIfxnmlEj7stHMFBIldSZevk_Y4Y92MrTSxSvdD_2Zs-WsHAbAprZ789HO4CkuTV0aMgtRj)**

**![](https://lh5.googleusercontent.com/MTNSzxlXMPDVi660Kfe70BhikU6xXIAt8C_Dejp1Xhr2icD1oDQNdlcKCcZj3wA-NNB0cFEefyUTHPS45AjOaVfrFAUBHLVyPozU7erdUYlNISKa-wRkGhxf9Sge2gKksDB3g2U2)**
-> add 함수 실행
**![](https://lh6.googleusercontent.com/d6ymxLXUDeZ3bd4C-iz83hHp_NnGHLc2JfCSnD7UdB7wYY90Z3jdGwyZQan1rG2yX9XxepPjWoyiioWFgVjoKZmA5-bW5H4BZlMTcWjOwSoDgv3eXXoomYGdE4r6-IE3_a9ngnut)**
⇒ P71 일반함수에서 this는 호출 시점에 사용된 객체로 바인딩



#### 생성자 함수 내부에서 정의된 화살표 함수의 this는 생성된 객체를 참조한다.
```html
<script>
{
    function Something() {
        this.value = 1;
        this.increase = () => {
            console.log(this);
            this.value ++;
        };
    }
 
    const obj = new Something();
    obj.increase();
    console.log(obj.value);         // 2
 
    const increase = obj.increase;
    increase();
    console.log(obj.value);         // 3
}
</script>
```

```html
<script>
{
    function Something1() {
        this.value = 1;
        setInterval(
            function increase() {
                if (this.value !== undefined)
                    this.value ++;
                else 
                    this.value = 1;
                console.log(this.value);
            }, 
            1000
        );
    }
    //  const obj1 = new Something1();
 
    function Something2() {
        this.value = 1;
        let that = this;
        setInterval(
            function increase() {
                that.value ++;
                console.log(that.value);
            }, 
            1000
        );
    }
    //  const obj2 = new Something2();
 
    function Something3() {
        this.value = 1;
        setInterval(
            () => {
                this.value ++;
                console.log(this.value);
            }, 
            1000
        );
    }
    const obj3 = new Something3();
}
</script>
```

## P74 프로미스(promise)

비동기 상태를 값으로 다룰 수 있는 객체

프로미스 이전에는 콜백 패턴을 많이 사용

  

프로미스 상태

-   대기중(pending) → 결과를 기다리는 상태
    
-   이행됨(fulfilled) → 수행이 정상적으로 끝났고 결과값을 갖고 있는 상태
    
-   거부됨(rejected) → 수행이 비정상적으로 끝난 상태
    
-   이행됨, 거부됨 상태를 처리됨(settled) 상태라고 함
    

  

프로미스는 처리됨(settled) 상태가 되면 더 이상 다른 상태로 변경되지 않으며, 대기중 상태에서만 이행됨, 거부됨 상태로 변경될 수 있음

```html
<script>
    // 프로미스를 생성하는 방법
    
    // new 키워드를 사용해서 프로미스를 생성
    //  이렇게 생생된 프로미스는 대기중 상태가 됨
    //  생성자에 입력된 함수는 resolve와 reject라는 콜백 함수를 매개변수로 가지며, 
    //  비동기로 작업 수행 후 성공했을 때 resolve를 호출하고, 실패했을 때 reject를 호출
    const p1 = new Promise((resolve, reject) => {
        //  ...
        //  resove(data)
        //  or
        //  reject('error message')
    });
 
    // new 키워드를 사용하지 않고, 
    //  Promise.reject를 호출하면 거부됨 상태의 프로미스가 생성
    const p2 = Promise.reject('error message');
 
    //  Promise.resolv를 호출해도 프로미스가 생성
    //  입력값이 프로미스이면 그 객체가 그대로 반환되고, 
    //  프로미스가 아니라면 이행됨 상태의 프로미스가 반환
    const p3 = Promise.resolve(param);
</script>
```

**![](https://lh3.googleusercontent.com/iAVX7X1PvBevloLth4_YNwuIMGRVEgrkJM7McGmmog8O6MuGZAsuriJ-r95qvb_uM8f6zO9MStEOzciOxKEJ9KXKIZk1amFdjqZPL7mQy8OxS74RJnmxjLVTlQcfMcxGxcW_dyjX)**
// P77 Promise.resolve 반환값

  
```html
<script>
// Promise.resolve 입력값이 프로미스가 아니면 이행된 상태의 프로미스가 반환

const p1 = Promise.resolve(123);

console.log(p1); // Promise {<resolved>: 123}

  

// Promise.resolve 입력값이 프로미스이면 그 객체가 그대로 반환

const p2 = new Promise(resolve => setTimeout(() => resolve(10), 1));

console.log(Promise.resolve(p2) === p2); // true

console.log(p2);
</script>
```
