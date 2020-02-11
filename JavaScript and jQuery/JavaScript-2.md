# 잡담
- 가상화란?
	- 소프트웨어를 통해 하드웨어 사용
- 가상화의 가장 큰 문제
	- 불필요한 요소가 많음
	> 나는 Apache하나, MySQL하나 이렇게 올리고 싶음. Apache랑 MySQL은 용량이 작음. 그런데 Ubuntu는 큼. 그래서 Apache, MySQL을 구동시키기 위해 Ubuntu를 깔아야하는지 의문이들기 시작함.
	**모든 VMware에 ubuntu 깔고 싶지 않음!!**
	여러개 올리니 관리도 어렵고 낭비도 심함. 내가 원하는건 10MB마먼안대 실제는 60MB 이럼

- 그래서 컨테이너가 나옴
	- Host에 있는 리눅스 코어 공유, 즉 Guest가 깔아야하는 OS부분 없음. 자원도 효율적
	- 서버를 소프트웨어적구동하는 것임. 파일 형태!! 그래서 맘에 안들어! 다른거로 넣어! 가능

**그래서 컨테이너 아키텍쳐 쓸때는 최대한 의존성 없게!!**

# HTML
[https://www.w3schools.com/html/html_basic.asp](https://www.w3schools.com/html/html_basic.asp)

- \<a href="www.naver.com"> this is naver \</a>
	- a : 태그 
	- href : 속성

- 닫는 tag 없는 거
	- img
		- `alt`
			- 이미지를 찾지 못했을때 보여주는 용도. 시각적으로 불편한 사람들 소리로 들을 수 있음
		```html
		<img src="img.jpg" alt="Girl with a jacket"/>
		```
		```html
		//끝에 '/' 넣어줘도 됨
		<img ... /> 
		```

		>**`'\'`꼭 넣기기를 권장** : React에서 .jsx에서는 닫는 태그 없으면 인식 안함
	
- \<ul>
	- unordered list
	- 순서 상관 없음
- \<ol>
	- ordered list
	- 순서 상관 있음
- \<br>
	- 다음 줄로 바꾸는 태그
- \<p>
	- 문단을 나누는 역할

## Style
[https://www.w3schools.com/html/html_styles.asp](https://www.w3schools.com/html/html_styles.asp)

- color
- background color
- font-family:[color]
- text-align:center
- 등등 홈페이지에서 확인

## Tables
[https://www.w3schools.com/html/html_tables.asp](https://www.w3schools.com/html/html_tables.asp)
- 목록
	- 같은 속성 나열
	- 테이블 태그
	**![](https://lh5.googleusercontent.com/bX6Cm3-FcPZVMAIuNptJ5r7SLTfVRDAXO8yR5LQWWBHuzpPoqgGkGId3kChNq00mmp9NRetwYjbFMvycMvus04Y3NMcE1H2rUrN8Y4UC_XO0zosI9bbUiKGm9XDU9TYSvbrUnEuQ)**
	- `tr`(table row) : 한줄에 들어가는 것
	- `th`(table header) : 컬럼
	- `td`(table data) : 그 밑에 data
1. colspan : 컬럼 합치겠다.
**![](https://lh3.googleusercontent.com/qDBHz3SaJeIBwk_vax6WJdsuIEwVHzaxGDaPk39gKHGfnW5EmDlaZDBz9XSoFVCBM0nFxjhl1Xg8FUCLoHExmmB-56zoqiNxI6Myj2fLWG4_pPScOEqyEB9T1v3uPjQvzmUvFQqN)**
```html

<table style="width:100%" border="1">
  <tr>
    <th colspan="2">Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
    <td>80</td>
  </tr>
</table>
<br>
```
2. rowspan : 행을 합치겠다
**![](https://lh5.googleusercontent.com/ZfusG59hAj10lYW68ZJbMFI_c6LinrhpcKLgh2J1wKgrXhLgsd1eCjb9yqUZE95W14zNRnbzMs1yAlbc8aAHac7xBRev1PbSeicvZQbehtBLeVfJQGyP7kJYjcNK9gJNc_X_3u5t)**
```html

<table style="width:100%" border="1">
  <tr>
    <th colspan="2">Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td rowspan="3">80</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
</table>
<br>
```

## Class
- `id`
	- 하나만 있을때
	- 문서에서 유일하게 식별해서 제어할 때
	- 첫번째 줄을 빨간색으로 바꾸고 싶을때
	- `#` 이용 - id selector
- `class`
	- 분류
	- 묶어서 제어하고 싶을때 사용.
	- 테이블 만들었는데 짝수번째 줄에는 배경 회색으로 깔고 싶으면 class로 묶어야함
	- `.` 이용 - class selector
- 태그로 가능
	```html
	<style>
		h2{
			color: blue;
		}
		#first{
			color: yellow;
		}
		.cities {
		  background-color: black;
		  color: white;
		  margin: 20px;
		  padding: 20px;
		}
	</style>
	```
- `<style>` 쓰면 css 사용한다고 생각
	- `.cities` 처럼 점이 앞에 있는 경우 클래스의 이름

**![](https://lh3.googleusercontent.com/t3tMWw5eV7INdvZ6nZw1Exfh02_Sv7ocXMivUAM-c992xLaptQsBmA-Mvrl2bnvMPgerpqYod_-rCc49uJBoX7z-_Iudea45se7OQhgcNRHRz310BHgyDNJp4BTWjUwbLKTmyzl7)**
```html
<!DOCTYPE html>
<html>
<head>
<style>
h2{
	color: blue;
}
#first{
	color: yellow;
}
.cities {
  background-color: black;
  color: white;
  margin: 20px;
  padding: 20px;
}
</style>
</head>
<body>

<div class="cities" id="first">
<h2>London</h2>
<p>London is the capital of England.</p>
</div> 

<div class="cities">
<h2>Paris</h2>
<p>Paris is the capital of France.</p>
</div>

<div class="cities">
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan.</p>
</div>

</body>
</html>
```

## from
- 입력 태그
- `<input>`
	- 한줄 입력
- `<textarea>`
	- 게시판 입력
	- 여기에 제한을 주고 싶다면 ( 값을 선택입력)
	 ```html
		<input type="radio" name="sex"> 여
		<input type="radio" name="sex"> 남
	```
- `checkbox`
	- 다중 선택 가능
	```html
		<input type="checkbox" name="color"> 빨강
		<input type="checkbox" name="color"> 노랑
		<input type="checkbox" name="color"> 파랑
	```
	- `select`
	 ``` html
	 <select>
		 <option>A</option>
		 <option>B</option>
		 <option>AB</option>
		 <option>O</option>
	```
- 타입 설정
	```html
	<input type="number" id="b" value="50">=<output ...>
	```
	--> 가는 길에 읽어라
	[https://www.w3schools.com/html/html_forms.asp](https://www.w3schools.com/html/html_forms.asp)


# JavaScript
- 자바 스크립트는 스크립트 태그를 가지고 운영 되는 것
## 문자열 입력 받는 방법
- 숫자 입력 받는 방법
	- `prompt`
	- `confirm`
		- 사용자에게 물어보는 것.
		- 확인 누르면 `True` 반환
		- 취소 누르면 `False` 반환
		- 사실 잘 안씀ㅋㅋ안예뻐서 나중에는 `toast.js` 사용
		
## let 사용
	- let사용하면 재할당은 가능
	- 재정의는 불가능
	
- 문자 + 숫자
	- 문자+숫자 결합된 문자열나옴(숫자가 문자로 변형됨)
	![](https://lh3.googleusercontent.com/v13F2rvQjLLixPBHpNVL0_FyC15cN_0lIxFxEpGThBpIQ2GYZSiTTzygPnsGiKLK0U9cvMVzvXAsZJdBUHuZhGnrmU7RDIgZNEi0TZYt3zX2CkaGcc67wPdb959wJblh3c29fyAr)
	
	- 숫자와 문자열 덧셈을 제외한 연산은 숫자가 우선임 ('문자*문자'도 숫자로 바뀜)
	![](https://lh4.googleusercontent.com/OeTg1gxwBcuU2f3dkf-RkIlionI6lrKKKmtb7xCJw2ZhcqVyVG6pPEE0aKsvh2aiSgFf9ykfLJH6DRAl7BAd_pqZKZJpsDS-bTlfaVwteABAKMzeMQbfL3yWjb8QGqa2JUzSMj7S)
## 강제적 형변환
	- 위에 한거는 JavaScript가 알아서 바꾼 `묵시적 형변환`
	- 이거는 `명시적 형변환`
![](https://lh4.googleusercontent.com/aOJTRuPTkhGP435MZJaPURqXm48oC1CIggB4fPIj_yS7jjrDOOta49o3_iwyWJaSHtJaKdl6bIAy3DQTkidPGUqo1CbfNxJ5tzRoGSHThPib2gXbgaKRO4cBdWhIrOdLQgfltTPi)

|기능                          |함수                         |
|:----:|:----:|
| 다른 데이터 타입을 숫자형으로 변환 | number()함수 사용 |
| 다른 데이터 타입을 문자열로 변환 | String() 함수를 사용

## `NAN` = Not a Number
	- 자료형은 숫자이나 자바스크립트로 나타낼 수 없는 숫자 의미
		- 예) 자바스크립트에서는 복소수 표현이 불가능(Math.sqrt(-3) 은 루트 3을 의미 이런거 NaN뜸)

![](https://lh4.googleusercontent.com/O6jMv0RUlV09F0x9VhEUBQdB_WuyxvsWMX0H0sPqutNUU-cKzR5qYB6MYJHdDuZvpHAmiLRYzxKCqU0CpPP6uOyjIqjvwihy1m7ntd0sBMqbe8-fioMoowamrZDn5IlZS0LgvHGc)

## Boolean() 함수
- boolean() 함수
	- 다른 자료형을 불(bool) 자료형으로 변환
- 0, NaN, '', null, undefined 는 모두 `false` 반환
	- 나머지는 true 변환
- 해당하는 입력값이 True다 False다 나오는데 위의 5가지 빼고는 True 나옴
- 이건 **묵시적인 형변환**
- `0, NaN, '', null, undefined 데이터에 대한 암시적인 형변환은 어떻게?`
	- `!!` 사용
![](https://lh5.googleusercontent.com/xm61fRJT5Wb0SOgDFJlXnaH36X1B5HOKRL0y2G7sqcU0DFfVBkxNKiUJrh_70MC9d_OvF2A1gbpdyyu1iwBS2hz-MjEcp0lAL75b03GmzIIHNjV3f3z4FSM28aojba3ASVH1J1l3)
	-	자동 형변화(암시적 형변환)의 문제점
		-	밑의 코드 다 True
		-	비논리적인 비교 연산이 이루어질 수 있음
		-	아무것도 없는 것은 거짓이다 0은 거짓이다 등
		-	이 같은 문제를 해결하기 위해 일치 연산자 사용!
		```html
			<script>
				console.log('' == false);
				console.log('' == 0);
				console.log(0 == false);
				console.log('273' == 273);
			</script>
		```

	- 일치 연산자
		- 양변의 자료형과 값의 일치 여부를 확인
		- `===` : 양변의 자료형과 값이 모두 일치해야 true
		- `!==` : 양변의 자료형과 값이 일치하지 않음
		- 이걸 사용하게 되면 위의 코드 모두 **FALSE**

ECMA 6에서 추가된거 백틱(`) 사용
let과 어떤거 scope 때문에 그럼

## Scope
- 중괄호 사이 안 범위
- 변수를 가질 수 있는 유효범위
- 근데 자바스크립트는 scope로 구분 안함

- var는 전역 scope에 저장
>**전역 scope** 란?
>윈도우 브라우저에 variable이란 것을 지정해 놓음. 그렇기 때문에 아무대서나 참조 가능

- 71p)보면 이걸 var를 let으로 바꾸자!
		- let으로 바꾸면 흔히 알고 있는 변수처럼 scope안에서만 변수가 살아 있음

- 72p) 코드 치겠다
	- `=>` : 화살표 함수(arrow function)
		- 함수 이름 안가져가고(익명 함수, anonymous function) 사용할때
		- 화살표로 함수 정의한다
		- 익명 함수 어떤 경우에 쓰이나?
			- 만들어 놓고 한번만 호출할 때
			- 보통 이름을 쓸때는 여러번 부르려고
		- 익명 함수 사용 법
		```html
		//1)
		function () {}
		//2)
		() => {}
		```
		- `setTimeout()` 함수
			- **비동기 함수**
				- 병렬적으로 처리하는 것
				- 어떤 것을 하는 상황에서 다른 것을 시작하고 다른 것을 시작하고
				- 그럼 비동기에서는 먼저 끝난 프로세스가 결과값을 던질 때가 꼭 있음
					- 그것이 **Call Back**
			- **동기 함수**
				- 하나씩 처리하는 것
				- A,B,C,D 있으면 A끝나면 B시작, B끝나면 C시작, C끝나면 D시작
			- 그래서 setTimeout() 걸어놓고 루프를 계속 돌아 다른일 하는 것임. 마지막 i 가 찍힘. i가 공유 됨.
			```html
			<script>
				for(var  i = 0; i < 3; i++){
					setTimeout(() => {
					console.log(i);	
					}, 1000 * i);
				}
			</script>
			```
			- 선언과 동시에 실행 -> 이거 너무 귀찮음(var가 전체적으로 다쓰이니까!) -> **let**을 쓰자!!
			```html
			<script>
					for(var  i = 0; i < 3; i++){
						((i) => {
						setTimeout(() =>{
						console.log(i);
						}, 1000*i)
						})(i);
					}
			</script>
			```
			- let 사용
			```html
			<script>
				for(let  i = 0; i < 3; i++){
					setTimeout(() => {
					console.log(i);	
					}, 1000 * i);
				}
			</script>
			```
			- 확인
			```html
			<script>
				for(var  i = 0; i < 3; i++){
					console.log("#1", i)	
					setTimeout(() => {
					console.log("#2", i);
					}, 1000 * i);
				}
			</script>
			```

		*`70p~74p(정확하지 않음)`
		*함수 안에 있지 않은 것은 다 global 변수로됨. 그걸 hosting이라고 함
		*미리 전체 코드 해석해서 함수를 위로 올렸기 때문에 함수가 정의되기 전에 호출해도 호출이 된다.
		

## typeof
- **연산자**
- 괄호 쓰고 써서 함수로 착각할 수 있음

## IF(81p)
```html
	// P81 if - else 구문을 이용한 표현
		if (hour < 12) {
		console.log('오전입니다.');
	} else {
		console.log('오후입니다.');
	}
```

- `switch`
```html
	// P87 switch 구문을 이용해서 표현

	switch (week) {
		case  0: console.log('일요일입니다.');
			break;
		case  1: console.log('월요일입니다.');
			break;
		case  2: console.log('화요일입니다.');
			break;
		case  3: console.log('수요일입니다.');
			break;
		case  4: console.log('목요일입니다.');
			break;
		case  5: console.log('금요일입니다.');
			break;
		case  6: console.log('토요일입니다.');
			break;
		default: console.log('잘못된 요일입니다.');
			break;

	}
``` 
## 삼항 연산자
- 숫자가 아닌 경우 콘솔에 오류 메시지 출력
- 연산에 사용되는 값이 3개
- `조건식 ? 참인경우 : 거짓인 경우;`

> **단항 연산자**
> - `typeof`
> - `-`
> **이항 연산자**
> 숫자가 두개 필요한 것
```html
	num % 2 === 0 ?
	console.log("짝수입니다.") : console.log("홀수입니다.");
```

## NaN
- 은 같음 연산(`==`, `===`)을 사용해서 판별할 수 없음
- **isNaN()** 사용해야함

## 짧은 조건식(short-circuit)(p89)
- 논리 연산을 할때 ||. && 이런거 있었음
	- A || B
		- A 또는 B 둘 중 하나가 참이면 참
		- A 와 B 둘 모두 거짓이어야 거짓
	- A && B 
		- A와 B 둘 모두 참이어야 참
		- A 또는 B 둘 중 하나가 거짓이면 거짓
	- &&과 || 이거는 앞에 값에 따라 결정
```html
	// 방법3. 짧은 조건문을 이용한 구현
	input % 2 === 0 || console.log("홀수");
	input % 2 === 0 && console.log("짝수");
```

## 반복문
- 97p
- 컴퓨터 나와서 가장 먼저 해결한 것은 엄청난 계산
- 2차 혁신은 반복문
	- 탄도미사일 하나만이 아니라 여러개 반복
	```html
	for(변수=초기값; 조건문; 증가분) {
		조건문을 만족하는 경우 수행할 구문
	}
	```

## 배열
- 98p
- 다른 데이터 타입이 static하게 지정되는 언어에서는 하나의 타입에 대해서만 만들 수 있음
- JavaScript는 타입에 대해 굉장히 유연함
- 배열이 길때 배열의 요소를 보고 싶을때는 loop를 돌리면 됌!
- 동일한 이름에 여러개의 값들이 있는데 이와 같은 애들을 `iterater`라고 함.
	- 방이 순차적으로 나와있으면 방 번호를 몰라도 순차적으로 가고 있음.
	- `For`
	- `For Each`에서 제공해주는 것
		- 거기 있는 값을 여기에 사용해라
	- `push`
		```html
		//배열 선언
		let arr = [ 273, 'String', true, function() {}, {}, [100, 200]];
		arr.push("xz 이후");
		//arr.length 증가
		```

## while
- p102
- while과 do while
- 근데 왠만하면 헷갈리니 do while 쓰지마라!
```html
	const  MIN = 1;
	const  MAX = 20;

	let  answer = Math.floor(Math.random() * (MAX - MIN + 1 )) + MIN; //1~20 사이 임의의 난수 생성

	let  guesses = 0;
	let  input;

	do{
		input = prompt(`${MIN} ~ ${MAX} 사이의 숫자를 입력하세요.`);
		input = Number(input);

		guesses++;

		if( input > answer) {
		console.log("입력한 값 보다 작은 값을 입력하세요");
		} else  if ( input < answer) {
		console.log("입력한 값 보다 큰 값을 입력하세요");
		} else {
		console.log("정답입니다. (시도횟수 : " + guesses + ")");
		}
	} while (input !== answer);
```

**우리가 가장 많이 쓰는건 For loop**

## For Loop
- For loop
- For In 
	- 뒤에 나오는 배열의 내용을 하나하나 가져와라
- For Each
	- fruit가 들어오면 로그를 남겨라
	- 또는 화살표 함수를 이용해서 표현

```html
<script>

	const  fruits = [ "사과", "오렌지", "딸기", "바나나" ];
	console.log("방법1. for loop");
	
	for (let  i = 0; i < fruits.length; i ++) {
		console.log(fruits[i]);
	}

	console.log("방법2. for in");

	for (let  i  in  fruits) {
		console.log(fruits[i]);
	}

	console.log("방법3. forEach");
	fruits.forEach(function(fruit) {
		console.log(fruit);
	});
	
	console.log("방법4. forEach + arrow function");
	fruits.forEach(fruit  =>  console.log(fruit));
</script>
```
