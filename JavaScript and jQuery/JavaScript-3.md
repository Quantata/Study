
# For Loop
```html
for(초기식; 조건식; 종결식) {
	문장
```

## 새로운 파일 생성
Visual Studio Code 실행 > File > Open Folder 메뉴 선택 > C:\JavaScript 폴더 선택

New File 아이콘 클릭 > test.html 파일 생성

![](https://lh3.googleusercontent.com/_qPpHazhdfoK61PSINluPQWIpheYQ8pCjhSMyRs0DTlUw63jXASxakkyVnHa7pECEeeTohU9n3t_ZQ_NqUaCh717MJaIws4UM5kEfmw9rAavGcCTJErJq4hd2Rf4GqMnT0DYmDSx)![](https://lh4.googleusercontent.com/_IChRN7WTr5kFbOMHCYg5qsYeBWV15zjzNw6JvSDiFklYl9yRW0WtGln2AhE1_qtUYnn6JGUiIbOqN7kZwrCMsAe3paotm9UPS-EmYf_I3zntCY6F5mI6-U93frL9H2iWSugCnSV)

Terminal > New Terminal 메뉴 클릭 > PS C:\javascript> npx http-server

## 구구단
```html
//구구단

for(let  dan = 2; dan < 10; dan++){
	for(let  num = 1; num < 10; num++){
	console.log(` ${dan} * ${num} = ${dan*num}`)
	}
}
```

>사용자에게는 console에서 보여주는게 아니라 화면에 찍어줘야함. 이때 사용하는 것이 **div**

### id를 header에서 호출하면 div가 먼저 없었기 때문에 Error남. 이때 두가지 해결법
1. Script를 div 밑에다가 갖다 놓는다
2. `window.onload = function()` 사용

```html
<head>
	<script>
		window.onload = function() {

			//구구단

			for(let  dan = 2; dan < 10; dan++){

				for(let  num = 1; num < 10; num++){
				// console.log(` ${dan} * ${num} = ${dan*num}`)		
				document.getElementById("display").innerText = `${dan} * ${num} = ${dan * num}`

				}

			}
		}
	</script>
</head>
<body>
	<div  id="display">
	</div>
</body>
```
이러면 또 덮어 씀. 마지막 `9*9=81` 만 나옴
이때, 기존에 있던 것에 더하기 해줘야함

```html
<head>
	<script>
		window.onload = function() {

			//구구단

			for(let  dan = 2; dan < 10; dan++){

				for(let  num = 1; num < 10; num++){
				// console.log(` ${dan} * ${num} = ${dan*num}`)
					document.getElementById("display").innerText == document.getElementById("display").innerText

+ `${dan} * ${num} = ${dan * num}\n`

				}

			}
		}
	</script>
</head>
<body>
	<div  id="display">
	</div>
</body>
```

### 가로로 단이 증가할 수 있도록 코드를 수정하시오
**![](https://lh6.googleusercontent.com/39HW71uekJ1fBwMe68QUssX9XIur9CeItVXfnY6h9MvI4mLAsUE5ks4lX9TN0JfGskoiIyhNNGoP1nRchvkVgxIy5gidY3CLD6ooxNZMQsU7kD-Ko9OWDoJ1c5KoccRNF-DUhmnY)**
```html
<head>
	<script>
		window.onload = function() {
			let  disp = document.getElementById("display");
			disp.innerText = ""
			for(let  num = 1; num <= 9; num++){
				for(let  dan = 2; dan <= 9; dan++){
					disp.innerText += `${dan} * ${num} = ${dan * num}  \t`;
				}
				disp.innerText += '\n'
			}
		}
	</script>
</head>
<body>
	<pre id="display">
	</pre>
</body>
```

> **\<pre>**
> pre와 같은 태그를 써야 입력한 그대로 나옴

> **innerText**
> 해당 id 태크 사이에 text형태로 값을 넣어라

> **innerHTML**
> html에서는 \n을 띄어쓰기로만 인식
> \<br>도 html에서는 줄바꿈. but **innerText**에서는 그냥 그대로 글자나옴
> **&nbsp** 쓰려면 HTML 사용해 줘야함

```html
<!DOCTYPE html>
<html>
    <head>
      <script>
	      window.onload = function() {
		    let  disp = document.getElementById("text");
			disp.innerText = ""

			for(let  num = 1; num <= 9; num++){
				for(let  dan = 2; dan <= 9; dan++){
					disp.innerText += `${dan} * ${num} = ${dan * num}  \n`;
				}
				//disp.innerText += '\n'
			}
			let  disp2 = document.getElementById("display");
			//disp.innerText = ""
			for(let  num = 1; num <= 9; num++){
				for(let  dan = 2; dan <= 9; dan++){
					disp2.innerHTML += `${dan} * ${num} = ${dan * num} &nbsp &nbsp`;
				}
				//disp.innerText += '\n'
			}
		}
		</script>
    </head>
    <body>
	    <div  id="text">
		</div>
		<div  id="display">
		</div>
    </body>
</html>
```

### 사용자가 입력한 숫자에 해당하는 구구단을 출력해 보세요
<코드 추가>


### 아래와 같은 형식으로 콘솔에 출력해 보세요.
**![](https://lh3.googleusercontent.com/uhybqxCja4xre4m6MfAz0fQH2Fsuhp2AvD6xhQ6ToK3SYjX_cFe0VEeSClvM1mCj5qU6fgy9rB8kHV6Hxm7RzpJqgjJe9530L1PTZ5oQPVIiV5cknkOWcA8__umsTLe6_VEf-WrO)**
<코드 추가>


**![](https://lh4.googleusercontent.com/m50OxUZqjTi3q8znofSC-O1z-vNHpe7YEodMUMzqfGFsMLQFQIOh3Qew6Me-RlHd_cb4XtDrsrHzn0XezUrTB3GgIQfPwc2ThWgDvHqSBGpyTBtUjsN6cI2xxvH2NeeO7-SzCdVf)**
<코드 추가>


# Break, Continue
## break
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        window.onload = function() {
			for(let  i = 0; true; i++){
				// 코드 4-18
				console.log(`${i}번째 반복입니다.`);
				if(!confirm("계속할까요?")) {
					break;
				}
			}
			console.log(`프로그램을 종료합니다.`);
        }
      </script>
    </head>
    <body>
    </body>
</html>
```
confirm했을때 `아니오` 하면 false 반환 `!confirm` 이기때문에 true를 반환하고 break를 만나서 종료.
> `break`는 반복문을 빠져나올때 사용 

## continue
continue는 가장 가까운 반복문으로 올라감
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        window.onload = function() {
			for(let  i = 0; i < 10; i++){
				// 코드 4-18
				console.log(`이전`, i);
				if(i % 2 === 0) {
					continue;
				}
				console.log('이후', i);			
			}
			console.log(`프로그램을 종료합니다.`);
        }
      </script>
    </head>
    <body>
    </body>
</html>
```

### 배열에 포함된 숫자의 합을 구하시오.
#### for-in 구문 사용
- 배열의 인덱스 반환
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        window.onload = function() {
			//배열에 포함된 숫자의 합을 구하시오
			const  values = [100, '백', 200, '이백', 300, '삼백'];
			let  result = 0;
			//for in은 배열의 index를 반환함. java에서는 값을 반환
			//이거 불편해서 for of 구문 나옴
			for(i  in  values){
				let  v = Number(values[i]);
				if(!isNaN(v)){
					result += v;
				}
			}
			console.log(`배열에 포함된 숫자의 합은 ${result} 입니다.`);
			document.getElementById("result").innerText = `배열에 포함된 숫자의 합은 ${result} 입니다.`;
        }
      </script>
    </head>
    <body>
    <div  id="result"> </div>
    </body>
</html>
```

> for in 구문은 인덱스를 반환 그래서 **for of** 나옴

#### for-of 구문 사용
- 배열의 값 반환
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        window.onload = function() {
			//배열에 포함된 숫자의 합을 구하시오
			const  values = [100, '백', 200, '이백', 300, '삼백'];
			let  result = 0;
			//for of는 배열의 값을 반환
			for(i  of  values){
				let  v = Number(i);
				if(!isNaN(v)){
					result += v;
				}
			}
			console.log(`배열에 포함된 숫자의 합은 ${result} 입니다.`);
			document.getElementById("result").innerText = `배열에 포함된 숫자의 합은 ${result} 입니다.`;
        }
      </script>
    </head>
    <body>
    <div  id="result"> </div>
    </body>
</html>
```

# 함수
- 함수
	- 규칙성을 가지고 반복적인 작업들을 하나의 기능으로 묶어놓은 것
- 입력
	- 매개변수(=파라미터=인자(값))
		- 함수가 일정한 규칙을 수행하기 위해 필요한 인자 값
- 출력(=반환값=리턴값)

## 함수를 정의하는 방법
함수 리터럴
```javascript
function add (x,y) { return x + y; }
```
1. function
	- function 키워드
2. add
	- 함수 이름 (식별자)
3. (x,y)
	- 매개변수 목록 = 파라미터
4. {return x+y;}
	- 함수 본문(body)

**함수 리터럴 외에도 함수를 정의할 수 있음**
- 함수 선언문(function statement)
- 함수 표현식(function expression)
- Function() 생성자 함수

## 함수 선언문을 이용한 함수 정의 방법
= 함수 리터럴과 동일한 방법
반드시 **함수 이름을 정의 해야함**
```javascript
//함수 선언
function add (x, y) {
	return x + y;
}

//함수 호출
add(3, 4);
```

## 함수 표현식을 이용한 함수 정의 방식
자바스크립트에서 함수는 하나의 값으로 취급
```javascript
let str = "hong il dong";
let add = function (x, y) { return x+ y; };
```
여기서 함수 특징 **이름이 없다!!!**
이것은 **익명 함수** (이름이 있는건 **기명 함수**)
익명 함수로 함수 정의하고 있음.
정의한 함수를 add라는 변수에 할당
이렇게 되면 add라는 함수를  호출할 수도 있고 
```javascript
add(3, 4);
let sum = add;
sum(4, 5)
```
이런식으로 사용 가능

**![](https://lh6.googleusercontent.com/Koj5EVzJ2nu_ddjrtSITtcOgw5ttWTMu3qc8nnZk2ZF2c6HIsu5i-LLgTQdd_Dq_Wslw-vz1QR874E5ckYAtaT_B-doq4vWiWJ8y6iYENaTgjZhNGF8Sg5wVKZNkOHnCsw2IIYCN)**

> **기명함수인 경우**
> 함수 표현식에 사용된 함수 이름은 외부 코드에서 접근할 수 없다.
```javascript
let sum = function add (x, y) { return x + y; }
```
이렇게 하면 
`console.log(add(3,4))`
`console.log(sum(3,4))`
하면 어떻게 될까?
`sum(3,4)` 는 정상 출력
`add(3,4)` 는 출력 불가
외부에서 함수 이름 출력 안됨.

## 함수 선언문
함수 선언문 형식으로 정의한 함수는 자바스크립트 내부에서 함수 이름과 함수 변수 이름이 동일한 함수 표현식 형식으로 변경
```javascript
//함수 선언문 형식으로 정의
function add (x, y) {
	return x + y;
}

//함수 표현식 방식으로 바꾼 것
let add = function add(x, y) {
	return x + y;
}
```
	
## Function() 생성자 함수를 이용한 함수 생성
[Function 생성자를 이용해서 함수 만들 수 있다](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function)
```javascript
new Function ([arg1[, arg2[, ...argN]],] functionBody)
```
위에서 정의한 add함수는 Function을 이용해서 사용가능

```javascript
let add = new Function('x', 'y', 'return x+y');
add(3,4);
```
이렇게 정의할 수 있다.

여기까지 함수의 기본!

## 익명 함수 => 익명함수 표현식
```html
//선언
let 함수 이름 변수 = function (매개변수) {함수 본문};

//호출
함수이름변수(매개변수);
```
1부터 사용자가 입력한 숫자만큼의 합을 반환하는 함수를 정의
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //1부터 사용자가 입력한 숫자만큼 합을 반환하는 함수를 정의
        function sigma(n) {
          let sum = 0;
          for(let i = 1; i <= n; i++){
            sum += i;
          }
          return sum;
        }

        let num = prompt("숫자를 입력하세요.");
        console.log(`1~${num} 합은 ${sigma(num)} 입니다.`)
      </script>
    </head>
    <body>
    </body>
</html>
```
- 3가지 형태
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //1부터 사용자가 입력한 숫자만큼 합을 반환하는 함수를 정의
        function sigma(n) {
          let sum = 0;
          for(let i = 1; i <= n; i++){
            sum += i;
          }
          return sum;
        }

        let sigma2 = function(n) {
            let sum = 0;
            for(let i = 1; i <= n; i++){
                sum += i;
            }
            return sum;
        };  //함수 전체가 변수의 값이다까지 찍어주는 것임

        let sigma3 = (n) => {
            let sum = 0;
            for(let i = 1; i <= n; i++){
                sum += i;
            }
            return sum;
        };

        let num = prompt("숫자를 입력하세요.");
        console.log(`1~${num} 합은 ${sigma(num)} 입니다.`);
        console.log(`1~${num} 합은 ${sigma2(num)} 입니다.`)
        console.log(`1~${num} 합은 ${sigma3(num)} 입니다.`)

      </script>
    </head>
    <body>
    </body>
</html>
```

### 선언적 함수
- p123
- 함수 선언문 방식으로 생성한 함수
```html
//선언
function 함수이름 (매개변수) { 함수 본문 }

//호출
함수이름(매개변수);
```

## 함수 재정의
- 124p
- 동일한 이름의 함수가 중복해서 정의되는 것
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //같은 이름의 함수를 정의하고 호출
        function doSomething(x, y) { return x + y;}
        function doSomething(x, y) { return x * y;}

        console.log(doSomething(3,4));
      </script>
    </head>
    <body>
    </body>
</html>
```
여기서 아래부분이 호출됨.
동일한 함수 정의되면 맨 마지막에 정의된 함수 호출됨.

- 함수 표현식 방식
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //같은 이름의 함수를 정의하고 호출
        //선언무        function doSomething(x, y) { return x + y;}
        function doSomething(x, y) { return x * y;}

        console.log(doSomething(3,4));
		
		//표현식
        var doSomething2 = function(x, y) { return x + y; }
        var doSomething2 = function(x, y) { return x * y; }
        console.log(doSomething2(4, 5));
      </script>
    </head>
    <body>
    </body>
</html>
```
똑같이 마지막으로 정의된 함수가 호출됨
그럼 선언 방식이 달라도 같은거야??

```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //같은 이름의 함수를 정의하고 호출
        //선언문
        console.log(doSomething(3,4));

        function doSomething(x, y) { return x + y;}
        function doSomething(x, y) { return x * y;}

        //표현식
        console.log(doSomething2(4, 5));
        var doSomething2 = function(x, y) { return x + y; }
        var doSomething2 = function(x, y) { return x * y; }

      </script>
    </head>
    <body>
    </body>
</html>
```
이러면 밑에게 오류남.
변수를 선언하기 전에 사용했기 때문에 오류가 났다.

선언문 형태로 정의된 함수들을 먼저 읽는다. 
선언문 형태 함수는 위치와 상관없이 호출할 수 있음. (함수가 hosting되었다.) 그래서 마지막으로 곱하기한 결과가 나옴.

표현식은 var 변수 자체는 위로 올라가는데 var 변수의 값은 할당되기 전까지는 모르는 것.

> **책 추천**
> 인사이드 자바스크립트
>코어 자바스크립트
>러닝 자바스크립트

## 선언문 vs 표현식(익명)
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        // 선언문 형식으로 정의된 함수와
        // 표현식 형식으로 정의된 함수가 공존하는 경우

        var f = function() {
            console.log("#1 f is called");            
        };
        function f () {console.log("#2 f is called.");}

        f();

      </script>
    </head>
    <body>
    </body>
</html>
```
**선언문 형식**이 익명 함수(표현식) 보다 **먼저 만들어지고** 익명 함수가 마지막에 생성

## 매개변수와 return 값
- 매개변수
	- 함수 실행할 때 넘겨 주는 값
- return 값
	- 반환하는 값

### 매개변수
- 매개 변수에 따른 배열
- 배열에 들어가는 타입 한정짓지 않음
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //p129
        //다양한 형식의 매개변수를 전달할 수 있다.
        let arr1 = new Array();
        let arr2 = new Array(10);
        let arr3 = new Array(1, 2, 3, 4);

        console.log(arr1);  // []
        console.log(arr2);  // [empty x 10]
        console.log(arr3);  // [1, 2, 3, 4]
      </script>
    </head>
    <body>
    </body>
</html>
```

## 가변인자 함수
- 파라미터(매개변수)의 개수가 변할 수 있는(= 고정되어 있지 않은) 함수
	- 함수 객체의 arguments 속성을 이용해서 매개변수를 이용(처리)
- 모든 함수에는 arguments가 있음
- 앞에서 함수를 정의할 때 new function() 사용해서 생성. 이 function이라는 객체가 arguments를 갖고 있기 때문에 이를 이용해서 생성된 함수는 arguments 갖고 있음

### 매개변수로 전달된 숫자값의 합을 구하는 함수 정의
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //매개변수로 전달된 숫자값의 합을 구하는 함수를 정의
        //모든 함수에는 arguments가 있음
        //앞에서 함수를 정의할때 new function() 이라는거 사용
        //이 function이라는 객체가 arguments를 갖고 있기 때문에
        function sumAll() {
            console.log(typeof arguments);
            console.log(arguments);
            let sum = 0;
            for (i of arguments){
                if(!isNaN(Number(i))){
                    console.log(i);
                    sum += i;
                }

            }
            return sum;
        }
        console.log('모든 숫자의 합: ' + sumAll(1, "하나", 2, "둘", 3, "셋")); // 6
        
      </script>
    </head>
    <body>
    </body>
</html>
```
가변길이의 파라미터를 전달했을 때 **arguments**를 이용해서 내가 원하는 기능 구현할 수 있다.


### 함수 실행 중간에 값을 return하는 경우
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        // 함수 (실행) 중간에 반환하는 경우
        console.log("f() 호출 전");
        function f() {
            console.log("return 전");
            return;
            console.log("return 후");

        }

        f();
        console.log("f() 호출 후")
      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh6.googleusercontent.com/StduVmjlhQvCGf5mbC8oiYXY2iqiBjFXFuyzTVxHIKX9-GBHsKX-0yQmzsB0oauhW1ykdthKo_dUhyxBTfR08ZM1iTdnna4FL2fOsrpD6dYF39K0EO5iE29Iviy351OUmtVUGVE7)**

### 파라미터로 전달된 숫자 중 첫번째 3의 배수를 반환하는 함수를 작성하시오
- for in
```html
<!DOCTYPE html>
<html>
    <head>
      <script>
        //  파라미터로 전달된 숫자 중 첫번째 3의 배수를 반환하는 함수를 작성하시오
        function f() {
            for(i of arguments){
                if(i % 3 === 0){
                    return i;
                    break;
                }
            }
        }
        console.log(f(1,7,11,15,20,12));    // 15

      </script>
    </head>
    <body>
    </body>
</html>
```

- for-Each
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //  파라미터로 전달된 숫자 중 첫번째 3의 배수를 반환하는 함수를 작성하시오
        //for-of
        function f1() {
            for(i of arguments){
                if(i % 3 === 0){
                    return i;
                    break;
                }
            }                
        }
        
        //for-each
        //find 조건 맞으면 값을 반환
        function f2() {
	        return Array.from(arguments).find(i => i % 3 === 0);
	    }
		
		function f3() {
			return [...arguments].find(i => i % 3 === 0);
		}
	    //for-each는 예외 안던지면 중간에 멈출 수 없음
        /*
        function f2() {
            let value;
            Array.from(arguments).forEach(i => {
                if(i % 3 === 0){
                    //console.log(typeof i);
                    value = i;
                    return true;
                }   
                return value;
            });

        }

        //for-each
        //[...argumnets, 12, 16] 기존 배열에 더해서
        function f3() {
            let value;
            [...arguments].forEach(i => {
                if ( i % 3 === 0) {
                    value = i;
                    return false;
                }
            });
            return value;
        }
		*/
        let f = f1;
        console.log(f(3));    // 3
        console.log(f(3, 7, 11));    // 3
        console.log(f(1, 7, 11, 15));    // 15
        console.log(f(1,7,11,15,20,12));    // 15

      </script>
    </head>
    <body>
    </body>
</html>
```
>**[...arguments, 12, 13]**
>기존 arguments들을 배열로 받고, 12, 13 값을 더 추가
>[...arguments]만 사용 가능

## 내부 함수
- 135p
- 함수 내부에서 함수를 정의
```javascript
function 외부함수() {
	function 내부함수1 () { ... }
	function 내부함수2 () { ... }
}
```
### 피타고라스의 정리
- 137p
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
       //피타고라스 정리를 이용한 빗변의 길이를 구하는 pythagroas 함수를 정의
       function pythagoras (width, height){
           return Math.sqrt(width * width + height * height);
       }

       console.log(pythagoras(3, 4));   // 5
      </script>
    </head>
    <body>
    </body>
</html>
```
- 함수는 이런 반복적인 기능(width, height를 곱하는) 을 구현해 놓은 것
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
       //피타고라스 정리를 이용한 빗변의 길이를 구하는 pythagroas 함수를 정의
       function pythagoras (width, height){
           return Math.sqrt(square(width) + square(height));
       }
		
		//곱하기 함수 추가
       function square(x) {
           return x * x;
       }
       console.log(pythagoras(3, 4));   // 5
      </script>
    </head>
    <body>
    </body>
</html>
```

근데 square가 이렇게 재정의 될 수도 있음. 코드가 많아지면. 그래서 이 square 함수가 피타고라스 함수에서만 사용될 수 있도록 **내부함수**로 정의
```javascript
//재정의로 인해 원하는 값이 나오지 않음
<!DOCTYPE html>
<html>
    <head>
      <script>
       //피타고라스 정리를 이용한 빗변의 길이를 구하는 pythagroas 함수를 정의
       function pythagoras (width, height){
           return Math.sqrt(square(width) + square(height));
       }

       function square(x) {
           return x * x;
       }
       //같은 이름의 다른 기능을 함수로 구현
       function square(width, height, hypotenuse){
           if (width * width + height*height === hypotenuse*hypotenuse)
                return true;
            else
                return false;
       }
       console.log(pythagoras(3, 4));   // 5
      </script>
    </head>
    <body>
    </body>
</html>
```
- 내부 함수로 정의한 코드
> 내부함수를 정의하면 외부에 같은 이름의 함수가 있어도 내부함수를 사용
```javascript
//외부에 재정의된 함수 있어도 내부의 square함수를 실행함
<!DOCTYPE html>
<html>
    <head>
      <script>
       //피타고라스 정리를 이용한 빗변의 길이를 구하는 pythagroas 함수를 정의
       function pythagoras (width, height){
            function square(x) {
                return x * x;
             }
           return Math.sqrt(square(width) + square(height));
       }

       //같은 이름의 다른 기능을 함수로 구현
       function square(width, height, hypotenuse){
           if (width * width + height*height === hypotenuse*hypotenuse)
                return true;
            else
                return false;
       }
       console.log(pythagoras(3, 4));   // 5
      </script>
    </head>
    <body>
    </body>
</html>
```

## 자기 호출 함수
- 139p
- 생성하자마자 한번 호출되는 함수
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
            //기존 호출했던 방법
            let f = function() {
                console.log("#1");
            };
            f();

            //소괄호로 묶어서 함수 정의하고 정의한 함수를 (); 로 실행
            //선언과 동시에 실행
            (function () {
                console.log("#2");
            })();
      </script>
    </head>
    <body>
    </body>
</html>
```

## Callback 함수
- 139p
- **동기화**(동기식 처리)
	- 어떤 하나의 처리결과가 끝나야만 다음으로 넘어가는 것

-  **비동기화**(비동기식 처리)
	- 함수를 호출하고 넘어감(f()호출, g()호출, ....)
	-  호출한 f()의 결과가 올 수 있음
	-  뒤에오는 결과를 처리하기 위해서는 호출한 함수에게 메세지를 전달해 줘야함.
	- event handler 등이라고 말함
		> ex) 엄마
		> "숙제 다했어? 다하고 나면 얘기해" - Call back
		> f()에게 다 끝나면 나에게 얘기하라고 전하는 것

- sub함수가 처리가 끝났을 때 처리하는 함수
- 병렬로 main흐름이 있고 side흐름이 있을 때, side를 호출하고 넘어갔을때 side에 메세지를 전달
- 시스템 자원을 효율적으로 사용하기 위해서 사용
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //p139
        function callTenTimes(cb) {
            for(var i = 0; i < 10; i++){
                cb(); //매개 변수이름에 (); 했으니 매개변수 callback은 함수일 가능성 있음
            }
        }

        var cb = function(){
            console.log("함수호출");
        }

        callTenTimes(cb);

      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/uQ6asHFjwA8dB6xtJY-N_FGCeQbnBJeECJWPAROEvBAELIWyW87KjBlIZ8Uae-jKAjb1deuLEkqQAfE6A_mUVIRHtnKK42OLBJ7UywtrUOAttiXm88KRBphU_KGhL3fp4lp4vHqo)**
비동기 처리에서 내가 끝났어! 했을때 callback함수 많이 씀.

## 함수를 리턴하는 함수
- 141p
- 함수를 반환하는 함수
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //141p
        function returnFunction() {
            return function() {
                console.log("^^");
            };
        }
        
        //returnFunction(); //
        let f = returnFunction();   
        console.log(f); //{ console.log("^^");}라는 함수가 f에 반환
        returnFunction()(); //우리는 그 함수의 실행이 필요
      </script>
    </head>
    <body>
    </body>
</html>
```
이것을 하는 이유는 closer를 하기 위해 하는 것

## Closer(클로저)
- 141p
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
          // 클로저
          function f(name) {
              var output = `Hello ${name}!!!`;
              console.log(`f() 안 ` + output);
          }

          f('홍길동')

          console.log(`f() 밖` + output);
      </script>
    </head>
    <body>
    </body>
</html>
```
- javascript에서는 함수 안의 변수에 대해 함수 안에서만 사용할 수 있도록 되어 있음
- 외부에서 직접 함수 내 변수에 참조해서 사용할 수 없음
**![](https://lh5.googleusercontent.com/XLeEPgmZq_Dx5FHmtbQGuRGMo9aXalYz1wUg9ukDlBq77TC9w3_gvvVUi7p22pPjN7pL9IuFDgr7nEABKxIhVgf_mtQFCYoSz6w2ZlK8gdovRZbto-TdwIXm25K87OWkVZM-_r3D)**
- 144p
- 클로저의 정의는 아주 다양합니다
	- 지역변수를 함수반환 이후에도 사용할 수 있도록 남겨두는 것을 클로저라고도 함.
	- 함수가 저의가 됐을때 함수가 메모리 공간에 잡힘.  이때, 이러한 데이터가 저장된 공간을 클로저라고 불리기도 함.
	- 리턴된 함수가 클로저라고 불리기도 함(ex)return 함수;)
	- 살아있는 지역변수 output을 클로저라고도 함
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
          // 클로저
          function f(name) {
              var output = `Hello ${name}!!!`;
              console.log(`f() 안 ` + output);
              return function() { console.log(output); };
          }

          let ff = f('홍길동'); // 함수 반환 후에도
          ff(); //반환값 사용 가능

          console.log(`f() 밖` + output);
      </script>
    </head>
    <body>
    </body>
</html>
```
저 클로저를 사용하기 위해서는 **함수 내부에서 함수를 반환(리턴)해야함!!**
함수 내부에서 사용된 **변수의 소멸을 지연**시키는 것임!!
이런 현상을 **클로저** 라고함.

- 함수 별로 closer 형성
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
          // 클로저
          function f(name) {
              var output = `Hello ${name}!!!`;
              console.log(`f() 안 ` + output);
              return function() { console.log(output); };
          }

          let f1 = f('홍길동');
          f1();

          let f2 = f('리차드');
          f2();

      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh6.googleusercontent.com/f_7rBQUpUAxywS4gWRss8Lg_qfFDper64h25EVQnEXNlpBXPE4agDfF38BGIwcJ71dqTdeSkLDtnPt8x5Wo07hmD6c33SNDlwVgMtwKE0_cQf4ZAHWQ2bxt3ER-g7-UkCgObmYpL)**


