
### 속성 선택자
```javascript
<body>
  <input type="text">
  <input type="password">
  <input type="radio">
  <input type="checkbox">
  <input type="file">
</body>
```
- RadioButton : 하나만 선택 가능
- CheckBox : 여러개 선택 가능

```javascript
    <body>
      성 : <input type="text" name="lastName"><br>
      이름 : <input type="text" name="firstName"><br>
      패스워드 : <input type="password" name="pw"><br>
      패스워드(확인) : <input type="password" name="pw2"><br>
      결혼여부 : 
      <input type="radio" name="ismarried" value="Y"> 네
      <input type="radio" name="ismarried" value="N"> 아니오 <br>
      좋아하는 색깔 :
      <input type="checkbox" name="color" value="red"> 빨강
      <input type="checkbox" name="color" value="blue"> 파랑
      <input type="checkbox" name="color" value="yellow"> 노랑
      사진 :
      <input type="file" name="photo">
    </body>
```
**![](https://lh3.googleusercontent.com/94eblq0MrSorzz_-O5R9YxrHZSEe7QpJg_x0f5Nu0dmkh2nrGd7pyjNuugc_JtN7PwBj0fTmzB62aVE_7XIMgaJBL2_tQ4OfPFq2OE52kzrbMzW3k61OvqmjNU4gOPJTg6iWtlqe)**
- 공통 적으로 가저가는 속성
	- type, name, value
	- password 같은거 사용자가 입력하면 name 값이 pw에서 **입력값**으로 바뀜

> http://naver.com/abc/xyz/do.jsp
> http(스킴) - 프로토콜
> naver.com - 호스트
> abc/xyz/do.jsp - 경로

- 경로 뒤에 `?` 를 붙이는 경우 있음
	- 요청 파라미터
	- 로그인 할때와 같이 사용자에게서 입력을 받아야할 때가 있음
>`...do.jsp?lastname=Park$firstName=CL...`
>lastName = 파라미터 요청 
>Park = 파라미터 값

- **Get 방식(메소드)**
	- 값들을 서버에 전달할 때 파라미터를 주소에 포함하여 보내는 방식
- **Post 방식**
	- 서버로 날아갈때 주소에 보이지 않고 눈에 보이지 않은 요청 본문에 포함시켜 보내는 방식
	```javascript
	<body>
	<form action="#" method="get">	//POST일땐 post
	```
### 속성값 사용
```javascript
/*
p426
E[A=V] 속성값이 같은 문서 선택
E[A!=V] 속성값이 다른 문서 객체 선택
E[A~=V] 속성값의 시작 단어가 같은 객체를 선택
E[A^=V] 속성값이 글자로 시작하는 객체를 선택
E[A$=V] 속성값이 글자로 끝나는 객체를 선택
E[A*=V] 속성값이 글자를 포함하는 객체를 선택
```
- **E[A=V]** 속성값이 같은 문서 선택
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>
        $(function() {
             // 성, 이름 입력창에 OOO을 입력하시오.
             // $("#lastName").val('성을 입력하세요.');
             $('input[type="text"]').val("입력하세요.");

            //성과 이름 따로 보여주고 싶다
            //$('input[name="lastName"]') 객체에 . 찍으면 속성값나옴
            $('input[name="lastName"]').val("성을 입력하세요");
             $('input[name="firstName"]').val("이름을 입력하세요");

        });
      
      </script>

    </head>
    <body>
    <form action="#" method="get">
      성 : <input type="text" name="lastName" value=""><br>
      이름 : <input type="text" name="firstName"><br>
      패스워드 : <input type="password" name="pw"><br>
      패스워드(확인) : <input type="password" name="pw2"><br>
      결혼여부 : 
      <input type="radio" name="ismarried" value="Y"> 네
      <input type="radio" name="ismarried" value="N"> 아니오 <br>
      좋아하는 색깔 :
      <input type="checkbox" name="color" value="red"> 빨강
      <input type="checkbox" name="color" value="blue"> 파랑
      <input type="checkbox" name="color" value="yellow"> 노랑
      사진 :
      <input type="file" name="photo">
    </form>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/ByhnqF9GA_GB0NwoUrGl28nP3AvRhfhewYoINYvCedLmurjRPjKl6tPW0FK88uKYqBz41nDfRtH-p2y9_pq2u7OcPh3sHxkDvritMf0JTqNgiGsmbm0vgVy5EYQSpB2Pggkg8fSU)**
- **E[A!=V]** 속성 값이 다른 문서 객체 선택

```javascript
<script>
    // 파일 선택 창을 제외하고 나머지 입력창에 (필수입력) 표시
    //prev 하면 각각 라벨이 선택
    $('input[type!="file"]').prev().append("(필수입력)").css('color', 'red');
</script>
```
**![](https://lh4.googleusercontent.com/eqIdbQBQF2xABmFYEVN0YWRQ_vZ4iTFg9PIDQ8bIRblUZBLNpni-Y8s6JSkJgh5yHbalSORjm4wSjWJLwO2np0l8S51HCZc_IRmX1N063Ehy0JY7q_K_9FltvhzulEXRc1TTRiQV)**

- **E[A~=V]** 속성값의 시작 단어가 같은 객체를 선택
```javascript
<script>
	//name 속성에 pw가 포함된 것을 검색
    $('input[name~="pw"]').css('background', 'red');
</script>
```
- **E[A^=V]**  속성값이 글자로 시작하는 객체
```javascript
<script>
	//name 속성이 pw로 시작하는 입력창
	$('input[name^="pw"]').css('border', '3px dotted blue');
</script>
```

- **E[A$=V]**  속성값이 글자를 포함하는 객체를 선택
```javascript
<script>
	//name 속성에 o가 들어가 있는 입력창을 삭제
	$('input[name$="Name"]').css('border', '3px solid black')
</script>
```
[여기까지 결과창]
**![](https://lh6.googleusercontent.com/JesUrQ9femFaZYToX2PFD3o1cZWN7TqCWw8_5ATR1HYV6iy6owO32J202hca8r36r-MSdFF_NIagBPop0kCTXA36x2nxg0BJRXso40EeLx7AF6xDjMZ5-jbVG0fuIznHkVH-gFCL)**

- **E[A\*=V]**  속성값이 글자로 끝나는 객체를 선택
```javascript
<script>
	//name 속성에 o가 들어가 있는 입력창을 삭제
	$('input[type*="o"]').hide();
</script>
```
[hide한 결과창]
**![](https://lh4.googleusercontent.com/HD5JS8b4AlP7uFTqRIIYVX4JCZ6V7bmOpvWMyKIfl18eCzhiIYWfPYxHYYb0_QlyceGUq7cjbJRE9A7Pr7erl9nDdTzbqssWyM3MMuByw0rds1luJm3Il4qYIBcGLCeu3JNjITu9)**

- 전체코드
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>
        $(function() {
             // 성, 이름 입력창에 OOO을 입력하시오.
             // $("#lastName").val('성을 입력하세요.');
             $('input[type="text"]').val("입력하세요.");

            //성과 이름 따로 보여주고 싶다
            //$('input[name="lastName"]') 객체에 . 찍으면 속성값나옴
            $('input[name="lastName"]').val("성을 입력하세요");
            $('input[name="firstName"]').val("이름을 입력하세요");


            /*
            p426
            E[A=V] 속성값이 같은 문서 선택
            E[A!=V] 속성값이 다른 문서 객체 선택
            E[A~=V] 속성값의 시작 단어가 같은 객체를 선택
            E[A^=V] 속성값이 글자로 시작하는 객체를 선택
            E[A$=V] 속성값이 글자로 끝나는 객체를 선택
            E[A*=V] 속성값이 글자를 포함하는 객체를 선택
            */

            // 파일 선택 창을 제외하고 나머지 입력창에 (필수입력) 표시
            //prev 하면 각각 라벨이 선택
            $('input[type!="file"]').prev().append("(필수입력)").css('color', 'red');

            //name 속성에 pw가 포함된 것을 검색
            $('input[name~="pw"]').css('background', 'red');

            //name 속성이 pw로 시작하는 입력창
            $('input[name^="pw"]').css('border', '3px dotted blue');

            // name 속성이 pw로 끝나는 입력창
            $('input[name$="Name"]').css('border', '3px solid black')

            //name 속성에 o가 들어가 있는 입력창을 삭제
            $('input[type*="o"]').hide();

        });
      
      </script>

    </head>
    <body>
    <form action="#" method="get">
      <label>성</label>
      <input type="text" name="lastName" value=""><br>
      <label>이름</label>
      <input type="text" name="firstName"><br>
      <label>패스워드</label>
      <input type="password" name="pw"><br>
      <label>패스워드(확인)</label>
      <input type="password" name="pw2"><br>
      <label>결혼여부</label>
      <input type="radio" name="ismarried" value="Y"> 네
      <input type="radio" name="ismarried" value="N"> 아니오 <br>
      <label>좋아하는 색깔</label>      
      <input type="checkbox" name="color" value="red"> 빨강
      <input type="checkbox" name="color" value="blue"> 파랑
      <input type="checkbox" name="color" value="yellow"> 노랑
      <label>사진</label>
      <input type="file" name="photo">
    </form>
    </body>
</html>
```

### css를 이용해서(style 태그) 바꾸기
- css
	- 화면에 보이는 것을 뭔가 예쁘게 바꿔주는 것
- class 여러개 클래스 동시에 선언 가능
	- `\<div class="[class1이름] [class2이름"> \</div>`
	```javascript
	<body>
      <div class="num red">1</div>
      <div class="num blue">2</div>
      <div class="num yellow">3</div>
      <div class="num green">4</div>

      <div class="char red">하나</div>
      <div class="char blue">둘</div>
      <div class="char yellow">셋</div>
      <div class="char green">넷</div>

    </body>
	```
- css에서 사용하는 selector와 jQuery에서 사용하는 속성값 이용하는 것과 같음
- jQuery에서 사용하는 selector는 style태그 안에서 넣어주는 것과 동일하다
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>
        $(function() {
          // jQuery에서 쓰는 selector
          //  $("div").css('background', 'blue');

        });
      
      </script>
      
      <style>
        /* css에서 쓰는 selector*/
        div {
          border: 1px solid black;
        }

        div.num {
          background: gray;
        }
        div.red {
          color: red;
        }
      </style>
    </head>
    <body>
      <div class="num red">1</div>
      <div class="num blue">2</div>
      <div class="num yellow">3</div>
      <div class="num green">4</div>

      <div class="char red">하나</div>
      <div class="char blue">둘</div>
      <div class="char yellow">셋</div>
      <div class="char green">넷</div>

    </body>
</html>
```
**![](https://lh4.googleusercontent.com/IlKUSIgjEozjomrXc9Gl1YZ-CysEXnoFpk6UghYp4R1vALVGrO4DmKYCd8mwWcK8roDlZJw6ME4B-beDlP8ousjI-Z_P-Egdpdm1ndQFDuF7WBy7mxV_-X0I2hXYtrAdyAMp9ONu)**

- Style tag 수정
```javascript
<style>
        /* css에서 쓰는 selector*/
        div {
          border: 1px solid black;
          padding : 10px;
          margin : 10px;
          width : auto;
          height : auto;
          font-size: 30px;
          
          /* float : 영역 이외에 공간이 남으면 끌어올려서 원하는 방향으로 으로 붙이는 것 */
          float : left; 
          
        }
</style>
```
**![](https://lh3.googleusercontent.com/T97goeNei643nrGyjJ4jpreZB0NAfcgS5R3Ob1z7DqKcp9L5w3sbQBYGNsV5zohAFW0bm_raS9GVU24mpKRuFDNce-GjRrMdDdRNuXkA19JHq0zB64JgLIGCLsQ0dAEmKgp884Cp)**

- margin을 각각 주고 싶다
	- margin : [top] [right] [bottom] [left]
```javascript
//네개 다쓰면 네개 다 먹음
//한개쓰면 모두 적용
//두개는 top과 bottom만
//세개까지 적으면 top, right, bottom에 적용
```
- 색도 다시 넣음
	- 숫자는 회색 바탕
	- 글자는 greenyellow
	- 1과 하나는 빨강 / 2와 둘은 파랑 / 3과 셋은 노랑 / 4와 넷은 초록
```javascript
<style>
        /* css에서 쓰는 selector*/
        div {
          border: 1px solid black;
          padding : 10px;
          margin : 10px;
          width : auto;
          height : auto;
          font-size: 30px;

          /* float : 영역 이외에 공간이 남으면 끌어올려서 원하는 방향으로 으로 붙이는 것 */
          float : left; 
          
        }

        div.num {
          background: gray;
          
        }
        div.char {
          background : greenyellow;
        }
        div.red {
          color: red;
        }

        div.blue {
          color : blue;
        }

        div.green {
          color : green;
        }

        div.yellow {
          color: yellow;
        }
      </style>
```
### CSS에서 바꾼 스타일 jQuery로 
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>
        $(function() {
          
          // num : 배경색을 회색
          // char : 배경색을 적당한 색
          // red, yellow, green, blue -> 글자색으로
          $("div.num").css('background', 'gray');
          $("div.char").css('background', 'orange');
          $("div.red").css('color', 'red');
          $("div.yellow").css('color', 'yellow');
          $("div.green").css('color', 'green');
          $("div.blue").css('color', 'blue');
          
        });
      
      </script>
      
      <style>
        /* css에서 쓰는 selector*/
        div {
          border: 1px solid black;
          padding : 10px;
          margin : 10px;
          width : auto;
          height : auto;
          font-size: 30px;

          /* float : 영역 이외에 공간이 남으면 끌어올려서 원하는 방향으로 으로 붙이는 것 */
          float : left; 
          
        }

        </style>
    </head>
    <body>
      <div class="num red">1</div>
      <div class="num blue">2</div>
      <div class="num yellow">3</div>
      <div class="num green">4</div>

      <div class="char red">하나</div>
      <div class="char blue">둘</div>
      <div class="char yellow">셋</div>
      <div class="char green">넷</div>

    </body>
</html>
```
이렇게 하면 색이 1000만개면 1000만개 다 한줄한줄 해줘야함 이렇게 하기 싫음! -> **Each** 사용!

### index와 item
- 422p
- **Each**
	- 여러개 Tag를 갖고와서 item에 넣어줌
```javascript
//each는 여러개 tag를 갖고와서 item에 갖고 오는 것
          console.log($('div.num'));
          $('div.num').each(function(index, item) {
            // console.log($(item).attr('class') 까지하면 class 속성값을 반홤함. num red, num blue ..이렇게 나옴.
            //substr을 이용해서 4번째부터(포함) color 이름만 빼옴
            console.log($(item).attr('class').substr(4));

          })
        });
```
**![](https://lh4.googleusercontent.com/ypPtVMxjYVCIQ6N_X1LGbcVILiNBjt8Nx-HmsakImiJ8fQnb-w8ugQ8L3Tzw27tr4fdgJLTsA83W7_QOehvCvzQNAjH-NVKh5_mSzGrvw18-4tu5nyUVIfUiHpS8WA7mYpkz7xun)** -> **![](https://lh6.googleusercontent.com/Z9xNDBGBcgkKOom2QbGyTI7U3cvMosXvBUrr39TRYcLIulSRRLgkhkzc4mAhHTkGD9qzej6OSvoPRGFn4qoabotxL4vPOSpqgYAasnG4aCXdSmPCR0BgdAX-1VwD9Kx7JOjMx-e_)**
```javascript
<script>
        $(function() {
          // jQuery에서 쓰는 selector
          //  $("div").css('background', 'blue');
          // num : 배경색을 회색
          // char : 배경색을 적당한 색
          // red, yellow, green, blue -> 글자색으로
          $("div.num").css('background', 'gray');
          $("div.char").css('background', 'orange');
          
          //1번 방법
          $("div.red").css('color', 'red');
          $("div.yellow").css('color', 'yellow');
          $("div.green").css('color', 'green');
          $("div.blue").css('color', 'blue');
          
          //2번 방법
          //each는 여러개 tag를 갖고와서 item에 갖고 오는 것
          console.log($('div.num'));
          $('div.num').each(function(index, item) {
            // console.log($(item).attr('class') 까지하면 class 속성값을 반홤함. num red, num blue ..이렇게 나옴.
            //substr을 이용해서 4번째부터 color 이름만 빼옴
            //substr 한개만 들어가면 그 위치부터 끝까지
            let color = $(item).attr('class').substr(4);
            $(item).css('color', color);
          })
        });
      
</script>
```
**![](https://lh5.googleusercontent.com/hAhKjsL2_EVzRsaiaTh4zq_PLbR9Na-A3Gv2JNRte1XAZt6BKdacKenc709IHZAU6qx6A9RD3ckjjnzYUXIvLye-ON3QWXyDaR71Tv9L6L_jyrzcOioqk_B8_KEvHPn1kkheSzh6)**

## 이벤트
- 16장
- 502p
- document 다 실행된 다음에 뜨는 것
- 이벤트들은 어떻게 처리하는가?
	- jQuery에서 이벤트 핸들링

### text 이벤트
```javascript
<script>
    //each는 여러개 tag를 갖고와서 item에 갖고 오는 것
    console.log($('div.num'));
    $('div.num').each(function(index, item) {
      // console.log($(item).attr('class') 까지하면 class 속성값을 반홤함. num red, num blue ..이렇게 나옴.
      //substr을 이용해서 4번째부터 color 이름만 빼옴
      //substr 한개만 들어가면 그 위치부터 끝까지
      let color = $(item).attr('class').substr(4);
      $(item).css('color', color);
    });

    //이벤트 핸들링
    //click 이벤트 감지하면 function함수 실행해 주세요
    $('div').click(function() {
      //이벤트를 받은 div가 갖고 있는 값을 value에 삽입
      let value = $(this).text(); 
      console.log(value);
    });
  });

</script>
```
- 마우스에 올린다음 클릭
**![](https://lh4.googleusercontent.com/xKL-yhXE5Ha0fopNUBZgjfKSdp5Q6EByC7I6uzfxqijpvTUsxWT4x9zO38Lu-zdVQEvEcv7oUVPOl5_uaO81aj2za0-priWzjyxeVqO4BbjPbQV9Ga2f7IrgraU797MzASsWEdAC)**

### 속성도 같이 출력
- `css('cursor', 'pointer')` 를 통해 화살표를 손동작으로 바꿔줌
- `attr('class')` 를 통해 속성값도 같이 출력
```javascript
<script>
    //each는 여러개 tag를 갖고와서 item에 갖고 오는 것
    console.log($('div.num'));
    $('div.num').each(function(index, item) {
      // console.log($(item).attr('class') 까지하면 class 속성값을 반홤함. num red, num blue ..이렇게 나옴.
      //substr을 이용해서 4번째부터 color 이름만 빼옴
      //substr 한개만 들어가면 그 위치부터 끝까지
      let color = $(item).attr('class').substr(4);
      $(item).css('color', color);
    });

    //이벤트 핸들링
    //click 이벤트 감지하면 function함수 실행해 주세요
    $('div').click(function() {
      //이벤트를 받은 div가 갖고 있는 값을 value에 삽입
      let value = $(this).text(); 
	  let  attr = $(this).attr('class');
	  console.log(value, attr);
    });
  });

</script>
```
**![](https://lh6.googleusercontent.com/1VSpnZ_eWMP93_WvcxRUMHMdgZh2Bt09EUNVtYZTzOCrbMfNfSNYSnKapeX58R66yh_KgxDOn40ellpw56voGC92XWRFEiy5qk0KtpVXqlCAvD1vF2xeCmA-Evg7wsxI5qzGvSXC)**
### 이제 화면에 출력해 보자
```javascript
<body>
	<div  id="disp"></div>
</body>
```
- `$('#input div')` 를 하면 input 밑의 div만 click 이벤트를 감지할 수 있도록 함
```javascript
<script>
     //each는 여러개 tag를 갖고와서 item에 갖고 오는 것
     console.log($('div.num'));
     $('div.num').each(function(index, item) {
       let color = $(item).attr('class').substr(4);
       $(item).css('color', color);
     });

     //이벤트 핸들링
     //click 이벤트 감지하면 function함수 실행해 주세요
     //'div' 에서 '#input div' 으로 바꿈 (disp div가 click event가 발생하지 않도록 하기위해서
     $('#input div').css('cursor', 'pointer').click(function() {
       //이벤트를 받은 div가 갖고 있는 값을 value에 삽입
       let value = $(this).text(); 
       let attr = $(this).attr('class');
       //console.log(value, attr);
       $('#disp').append(value, attr);
     });
   });
 
 </script>
<body>
   <div id="disp"></div>
   <div id="input">
     <div class="num red">1</div>
     <div class="num blue">2</div>
     <div class="num yellow">3</div>
     <div class="num green">4</div>

     <div class="char red">하나</div>
     <div class="char blue">둘</div>
     <div class="char yellow">셋</div>
     <div class="char green">넷</div>
   </div>
 </body>
```
**![](https://lh3.googleusercontent.com/sLPXoIBcdREnichmOARdPTeXyedGX7CJIujxnaIqT6Nl_7oqkNfoP6jkIpTwnQ8CdCqSIeEbtnvlyZUPPt1WRx2fF8VYl_-WFqEji5mR9mJDq44bAT1oFpagyXf2wWHx6ZtuJfa6)**

### div 박스 클릭하면 동일한 data가 있으면 다른 class의 박스를 숨김(hide) / 없으면 다른 class의 박스를 보임(show)
- body 수정
```javascript
 <body>
   <div id="disp"></div>
   <div id="input">
     <div class="no" data="1">1</div>
     <div class="no" data="2">2</div>
     <div class="no" data="3">3</div>
     <div class="no" data="5">4</div>


     <div class="ch" data="1">one</div>
     <div class="ch" data="2">two</div>
     <div class="ch" data="3">three</div>
     <div class="ch" data="4">four</div>
   </div>
 </body>
```
- script 수정
```javascript
<script>
	$(function() {
	  // div 박스 클릭하면 동일한 색깔 class의 박스가 있으면 숨김 / 없으면 보이기(단, 보이기시 num와 char class는 다르게 설정)
		$('div').click(function() {
			let  cls = $(this).attr('class');
			let  val = $(this).attr('value');

	    //현재 클릭된 div와 value가 같고 class가 다른 div 선택
	    //selector 만들어야함
	    //변수로 갖고 있는 값은 +val+ 처럼 사용
	    //.is() 상태 확인
	    let div = $('div[value="'+val+'"][class!="'+cls+'"]');
		/*
         if (div.is(':visible')) {
             div.hide();
         } else {
             div.show();
         }
         */
         div.toggle();
	  });
	});
</script>
```

### select 태그
- 502p 에 보면 change 이벤트 있음
``` javascript
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script>
        $(function() {
            $('select').change(function() {
                console.log("here");
            });

        });
    </script>
    <style>        
    </style>
</head>
<body>
    <select>
        <option value="">선택하세요.</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
        <option value="6">6</option>
        <option value="7">7</option>
        <option value="8">8</option>
        <option value="9">9</option> 
    </select>
    <div></div>
</body>
</html>

```
**![](https://lh3.googleusercontent.com/lhLLtm6piwXKO1o22Opmhnei6tdt2cmeGiiJmrGkGc3zzGNmKcC0R2RTw74xFH4sl-dTj_H21ADc3GX9g5hPT02frebHVP6tbPXa_SeCBT6ctcGd03gF69ulXuIr9yTlZaDXT2Es)**

- 값을 바꾸면 구구단이 append 됨. 이를 위해 append하기 전에 초기화 하는 작업 필요
```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script>
        $(function() {
            $('select').change(function() {
                console.log($(this).val());
                //text는 전체 값 다나옴(선택하세요. 1 2 3 4 5 ...)
                //쓰면 안됨.
                //console.log($(this).text());
                
                //초기화
                //$('div').text('');
                $('div').empty();

                let dan = $(this).val();
                for(let i = 1; i <= 9; i++){
                  //이거 구구단한 값을 <div></div>에 넣어야함
                  // $('div').append(`${$(this).val()} * ${i} = ${$(this).val() * i} <br>`);
                  $('div').append(`${dan} * ${i} = ${dan * i} <br>`);

                }
            });

        });
    </script>
    <style>        
    </style>
</head>
<body>
    <select>
        <option value="">선택하세요.</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
        <option value="6">6</option>
        <option value="7">7</option>
        <option value="8">8</option>
        <option value="9">9</option> 
    </select>
    <div></div>
</body>
</html>
```

### mouseover, mouseleave 이벤트 처리
- 430p
- 홀수번째, 짝수번째, first, last 등이 있음
#### div태그 내부에 마우스가 들어가면 배경색을 붉은색으로 변경 / 빠져나오면 원래 색으로 변경
- script
```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script>
        $(function() {
            // 홀수번째 : red
            // 짝수번째 : blue
            // 첫번째 : yello
            // 마지막 : green
            $('div:odd').css('background', 'red');
            $('div:even').css('background', 'blue');
            $('div:first').css('background', 'yellow');
            $('div:last').css('background', 'green');


            // div태그 내부에 마우스가 들어가면 배경색을 붉은색으로 변경/ 빠져나오면 원래 색으로 변경
            //odd, even : index 기준
            //1번
            // $('div').mouseover(function(){
            //     console.log('진입');
            // });

            // $('div').mouseleave(function() {
            //   console.log('진입');
            // });

            //2번
            $('div').mouseover(function(){
                console.log('진입');
            })
            .mouseleave(function() {
              console.log('진출');
            });


        });
    </script>
    <style>  
        div {
          width: 100px;
          height: 100px;
          border: 1px solid blue;
          float: left;
          margin: 20px;
        }      
    </style>
</head>
<body>

    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
</body>
</html>
```

- mouseover, mouseleave 시 동작 저장
```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script>
        $(function() {
            // 홀수번째 : red
            // 짝수번째 : blue
            // 첫번째 : yello
            // 마지막 : green
            $('div:odd').css('background', 'red');
            $('div:even').css('background', 'blue');
            $('div:first').css('background', 'yellow');
            $('div:last').css('background', 'green');


            let orgColor; //origin 색 저장
            //2번
            $('div').mouseover(function(){
                orgColor = $(this).css('background');
                console.log(orgColor);
                //event를 받은 그 element가 this
                $(this).css('background', 'black');
            })
            .mouseleave(function() {

              $(this).css('background', orgColor);
            });


        });
    </script>
    <style>  
        div {
          width: 100px;
          height: 100px;
          border: 1px solid blue;
          float: left;
          margin: 20px;
        }      
    </style>
</head>
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
</body>
</html>
```
원래 색
**![](https://lh5.googleusercontent.com/mLxhe2xzJxnWmSiYD1r0LwbfANQEAvhTICy2zEohfiF90WocZCn6UyDSiC0_vUveK8lBuHOrsv_rQiTkgL6jnzCIk0UZNmDsYu_F2qg-4wiQeqY6YvqMvqWFFMPz0rvFLcrmwjWa)**

mouse over시
**![](https://lh5.googleusercontent.com/TdBvGoMRV38vYMr_UkREkoxjbwN-H1jQGE8wX86PVZI7gYLS3a3YvJYZHi1gcNdzPjQiU7VfWty0B8GXuh8uJXZ3EQU0zfwF7khdDviOVRmjZh00ew_YAsvZ0g8JbgxnrT76_ri6)**

mouse leave시
**![](https://lh5.googleusercontent.com/mLxhe2xzJxnWmSiYD1r0LwbfANQEAvhTICy2zEohfiF90WocZCn6UyDSiC0_vUveK8lBuHOrsv_rQiTkgL6jnzCIk0UZNmDsYu_F2qg-4wiQeqY6YvqMvqWFFMPz0rvFLcrmwjWa)**

## $ 기호 선언 방지
- 441p, 13-42를 보면 나옴
- `$.noConflict();` : jQuery에서 `$`는 전역변수에 저장되어있는 `jQuery`를 뜻함
- 이때, `$` 기호가 jQuery를 대신하는 기호로 쓰지 않을 때가 있음. 이때는 `$` 기호의 중복사용을 막기 위해 `$.noConflict`하고 `var JJ=jQuery` 라고 선언하면 jQuery대신에 `JJ`를 사용할 수 있음 

## jQuery UI
**[https://jqueryui.com/](https://jqueryui.com/)**
- 일반적으로 웹사이트를 만들때 사용되는 **UI 기능**들을 쉽게 만들 수 있도록 제공해줌
- jQuery UI 설치
```shell
C:\>cd JavaScript
C:\JavaScript>npm install jquery-ui-css
```
**![](https://lh5.googleusercontent.com/dzK4_37byH9g8oX1xM3i89QH5v7Uk0H6EiUjudwxM7s4ud9E-nEJ3h0MDjCT8jPVewExb1XgR9zj9MYQBLe_B9STecIYjDAXrhK6PCk02Vy8sopRBvzta8MykaLr-8u6nPtqlsEj)**
이후 해당 jquery-ui 경로 추가
```
<script  src="/node_modules/jquery/dist/jquery.js"></script>
<script  src="/node_modules/jquery-ui-css/jquery-ui.js"></script>
<link  rel="stylesheet"  href="/node_modules/jquery-ui-css/jquery-ui.css">
```
**![](https://lh5.googleusercontent.com/prf2aEE2NrP2NR3Uf-CzWSBygll3bKMa3F1CBendhgBL6u7foJqNHkQseGj536PvbtDkZ-1D9GzieQ9WjMo-AzaJaM2AY1pVLQouoRGr3uuke7eTaIY2-_e-GxcZHV-RliZ-Sq86)**
```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>   
    <script src="/node_modules/jquery-ui-css/jquery-ui.js"></script>
    <link rel="stylesheet" href="/node_modules/jquery-ui-css/jquery-ui.theme.css">
    <script>
      $(function() {
        // , 는 multiful selector
        $("button, a").button();
      });
    </script>
    <style>  
        div { width: 100px; height: 100px; float: left; border: 1px solid red;}
        .red{background : red; }
        .blue{background : blue; }
    </style>
</head>
<body>
    <button>클릭하세요.</button>
    <a href="#">클릭하세요.</a>

    <div>1111</div>
    <div>2222</div>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>   
    <script src="/node_modules/jquery-ui-css/jquery-ui.js"></script>
    <link rel="stylesheet" href="/node_modules/jquery-ui-css/jquery-ui.theme.css">
    <script>
      $(function() {
        // , 는 multiful selector
        $("button, a").button();
      });
    </script>
    <style>  
    </style>
</head>
<body>
    <button>클릭하세요.</button>
    <a href="#">클릭하세요.</a>

    <div>1111</div>
    <div>2222</div>
</body>
</html>
```

### jquery-ui-css 사용
- style을 class, id 별로 관리 가능
```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>   
    <script src="/node_modules/jquery-ui-css/jquery-ui.js"></script>
    <link rel="stylesheet" href="/node_modules/jquery-ui-css/jquery-ui.css">
    <script>
      $(function() {
        // , 는 multiful selector
        $('div').mouseover(function() {
          $(this).attr('class', 'mycolor1');
        }).mouseleave(function() {
          $(this).attr('class', 'mycolor2');
        });
      });
    </script>
    <style>  
        /* div { width: 100px; height: 100px; float: left; border: 1px solid red;}
        .red{background : red; }
        .blue{background : blue; } */

        /* mycolor와 같은 class, id 들을 쫙 모아서 조합할 수 있도록 해주는 것임. 그것이 jquery-ui-css가 갖고 있는 값 */
        div { width: 100px; height: 100px; float: left; border: 1px solid red;}
        .mycolor1{background : red; }
        .mycolor2{background : blue; }
    </style>
</head>
<body>
    <div>1111</div>
    <div>2222</div>
</body>
</html>
```
**![](https://lh6.googleusercontent.com/ouOjUvmTGmhq9usrOAlto4LfBOClmAZPkCUIEgfXQ8NO00vIsNsnAT1oKvWN2vUtF6crK3J8rE2y0f9IbonC5VLhaQ9E3q907zKruxcnBC90SNyqjKdoXtqiUSjmnJ8pLD0Z2iML)**

## jQuery theme 사용
- jQuery UI 홈페이지 - Theme - 기본 Download - Stable(위에 링크) 클릭하면 다운 됨
- C:\JavaScript 밑에 압출 풀음
**![](https://lh6.googleusercontent.com/70uagewVB5lSEQ5hn1qo7p9e6IFFRPdRFUb2QoizSPVN8J_Z5E9x5vvV9F5-0t_Ckn-CYUB-Lql3XU9oenBvpwwvpHWLosDk81-dBggLUxDWuEcLMCvoWLGrEZ7i9BahKs6nvnEU)**

다운받은 후 위에 `node_module`에서 갖고온 css, .js 파일 바꾸기
```javascript
<link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">
<script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script> 
<script src="jquery-ui-1.12.1/jquery-ui.js"></script>
```
### jQuery-UI 에서 tabs 를 활용해 보자
```javascript
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">
    <script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script> 
    <script src="jquery-ui-1.12.1/jquery-ui.js"></script>

    <script>
      $( function() {
        $( "#tabs" ).tabs();
      } );
    </script>
    <style>  
       
    </style>
</head>
<body>
  <div id="tabs">
    <ul>
      <li><a href="#tabs-1">Nunc tincidunt</a></li>
      <li><a href="#tabs-2">Proin dolor</a></li>
      <li><a href="#tabs-3">Aenean lacinia</a></li>
    </ul>
    <div id="tabs-1">
      <p>Proin elit arcu, rutrum commodo, vehicula tempus, commodo a, risus. Curabitur nec arcu. Donec sollicitudin mi sit amet mauris. </p>
    </div>
    <div id="tabs-2">
      <p>Morbi tincidunt, dui sit amet facilisis feugiat, odio metus gravida ante, ut pharetra massa metus id nunc. </p>
    </div>
    <div id="tabs-3">
      <p>Mauris eleifend est et turpis.</p>
      <p>Duis cursus. Maecenas ligula eros, blandit nec, pharetra at, semper at, magna.</p>
    </div>
  </div>
</body>
</html>
```
**![](https://lh5.googleusercontent.com/zUQpP92RcdqJWjMAtQ4h8-CvolOJZ5ZbqAbjagUs_jOkfTv-kqQ03zTbAEvzaDZZ91RXKFFVbUsUq9lZMB9qH8US5lwGTcodj8FJ2a9TJDf1f5OtfmpggSa3IXDOmOeEmGveU4v_)**

### dialog도 해보자
```javascript
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">
    <script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script> 
    <script src="jquery-ui-1.12.1/jquery-ui.js"></script>

    <script>
      $( function() {
        $( "#tabs" ).tabs();

        $( 'input[name="userid"]').focusout(function() {
          if ($(this).val() == ""){
            //alert("아이디를 입력하세요");
            //jQuery 라이브러리에서 제공해주는 dialog
            $("#dialog").dialog();
          }
        });

      } );
      
    </script>
    <style>  
       
    </style>
</head>
<body>
  <!-- tabs id -->
  <div id="tabs">
    <ul>
      <li><a href="#tabs-1">Nunc tincidunt</a></li>
      <li><a href="#tabs-2">Proin dolor</a></li>
      <li><a href="#tabs-3">Aenean lacinia</a></li>
    </ul>
    <div id="tabs-1">
      <p>Proin elit arcu, rutrum commodo, vehicula tempus, commodo a, risus. Curabitur nec arcu. Donec sollicitudin mi sit amet mauris. </p>
    </div>
    <div id="tabs-2">
      <p>Morbi tincidunt, dui sit amet facilisis feugiat, odio metus gravida ante, ut pharetra massa metus id nunc. </p>
    </div>
    <div id="tabs-3">
      <p>Mauris eleifend est et turpis.</p>
      <p>Duis cursus. Maecenas ligula eros, blandit nec, pharetra at, semper at, magna.</p>
    </div>
  </div>

  <label>아이디</label>
  <input type= "text" name="userid"/>
  <div id="dialog" title="알림">
    <p>아이디를 입력하지 않았습니다.</p>
  </div>
</body>
</html>
```

-> 코드 확인해봐라

### Toast.js 적용
**[https://ireade.github.io/Toast.js/](https://ireade.github.io/Toast.js/)**

- 다운로드
```shell
C:\JavaScript>npm install jquery-toast-plugin
```
- Xcode에 script 추가
```
<script src="node_modules//jquery-toast-plugin/dist/jquery.toast.min.js"></script>
<link rel="stylesheet" href="node_modules/jquery-toast-plugin/dist/jquery.toast.min.css">
```
- dialog 대신 toast 라이브러리 사용
```javascript
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">
    <script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script> 
    <script src="jquery-ui-1.12.1/jquery-ui.js"></script>
    <script src="node_modules//jquery-toast-plugin/dist/jquery.toast.min.js"></script>
    <link rel="stylesheet" href="node_modules/jquery-toast-plugin/dist/jquery.toast.min.css">

    <script>
      $( function() {
        $( "#tabs" ).tabs();

        $( 'input[name="userid"]').focusout(function() {
          if ($(this).val() == ""){
            //alert("아이디를 입력하세요");
            //jQuery 라이브러리에서 제공해주는 dialog
            //$("#dialog").dialog();
            $.toast({
              text : "아이디를 입력하세요.",
              showHideTransition : 'fade',
              bgColor : '#E01A31'
            });
          }
        });

      });
      
    </script>
    <style>  
       
    </style>
</head>
<body>
  <!-- tabs id -->
  <div id="tabs">
    <ul>
      <li><a href="#tabs-1">Nunc tincidunt</a></li>
      <li><a href="#tabs-2">Proin dolor</a></li>
      <li><a href="#tabs-3">Aenean lacinia</a></li>
    </ul>
    <div id="tabs-1">
      <p>Proin elit arcu, rutrum commodo, vehicula tempus, commodo a, risus. Curabitur nec arcu. Donec sollicitudin mi sit amet mauris. </p>
    </div>
    <div id="tabs-2">
      <p>Morbi tincidunt, dui sit amet facilisis feugiat, odio metus gravida ante, ut pharetra massa metus id nunc. </p>
    </div>
    <div id="tabs-3">
      <p>Mauris eleifend est et turpis.</p>
      <p>Duis cursus. Maecenas ligula eros, blandit nec, pharetra at, semper at, magna.</p>
    </div>
  </div>

  <label>아이디</label>
  <input type="text" name="userid"/>
  <div id="dialog" title="알림">
    <p>아이디를 입력하지 않았습니다.</p>
  </div>
</body>
</html>
```
**![](https://lh5.googleusercontent.com/c5A5xINjfVNirIboxgoeAwj_14cYI32YGsQa3eYxf0O9rNvjUPk9Wrcg9ZZDUvhGNXtckrttEhqBjLxErJJbNb42TkIN1qeddofE4-lfKgWnBzVoPwTKiRDMEvc0gA2Ijtprt3FV)**

## 외부 라이브러리 사용하는 방법
### colorbox plugin
- 558p
- **[https://www.jacklmoore.com/colorbox/](https://www.jacklmoore.com/colorbox/)**
	- npm 제공
	- colorobx 설치
	```shell
	C:\JavaScript>npm install jquery-colorbox
	```
시작 코드
```javascript
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">
    <script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script> 
    <script src="jquery-ui-1.12.1/jquery-ui.js"></script>

    <script>
      $( function() {
        
      });
      
    </script>
    <style>  
       
    </style>
</head>
<body>
  
</body>
</html>
```

- script 추가
```javascript
<script  src="node_modules/jquery-colorbox/jquery.colorbox.js"></script>
<link  rel="stylesheet"  href="node_modules/jquery-colorbox/example1/colorbox.css">
```

- 코드 추가
	- colorbox()를 통해 파일 보여줌
	```javascript
	<!DOCTYPE html>
	<html>
	<head>
	    <link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">
	    <script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script> 
	    <script src="jquery-ui-1.12.1/jquery-ui.js"></script>

	    <script src="node_modules/jquery-colorbox/jquery.colorbox.js"></script>
	    <link rel="stylesheet" href="node_modules/jquery-colorbox/example1/colorbox.css">
	    <script>
	      $( function() {
	        //팝업 처럼 보여줌
	        $('a').colorbox();
	      });
      
	    </script>
    <style>  
       
    </style>
	</head>
	<body>
	  <a href="node_modules/jquery-colorbox/content/daisy.jpg">데이지</a>
	  <a href="node_modules/jquery-colorbox/content/homer.jpg">호머</a>
	</body>
	</html>
	```
**![](https://lh6.googleusercontent.com/GB0vnBAjzJiLJjPxQFoA4BAVXKXz-sFlJVoF7XGo71R2OSHBftrBsnKSzzoFUMA_mPgt-I6FRnXf_PIToPFmxyTlawm48Vndgnkvepa7th8rV8LVB-maa7poCquhPGJGKdiOqiNk)**
**![](https://lh4.googleusercontent.com/oDz8eSd_1jXJbEj8cRa9-kU4YNfJ9X2lDZoYKpJzUsbn6KD9Em8sP4oEb6UASOxHaklcvmNJSg9WQMGl_xKXp6jJ_ZiLxQPYrNGKdrXkAVdaG4vKVc1rPYI-TAKHLBFgwX-EYR02)**
## Ajax 통신
- **비동기** 통신
- 636p
	- 옛날에 웹이라는 것은 브라우저에서 링크, 버튼 누르면 새로운 문서 전체를 보내줌 
		- 페이지 나누어서 보여줌
		- 옛날에는 **html 문서**가 서버에서 옴
	- 사용자의 화면은 계속 유지되고 요청받는 것 서버에서 받아 보여주는 방식이 **비동기 방식**
		- 스크롤하면 계속해서 보여줌
		- 이런 통신 방식 **Ajax통신**(javaScript를 이용한 비동기 통신방식)
		- 화면에 보여줄 **data**만 오면됨. 그래서 넣어주는 방식만 알면됨. 그것을 **DOM Script**라고 말함
- 웹 2.0
	- **DOM Script** + **Ajax 통신**
- 지금은 당연히 해야하는 기술

### 데이터 전송 형식
- 637p
- `csv`
	- 콤마를 기준으로 값 전달
	- 문제점
		- 내용에 `,`가 포함되면 문서가 밀림
		- 데이터 의미도 구분하기 힘듦
- `XML` 형식
	- 데이터를 XML로 나누는 것
	- 태그를 가지고 데이터를 기술
	- CSV보다 해당하는 데이터가 어떤 의미인지 알 수 있음
		- 순서도 바뀌어도 됨
		- 대신,  복잡해 보임(태그가 교차되면 안되고, 포함관계 지켜야하고..등등)
- `JSON`
	- 기존에 있던 XML보다 조금 더 쓰기 간편, 직관적
### Node
- 631p
- Client에서 javaScript를 이용해 ajax라는 통신기법을 사용해서 서버쪽으로 데이터를 요청할때 서버가 Client에게 줌. 
 우린 더 나가기 어려우니 서버에서 정적인 데이터를 줄 수 있도록 하겠다.

#### 화면 순서
- 일반적으로 Clinet(PC/모바일)에 브라우저 앱이 있다고하면 Web Server가 있을 것임
- 만약 조회 페이지가 있다. 하면 Client는Server에 화면을 요청할 거야
-  그 데이터는 HTTP 요청을 통해서 ajax 통신을 통해 갈 것임. 거기에서 데이터가요청하는 것을 줘야함. 연산을 하던지 Server에서는 DB에 접근할텐데 DB-Server-Client 로갈때 Client와 Server 이 통신은 JSON형식의 Ajax 통신을 이용했을 가능성이 높음

### 우린 Node 사용하지 않고 구현
1. `students.json`파일 생성
	```json
	{
	    "students" :
	    [  
	        { "name" : "홍길동", "age" : 23, "score" : "A+" },
	        { "name" : "길동홍", "age" : 32, "score" : "B+" },
	        { "name" : "동홍길", "age" : 43, "score" : "C+" }
	    ]
	}
	```
	- http://localhost:8080/students.json 되는지 확인
2. `template.html`
```javascript
<!DOCTYPE html>
<html>
<head>

    <script src="/node_modules/jquery/dist/jquery.js"></script>

    <script>
      $(function() {
        $('button').click(function() {
          // console.log("A")
          $.ajax({
            //url : 서버로 요청하는 주소
            url: "http://localhost:8080/students.html",
            //data: { userid: "aaa", usrpw: "bb" } 이렇게 추가해도 됨
            //type : 요청 방식(get, post 등)
            type: "GET",
            dataType: "json"
          })
          .done(function(res){  //res = response 
            console.log("B")
            console.log(res);
            console.log(res.students);
            res.students.forEach(student => {
              console.log(student);
              console.log(student.name);
              let x = `
                <tr>
                    <td>${student.name}</td>
                    <td>${student.age}</td>
                    <td>${student.score}</td>
              `;
              $('table').html($('table').html() + x);
            });
          });
        });
      });
      
      
    </script>
    <style>  
       
    </style>
</head>
<body>
  <button>가져오기</button>
  <table border=1>

  </table>
</body>
</html>
```
**![](https://lh4.googleusercontent.com/Ak7REbI5clk1qQ-CgI31wA1oHD-epoyc8WWpZDZWGMwDtmNtRMhNcoWjzFU1yrmD5irf21pk6U0VJ4kqpXLnrryMSOXbYlF9ilfmHY1dX31l6iDDKNbGyNCgdx8CDmAgOl-Lefop)
**
	- 서버 no-cache로 실행 : `npx http-server -c -1`
	- json도 no-cache로 실행하고 싶으면 : `students.json`을 `students.html`로 바꾸기
	- 실행할때 안하고 싶으면 `개발자 모드`에서 `Network` 탭 들어가서 해당파일 오른쪽 선택 후  `Clear browser cache`
	- **![](https://lh5.googleusercontent.com/fh6NmXd9DvyaEx1V_v_0KSCSRihys1JlZuQ0leidhykYQPgbHBM_ZrQH9Jk0xrymxfZzFLN9_lmGf3uFeybpRu_W8ZMCsVf2k9BikJ6u2IQWLdpB0H1Gcuh6oPXQfRLSs4K3SP1K)**
3.만약 jquery안쓰면 711p에서 쓰는 것처럼 해야함
