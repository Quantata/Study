## 기본 매개변수 값
함수의 매개변수 개수보다 적게 들어왔을때 뒤의 매개변수는 undefine 으로 들어감.
뒤에서 부터 기본 값 넣어줘야함

```javascript
//1
function add(a, b=0, c=0) {
	return a + b + c;
}

//2, 표현식(익명함수)
let add = function (a, b=0, c=0) { return a+b+c; };

//3, function도 쓰기 싫다!, 화살표 함수
let sum = (a, b=0, c=0) => { return a+b+c; };

console.log(sum(1));
console.log(sum(1, 2));
console.log(sum(1, 2, 3);
```

## 전개 연산자
- 164p
- 함수 또는 배열에 적용 가능
- argument이용해서 가변 길이 배열 처리할 수도 있지만 `...배열`해도 된다
- 길이는 호출되는 시점에 결정
- 배열 값들을 풀어서 전달할때
```javascript
function test(){
	console.log(arguments[0]);
	console.log(arguments[1]);
	console.log(arguments[2]);
}

function test2(...values){
	console.log(values[0]);
	console.log(values[1]);
	console.log(values[2]);
}
```

### 전개 연산자 예시
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //반드시 입력해야하는 부분은 a와 b 처럼.
        //들어와도되고 안들어와도 되는 것 values처럼 전개연산자로 쓰면 됨
        function test(a, b, ...values) {
          console.log('a', a);
          console.log('b',b);
          values.forEach(i => console.log('values', i));
        }
		
		//1
        test(1, 2, 3, 4, 5);
        
        let value = [ 1, 2, 3, 4, 5];
 
        //2
        test(value);
        
        //3
        test(...value); // 값들을 풀어서 전달
		
		//4
        test(...value, ...value); // 값들이 계속 풀어서 전달됨
      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh3.googleusercontent.com/V9x27-rkR5jYFts_3WFEIy1MXVSW06-3qcS98q5n7KFuLeO1C_Yjc_OFS4i4t6GsZOz_dvulh5w5DsH8X_UsjOVl_E2KBmeRSitKIE9sI01CQi_2wKns4HMrFJjhHxsjnGPzty0c)**
배열은 tuple, 객체는 속성
이때, 전개연산자가 많이 사용됨

> **비정형 데이터**는 객체 형태로 쌓아 놓음

# 객체
- 170p
- 객체와 배열의 차이
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //배열 요소에 접근하기 위해서는 배열의 인덱스를 이용 
        let colors = [ '빨강', '파랑', '초록'];
        console.log(colors);
        console.log(colors[0]); 

        //객체
        //객체 요소에 접근하기 위해서는 요소의 이름을 이용
        let person = {
          name: '홍길동',
          age: 23,
          inMarried: false,
          'favorite colors' : [ '빨강', '초록' ],
          hello: function() { return "안녕, 나는 홍길동이야"; }
        };
        console.log(person);
        console.log(person.name);
        console.log(person['name']);
        //console.log(person.'favorite colors'); //안됨
        console.log(person['favorite colors']); //됨. 공백문자 포함인 경우 대괄호 필요
        console.log(person.hello());

      </script>
    </head>
    <body>
    </body>
</html>
```
속성 javaScript가 제공하는 모든 유형 다 사용 가능
**![](https://lh6.googleusercontent.com/ECuJjmi4bmEawjKY00z_59aIrA4o124WBmiC4hvfR50RZKGUzxlBDv5lIvABWvEdK-zv7JvDYLbpy-AkqA3_CmLl9H7xUORsnk1uegO0sF-FRaRm6LtUhzhkjlIckISlrVC-6ky1)**

## 메소드
객체에 정의되어 있는 함수 **메소드**
> person 객체의 hello 메소드다!

- **객체 내부**에서 가지고 있는 값을 참조할 때는 그냥 쓰는 것이 아니라 앞의 해당하는 정보의 위치를 나타내는 **this** 넣어줌
>**this** 객체 내부의 속성
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        
        //객체
        //객체 요소에 접근하기 위해서는 요소의 이름을 이용
        let person = {
          firstName : "길동",
          lastName : "홍",
          id : 1234,
          getFullname : function() {
            //return lastName + firstName;	//오류
            return this.lastName + this.firstName;
          }
      
        };

        console.log(person);
        console.log(person.lastName + person.firstName);
        console.log(person.getFullname());
      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/Evjd1jlc81a0Hq6G6ZTcgm9_DBs5LtsWhNUmzP5TuxLP9JgTDyF9zjHTFw7v_ayg47Sq10v0CpH3a9So6C4Pl44ezUdO9dmqg0TeBbOqb305f9EzVCvYWuEdweSJ6aRDezd9ylfT)**

## 객체와 반복문
### 객체 내부 내비게이션 할 때 for-in 많이 이용
- 170p
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let firstName = "익명";
        //객체
        //객체 요소에 접근하기 위해서는 요소의 이름을 이용
        let person = {
          firstName : "길동",
          lastName : "홍",
          id : 1234,
          getFullName : function() {
            //return lastName + firstName;
            return this.lastName + this.firstName;
          }
      
        };

        //key와 value 나타냄
        for(let key in person ) {
          console.log(`${key} : ${person[key]}`);
        }

      </script>
    </head>
    <body>
    </body>
</html>
```
배열은 for in, for of, for 많이 이용하지만 **객체는 for in 구문 이용!!**
for-in 구문에서 반환하는 것은 객체 속성의 이름. 우리는 **key**라고 함
- 객체 안에서 객체 사용 가능
	-	심심할때 코드 짜보렴

## 객체 관련 키워드
- 171p
- in
	- 해당하는 객체에 그 요소가 있다/없다를 판단해주는 것
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let score = {
          C: 80,
          Java: 90,
          Python: 100,
        };

        console.log(`score 객체에 java 점수 항목이 포함되어 있나요? ${`Java` in score}`);
        console.log(`score 객체에 java 점수 항목이 포함되어 있나요? ${`JavaScript` in score}`);
      </script>
    </head>
    <body>
    </body>
</html>
```
회원정보를 db에 저장해주세요~ 하고 서버에 날렸는데 서버에서 db에 저장하고 결과를 나에게 던져줄 때, Json으로 던져줄텐데 Error code가 있는가 없는가 확인할때 사용할 수 있음.
**![](https://lh5.googleusercontent.com/oIM1lOkrQH7S2jR-kr4eT_qcoVyJBfNrFwOgDFW3Tvul3fv8LM0IQ4t5e_2NuQsNrFgrytBEAQ2MONaPvjl6rq0oD7M1t48aPHTARE2H_dxvyiHKKBjx65dE8MZfR2_PZ1uxKHB5)**
- with
	- 동일 객체에 대해 참조가 **반복**해서 일어나는 경우 사용
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let score = {
          C: 80,
          Java: 90,
          Python: 100,
        };
        
        //각 과목별 점수 출력
        console.log(`C : ${score.C}`);
        console.log(`Java : ${score.Java}`);
        console.log(`Python : ${score.Python}`);

        with(score) {
          console.log(`C : ${C}`);
          console.log(`Java : ${Java}`);
          console.log(`Python : ${Python}`);

        }

      </script>
    </head>
    <body>
    </body>
</html>
```

## 객체의 속성 추가 및 제거
- 182p
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let score = {
          C: 80,
          Java: 90,
          Python: 100,
        };

        console.log(`JavaScript` in score);
        score.JavaScript = 100;
        console.log(`JavaScript` in score);

      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh3.googleusercontent.com/rejRYhFtoU6oX1MkxBf7AdSpXCWWZSn4gmbyVEwXmijPGNn_ve8ruxJX6GOyOs6ie6Olrx2R7xj3GxiZkhXS71Doq9CR0kVhC9kgTaRS2mTD11MTwYDozILtrda4PoOvLo_8Up1G)**

- 객체 수정
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let score = {
          C: 80,
          Java: 90,
          Python: 100,
        };

        console.log(score);
        score.JavaScript = 100;
        score.C = 100;
        console.log(score);

      </script>
    </head>
    <body>
    </body>
</html>
```
- 이 개념을 확장하면 아무것도 갖고 있지 않은 객체 **선언** 하고 데이터 **추가 및 수정** 가능
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let person = {};

        person.name = '홍길동';
        person.age = 23;
        person.isMarried = false;
        
        //person 객체가 가지고 있는 모든 속성과 속성값을 반환하는 메소드
        person.toString = function() {
          //문자열 담을 변수
          let output = '';
          for( let key in person){
            //해당하는 key값이 toString이 아닌 경우에만 넣어줘야함
            //그렇지 않으면 계속 돌게됨
            if(key != 'toString')
              output += `${key} : ${person[key]}\n`;
          }  
          return output;
        }

        console.log(person.toString());     


        //속성 빼는 것 가능
        delete person.name;
        console.log(person.toString());
		
		//delete 함수처럼 사용가능
        delete(person.isMarried);
        console.log(person.toString());     

      </script>
    </head>
    <body>
    </body>
</html>
```
typeof, -, delete 연산자 - 단항 연산자
**![](https://lh5.googleusercontent.com/0NMAnnis99QcdkJCPcPifEf0AMvEkAUXATMK_Q6sF_j8jSkQHv95mAdnU-N0yqZN0G0huYmCtZsd5Y_gSfZVBMxYZkGhqo15j54e4FfOGV_FRdRsj5WwDiH12uSgHt6QWgWaCRnP)**

## 객체와 배열을 이용한 데이터 관리
- 185p
- 일반적으로 데이터를 관리할 때는  밑의 모습
- **students라는 배열에 name, korean, math, english, science라는 구조의 객체가 저장 되어 있음**
- name, korean 등은 속성
**![](https://lh6.googleusercontent.com/x2r8x7MWC8Fde6d8GnTzXwGEU0jmIjWaVzYboE-xilDSwEWB4fzhRg5UdYFg5m95OtGCw3gurT_muqq31OfQrI8BaZIYTG6W3dvIfbo5pQJJSpjpyReDgHlLFP8eBOdKQ5mdHzn6)**

객체는 students라는 배열에 들어가 있음
객체를 하나씩 끄집어 내어서 객체에게 필요한 method 추가할 것.
먼저 배열의 루프를 돌아야함
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let students = [];
        students.push({ name: 'aaa', korean: 46, math: 65, english: 25, science: 64 });
        students.push({ name: 'bbb', korean: 56, math: 63, english: 85, science: 62 });
        students.push({ name: 'ccc', korean: 56, math: 63, english: 22, science: 43 });
        students.push({ name: 'ddd', korean: 12, math: 25, english: 26, science: 23 });
        students.push({ name: 'eee', korean: 18, math: 85, english: 25, science: 25 });
        students.push({ name: 'fff', korean: 32, math: 22, english: 79, science: 25 });
        students.push({ name: 'ggg', korean: 52, math: 26, english: 42, science: 42 });
        students.push({ name: 'hhh', korean: 22, math: 25, english: 41, science: 56 });
        students.push({ name: 'iii', korean: 87, math: 79, english: 25, science: 86 });
        students.push({ name: 'jjj', korean: 24, math: 42, english: 71, science: 88 });
   
        //학생별 총점, 평균점을 구하는 메소드를 추가
        students.forEach(student => {
          console.log(typeof student);
          console.log(student);

          //개별 객체에 getSum과 getAverage를 넣은 것임
          //총점을 구하는 메소드 추가
          student.getSum = function() {
            return this.korean + this.math + this.english + this.science;
          };
          //평균점을 구하는 메소드 추가
          student.getAverage = function() {
            return this.getSum() / 4;
          }
        });


        //학생별 총점, 평균점을 출력
        students.forEach(student =>{
          //console.log(`이름 : ${student.name}, 총점 : ${student.getSum()}, 평균: ${student.getAverage()}`);
          with(student){
            console.log(`이름 : ${name}, 총점 : ${getSum()}, 평균: ${getAverage()}`);
          }
        });

      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh6.googleusercontent.com/GoXAg9zbAz7mi2Rk7MEPLceT6A9BUu49EhCRxsYkjZmjfULP54e9l_dIPi2I_0nKH4mRnq9E1eCeMfDpC77KK_NzbQdEYADUmisIGcNb2DH6zg_YuiJXoI4mS5akpovg2kQ219WI)**

## 함수를 사용한 객체 생성 방법
- 189p
- 데이터 형식에 맞춰 데이터를 배열에 개별적으로 넣어주고 들어가 있는 데이터들을 데이터에다가 getSum()과 getAverage()를 넣는 방식보다는 데이터를 넣는 포맷을 정하고 포맷에 맞게 넣어주면 좀 더 효율적으로 데이터를 관리 할 수 있음
- 미리 함수를 통해 해당하는 데이터의 구조를 만들고 그 함수를 이용하여 그 객체의 배열을 만드는 것과 데이터를 만들어 놓고 데이터를 추가(getSum, getAverage 추가) 하는 것을 비교해 보세요!
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //다섯개의 변수를 받아들이는 함수
        function makeStudent(name, korean, math, english, science){
            //result 객체 반환할 것임
            let result = {
                'name' : name, // name, 이렇게 써도 됨(key와 value 같은 때)
                korean : korean,  // korean 속성(오른쪽)
                math : math,
                english : english,
                science : science,
                getSum : function() {
                  return this.korean + this.math + this.english + this.science;
                },
                getAverage : function() {
                  return this.getSum() / 4;
                }

            };

            return result;
        }

        let students = [];
        students.push(makeStudent('aaa', 46, 65, 25, 64));
        students.push(makeStudent('bbb', 56, 63, 85, 62));
        students.push(makeStudent('ccc', 56, 63, 22, 43));
        students.push(makeStudent('ddd', 12, 25, 26, 23));
        students.push(makeStudent('eee', 18, 85, 25, 25));
        students.push(makeStudent('fff', 32, 22, 79, 25));
        students.push(makeStudent('ggg', 52, 26, 42, 42));
        students.push(makeStudent('hhh', 22, 25, 41, 56));
        students.push(makeStudent('iii', 87, 79, 25, 86));
        students.push(makeStudent('jjj', 24, 42, 71, 88));

        //메소드를 먼저 선언하고 데이터를 삽입

        //결과값 출력
        students.forEach(student => {
          with(student){
            console.log(`이름 : ${name}, 총점 : ${getSum()}, 평균 : ${getAverage()} \n`);

          }
        })

      </script>

    </head>
    <body>
    </body>
</html>
```
## 옵션 객체
- 192p
> 기본 매개 변수
	- 함수를 정의할때 함수의 파라매터에 기본값을 주는 것 

- 기본 매개변수처럼 객체도 가능
- 함수의 매개변수로 전달되는 객체를 **옵션객체**라고 부른다 
	- 옵션객체는 입력해도되고 안해도 됨
	- 초기화 해주는 과정이 필요함
- 193p
- 매개변수가 객체인 옵션 객체는 함수에서 사용되고 있는 객체가 다 있는지 확인하고 초기화 해주는 작업 필요함

- 객체를 파라미터로 받는경우
	- 위의 students.push...
	- 만약 makeStudent함수의 매개변수가 obj고 속성이름을 `obj.name` 이렇게 지정하면 자료 push할때 makeStudnet(korean : 39, math : 200, name : '하이') 로 순서없이 자료 넣을 수 있음

```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        //test 함수는 obj 객체를 매개변수로 받아들인다.
        function test(obj) {
            //초기화 하는 방법
            obj.valueA = obj.valueA || 0; //obj.valueA가 값이 있으면 true, 값이 없으면(0, NaN, Null 등)
            obj.valueB = obj.valueB || 0;
            obj.valueC = obj.valueC || 0;

            with(obj){
              console.log(`${valueA} : ${valueB} : ${valueC}`);
            }
        }

        test({ valueA : 52, valueB : 273 });
         

      </script>

    </head>
    <body>
    </body>
</html>
```
## 참조 복사와 값 복사
- 194p
- 값 복사
	- 값 그 자체가 메모리에 들어가 있는 것
- 참조 복사
	- 실제 값이 들어가 있는 곳의 주소를 값으로 갖고 있는 것
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let oldValue = 10;
        let newValue = oldValue;
        console.log(oldValue, newValue);  // 10, 10

        oldValue = 100;
        console.log(oldValue, newValue);  // 100, 10
      </script>

    </head>
    <body>
    </body>
</html>
```
- 숫자형 데이터를 값을 데이터로 갖고 있음
- 그래서 oldValue, newValue 별도의 공간에 데이터 저장

```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let oldArray = [10, 20];
        let newArray = oldArray;
        console.log(oldArray, newArray); //  [10, 20] [10, 20]

        oldArray[0] = 100;
        newArray[1] = 999;
        console.log(oldArray, newArray); //  [100, 999] [10, 999]
      </script>

    </head>
    <body>
    </body>
</html>
```
- **주소가 복사*** 되었기 때문에 같음
- 일반적으로 **가변적으로 변하는 것들**은 주소값을 갖고 있을 확률 높음
	-  숫자나 문자는 길이 만큼 갖고 있음 되는데 배열과 같이 가변적인 것들은 주소값을 저장
	- 
**![](https://lh3.googleusercontent.com/guXDQEdmefTh2d6mTUztg85782Zs5T9DG4EQeCCgL7Ipnq-OoP11W0agdiVTYfMGHbbm5EOQVekAPcK4RTquaVS-YC4fqmg4pK6FGPqaMe_hD8mGYXyKwMOTUmo86JqyxnJ8vX7j)**

> 실제 값이 복사 == 깊은 복사
> 주소 영역 복사 == 얕은 복사

> 주소 영역 복사 : 데이터 전체가 움직이는게 아니고 주소만 갖고 움직이기 때문에 성능을 높일 수 있음. 

- 필요에 따라서 어떤 배열을 가리키고 있는 주소를 복사하는 것이 아니라 배열을 가리키는 값의 배열 값들을 새로운 배열에 그대로 복사해서 새로운 메모리 영역이 새로운 배열을 가리켜야할 때도 있음

- 객체도 얕은 복사(reference를 넘긴다)
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let oldArray = [10, 20];
        let newArray = oldArray;
        console.log(oldArray, newArray); //  [10, 20] [10, 20]

        oldArray[0] = 100;
        newArray[1] = 999;
        console.log(oldArray, newArray); //  [100, 999] [10, 999]

        let oldObject = { name : 'aaa', age : 50 };
        let newObject = oldObject;
        console.log(oldObject, newObject);

        oldObject.name = 'bbb'; 
        oldObject.age = 'bbb'; 
        console.log(oldObject, newObject);

      </script>

    </head>
    <body>
    </body>
</html>
```
- 배열이나 객체는 일반적인 연산자를 이용해서 값을 바꾸면 값이 모두 바뀜
- 얕은 복사가 아니라 깊은 복사를 하고 싶다면??

> 얕은 복사로 인해 복제되면 안되는 값이 복사되는 경우 생김

```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let oldArray = [10, 20];
        let newArray = oldArray;
        console.log(oldArray, newArray); //  [10, 20] [10, 20]

        oldArray[0] = 100;
        newArray[1] = 999;
        console.log(oldArray, newArray); //  [100, 999] [10, 999]

        let oldObject = { name : 'aaa', age : 50 };
        let newObject = oldObject;
        console.log(oldObject, newObject);

        oldObject.name = 'bbb'; 
        oldObject.age = 'bbb'; 
        console.log(oldObject, newObject);

        function cloneObject(obj) {
          let output = {};  
          console.log(oldObject2, newObject2);
          for (let key in obj){
            //빈 객체인 output에 key와 value(obj[key]) 넣어줌
            output[key] = obj[key]; 
          }
          return output;
        }
        //근데 배열, 객체가 안에 들어가면 안됨. why? 주소값이 들어가서
        let oldObject2 = { name : 'xyz', age: 123 };
        
        let newObject2 = cloneObject(oldObject2);
        console.log(oldObject2, newObject2);

        oldObject2.name = 'zzz';
        newObject2.age = 999;
        console.log(oldObject2, newObject2);


        //베열의 값 그대로 복사
        //복사한 값 그대로 복사
        function cloneArray(arr) {
            let output = [];
            for(let i of arr) {
              output.push(i);
            }
            return output;
        }
        let oldArray2 = [ 10, 20];
        let newArray2 = cloneArray(oldArray2);
        console.log(oldArray2, newArray2);
        
        oldArray2[0] = 100;
        newArray2[1] = 200;
        console.log(oldArray2, newArray2);
        

      </script>

    </head>
    <body>
    </body>
</html>
```
## 전개 연산자를 사용한 배열 테크닉
- 200p
- 전개 연산자를 이용하여 배열을 복사하면!!
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let oldArray = [1, 2, 3, 4];
        let newArray = [...oldArray];
        console.log(oldArray, newArray);

        oldArray[0] = 100;
        newArray[1] = 200;
        console.log(oldArray, newArray);

        
      </script>

    </head>
    <body>
    </body>
</html>
```
- 배열을 복사할 때 for loop을 이용하지 않고 **전개연산자** 사용하면 배열의 **깊은 복사** 가능

**![](https://lh6.googleusercontent.com/92nANjJeoNFPjB6jYD7jCQ6fMVQ2hyJJTjJ-WMr2-SIoz-u3aUdI7nfLZTbMv-UoToDXyDUaVeOB4VywaK5vjKXkeeY5_ERkFDafplo3q7ndGp8FH_TWctLZPP_SuRUvmEERH5cM)**

## 전개 연산자를 이용한 배열의 합병
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let arrayA = [ 1, 2, 3];
        let arrayB = ['a' , 'b', 'c'];
        let newArray = [...arrayA, ...arrayB];
        console.log(newArray);        
      </script>

    </head>
    <body>
    </body>
</html>
``` 
**![](https://lh6.googleusercontent.com/z8VaxnzZSYHZu3iDzaY-sasga8BBSp8ZA0gkTQKEQoLKDw_DMfurxfjfasRwQQs4QC07Ay21ju_lRlS3iER8MOwj3mXzdOSPcKEy_X5U0iSnJki4ai_ye3-qchtVyOQYkiOaUuW5)**

## 전개 연산자를 이용한 객체의 깊은 복사
- 그렇다면 객체도 전개연산자를 이용해서 가능할까?
- 203p 
	-	전개 연산자를 이용한 객체 복제
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script>
        let objA = { name: 'aaa', age: 10};
        let objB = { ...objA };

        console.log(objA, objB);

        objA.name = 'bbb';
        objB.age = 100;
        console.log(objA, objB);

      </script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh6.googleusercontent.com/_0A1U3o4Ta87haWNXWDYw6zb9V-zkijPmhXsl3PEPsuM6L4ySFEu7moHfcXbTwJu2PAwjJQtYEMnUxe_afUWhvtiHESZ-R3SrjNwpBOKizOeleLXuL2chAv_AFLd3H9SrVPrc1Cs)**
아직 완벽한 표준은 아님
but 거의 표준

## 바벨
- javascript 만드는데 버전이 다양하고 버전 별로 쓰는 문법들이 바뀐 것들이 있음. 앞서가는 버전(브라우저는 5버전까지만 지원 but 6버전 공부해서 서비스 만들고 5버전과 호환되게 하고 싶음) 등을 어떤 버전과 호환될 수 있도록 도와주는 것
- 특히 표준과 가까운 애들...!
- 현재는 책에서 하는거 브라우저에서 지원해주고 있음
- 여기까지 객체

**생성자 객체**, **브라우저 객체 모델**, **내장 함수** 등 살면서 할 것이고
**함수**, **객체** 중요함




