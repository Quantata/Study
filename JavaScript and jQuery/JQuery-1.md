
# JQuery
- 굉장히 방대. 그래서 필요한 내용들을 어떻게 찾는지에 초점을 맞출 것
- JQuery 홈페이지가 제일 좋음
	-[JQuery 다운로드]([https://jquery.com/download])
- 무료로 사용가능한 오픈소스 라이브러리
- 목적
	- 문서 객체 모델과 관련된 처리를 쉽게 구현
	- 일관적 이벤트 연결을 쉽게 구현
		- 마우스가 올라왔으면 올라왔다 벗어났으면 벗어났다 등
		- 어떤 행위가 발생하면 나에게 알려주는 것 **이벤트**
		- 브라우저마다 약간 달랐는데 이걸 통합
	- 시각적 효과 쉽게 구현
		- style이란 것을 다루어야 하는데 이것을 쉽게 구현할 수 있도록 함.
	- ajax 애플리케이션 쉽게 개발
		- ajax는 화면이움직이는게 아니고 javascript를 이용해서 내가 서버쪽으로 요청. 서버 쪽에서는 javascript에 대한 응답을 주는데 data만 서버에서 만들어서 줌. 그것을 가능하게 만드는 것이 **ajax**
		- 웹 2.0 ( ajax와 DOMTOL을 이용한 렌더링 기술이 메인 트렌드 )

## JQuery 설치 방법
-  CDN 서비스(Content delivery network)
```javascript
<!DOCTYPE html>
<html>
    <head>      
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    </head>
    <body>
    </body>
</html>
```
**![](https://lh5.googleusercontent.com/FBY4D82QgpOZCUuSjrPmbNMyZnW6X-JEkczxhfHTisdrfCFld1HmMXxscJTGIKO3ycEFvUH_cbp68IoyZeAIS82ilQu-f7JjGBHz-dWqNetw7eENFkQ_2MP67J8aGf7ruZOSUBHJ)**

- 직접 다운로드
	- cmd에 작업 디렉토리에서
		```javascript
		npm install jquery
		```
	- 이후 사용할 수 있도록 넣어주면 됨
		```javascript
		<!DOCTYPE html>
		<html>
		    <head>
		       <script src="/node_modules/jquery/dist/jquery.js"></script>
		    </head>
		    <body>
		    </body>
		</html>
		```
		**![](https://lh4.googleusercontent.com/qnT75W6V6y7dnSDOMfVeVTv5qvKqEBjPw9IGxte55HcDg3tge-oBXVUU--FzK8Ks9-sIoA2Gqq0YGna0yRo2PNar0yXMjEFMI_PjoG4NtgyGhkjvQw6mtIa6dJMeCptiOSZkMYkI)**

## JQuery 사용방법
- 417p
- `window(객체).jQuery(속성) = window.$ = jQuery`
	- 윈도우의 JQuery는 윈도우의 `$`가 되는 것이고 이것이 JQuery다
- 


### 문서가 로딩이 다 되면 body에다가 어떤 내용 찍어주고 싶음
```javascript
//문서가 준비되면 매개변수로 전달한 콜백 함수를 실행하라
        //window.onload와 같은
        $(document).ready(function() {

            console.log("hello JQuery");
            $("body").text("Hello JQuery");

        });
```

## 선택자
- `selector`(선택자) : 위치 찾아주는 것
	- 문서 객체 모델(DOM)에서 특정 위치를 지정(선택)하기 위한 방법
	- css의 selector와 거의 유사함
	- 종류
		- `$("*")` : 전체 선택자
		- `$(".class")` : 클래스 선택자
		- `$("#id")` ; 아이디 선택자
		- `$("element")` : 요소(태그, element 선택자)
		- `$("selector1, selector2, … , selectorN")` : 다중 선택자(multiple selector)

- block 요소
	- `<p>` : 한줄에 하나
	- `<sapn>` : 뒤에 붙음

### 후손 선택자
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>

      //$ 는 jQuery와 같은 값임.
      $(function() {
        //모든 요소 가져와서 css적용
        $("*").css('color', 'red');
      });
      </script>

    </head>
    <body>
      <h1>제목1</h1>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
      <h1>제목2</h1>
      <p>내용2내용2내용2내용2내용2내용2내용2내용2내용2</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/dzTMrkSBUjdlsTDB8-jOt71Btl02SZXWo2sC63pRpCxxBeUt0N_vBGhnLgA_pjXApEA-vFpatVIxY-4V8iK60moV9GlblGOF9CJuYAWuotOZ-dWAGfCHMcem7L0twStY7PWssiyW)**
**![](https://lh3.googleusercontent.com/7x13Venu0Zzy9wkFcQ_0Ic8Mwdsw1nM8M5CdFipWFYQtRFhiq2osEteUbxbX85SnAyIPgz9hmnrjkjeG1HzLjcMXmLy3OwJc44Zxv0ctjVbwlZqQk5wG4ktflzwTEEFPrIt8VNKE)**
모든 요소에 color : red 붙음

- 만약 body 안에 있는 것에만 빨간색 속성 넣고 싶으면?
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>

      //$ 는 jQuery와 같은 값임.
      $(function() {
        //모든 요소 가져와서 css적용
        $("body *").css('color', 'red');
      });
      </script>

    </head>
    <body>
      <h1>제목1</h1>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
      <h1>제목2</h1>
      <p>내용2내용2내용2내용2내용2내용2내용2내용2내용2</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
    </body>
</html>
```
**![](https://lh6.googleusercontent.com/GhiG3J5CdHR6wiYI83Cw60CUDgqKdPW7i7UyWuM73qVPghNdkKR0n77z32yidita1CZXP2rW-PRyd5y7XIdTx5wxKH3jWuJug-uppwgJvOGgmmoypoHTPLznitl-P7PjSGMlhVoy)**
- **$** : 후손 선택자

### 태그 선택자
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>

      //$ 는 jQuery와 같은 값임.
      $(function() {
               //후손 선택자
        $("body *").css('color', 'red');

        //h1 태그에 대해서 배경색을 부여
        //요소 선택자
        $("H1").css('background', 'yellow');
      });
      </script>

    </head>
    <body>
      <h1>제목1</h1>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
      <h1>제목2</h1>
      <p>내용2내용2내용2내용2내용2내용2내용2내용2내용2</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/l4c_NSV2gQIk_ASRoycXA1RcUFhpK2Rk92p5pNU22xCysNLLOi5DuWz8RU8abNpxyeU2eSwSXkFcnDEOCb2Sly7zIH_9vbG0OEXVjfBVSUVkSfgpubmzeAILwy2j20lwE4Oi67WY)**

### id 선택자
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>

      //$ 는 jQuery와 같은 값임.
      $(function() {
       
        //후손 선택자
        $("body *").css('color', 'red');

        //h1 태그에 대해서 배경색을 부여
        //요소 선택자
        $("H1").css('background', 'yellow');

        //ID 선택자
        $("#title").css('border', '1px solid red');
      });
      </script>

    </head>
    <body>
      <h1>제목1</h1>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <span>다른 내용</span>
      <span>다른 내용</span>

      <h1 id="title">제목2</h1>
      <p>내용2내용2내용2내용2내용2내용2내용2내용2내용2</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
    </body>
</html>
```
**![](https://lh6.googleusercontent.com/MNNX1wBcqU8Pi4lQJFL81voDhYZWNaLPB20OxDWX68WgjeIMZjc6EPXUtnGwBSoEb6NH31DzqAl7isktAwQ_D42QEhfYJPzixb0Wt2DIT7uevGDFOyyv5EkiNQem_dYU5kACMOTe)**

### class 선택자
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>

      //$ 는 jQuery와 같은 값임.
      $(function() {
       
        //후손 선택자
        $("body *").css('color', 'red');

        //h1 태그에 대해서 배경색을 부여
        //요소 선택자
        $("H1").css('background', 'yellow');

        //ID 선택자
        $("#title").css('border', '1px solid red');

        //class 선택자
        $(".right").css('textAlign', 'right');
      });
      </script>

    </head>
    <body>
      <h1 class="right">제목1</h1>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <span>다른 내용</span>
      <span>다른 내용</span>

      <h1 id="title">제목2</h1>
      <p class="right">내용2내용2내용2내용2내용2내용2내용2내용2내용2</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
    </body>
</html>
```
**![](https://lh5.googleusercontent.com/yG75kL3m9Gjaoibx4wtdGRujM6gHucFJT2897gCsx71ylAn6ITxm7gxNF1Xo5101ihcjGjKCrSmC1GlLdJe65AOWXPXlLrUJssgo_P5NC7Dn765Lz8iAiDDAJiRDtGvw9XssjnRw)**

### 다중 선택자
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>

      //$ 는 jQuery와 같은 값임.
      $(function() {
       
        //후손 선택자
        $("body *").css('color', 'red');

        //h1 태그에 대해서 배경색을 부여
        //요소 선택자
        $("H1").css('background', 'yellow');

        //ID 선택자
        $("#title").css('border', '1px solid red');

        //class 선택자
        $(".right").css('textAlign', 'right');

        //다중 선택자
        $("span, #title, .right").css('text-decoration', 'underline');
      });
      </script>

    </head>
    <body>
      <h1 class="right">제목1</h1>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <p>내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1내용1</p>
      <span>다른 내용</span>
      <span>다른 내용</span>

      <h1 id="title">제목2</h1>
      <p class="right">내용2내용2내용2내용2내용2내용2내용2내용2내용2</p>
      <span>다른 내용</span>
      <span>다른 내용</span>
    </body>
</html>
```
**![](https://lh4.googleusercontent.com/IE7vp3QsQeQ8Gt8O2BQ_MZ5sKVSrj_4SD5iuw8UAr4fzFeupcRmgz3jenoIC5hl8Ne2epH2TomfRmBoB3OS16hqUsUu6xSXN9z-eEl_HyNYxHPGhaixtlQrXROm3XtJ3bnE3oozT)**
지금 까지 **기본 선택자**

### 자손(자식) 선택자, 후손 선택자
-  423p
- https://api.jquery.com/shild-selector
- 자식 선택자
	- `$("parent > child")`
- 후손 선택자
	- `$("parent child")`
	
**![](https://lh6.googleusercontent.com/oMumPKE7rfmwsgISBylQxXi7mkcQ3V0M0gv8TFl6l3JIk49xxavhzHRr3P58_O89CWnH36rkrm4s4jfdym218jV2BLzaC4Zm65CchtRXHgbFwuW4cpOE93EAN3txNXCPTPV_9JNb)**
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>
        $(function() {
            // ID가 menu인 ul 태그 아래에 있는 모든 li 태그값 색을 파란색으로 설정, 후손
            $("ul#menu li").css('color', 'blue');
            // ID가 menu인 ul 태그 바로 아래에 있는 li 태그 값에 대해 밑줄을 출력 -> 하려 했으나 상속ㅠ_ㅠ
            //$("ul#menu > li").css('text-decoration', 'underline');
            //자식 
            $("ul#menu > li").css('border', '1px solid red');

        });
      
      </script>

    </head>
    <body>
      <div>
        <ul id ="menu">
          <li>첫번째</li>
          <li>두번째</li>
          <li>세번째
            <ul>
              <li>3-1</li>
              <li>3-2</li>
              <li>3-3</li>
            </ul>
          </li>
          <li>네번째</li>   
        </ul>
      </div>
    </body>
</html>
```
**![](https://lh5.googleusercontent.com/y9wg2HLQvueR1KJ_c-8XD8uxGbQUYG2kf-sdhbNVv75WedzJmnOxxJhxCkJlzb00wQlddvNWfJxS6sywuUvI3f2UrwdZuvURev_fl9PHGlcopOhLyQeJcOlK-D0ChiO2i6ywDLYk)**

### 속성 선택자
- 속성
	- 태그가 있으면 `<태그명 속성명="속성값" 속성명="속성값>태그값</태그명>`
	- 이때 `태그`를 `element`
	- `속성`을 `attribute`
		- id, class 등도 속성. 근데 얘네는 의미가 있어서..?
	- id도 지정해서 색 바꿈 가능
- 속성 선택자는
	- `$("엘리먼트이름[속성이름='속성값']")`
	- \<from> 아래에서 사용하는 사용자 입력을 처리하는 태그를 제어할때 사용
	- input인데 타입이 radioButton인것, input인데 타입이 text인 것 처럼 input 타입이 다 다름. 이때 속성 선택자 사용
		- input인데 타입이 text인것은 `$("input[type='text']")` 이렇게 씀.
```javascript
<!DOCTYPE html>
<html>
    <head>
      <script src="/node_modules/jquery/dist/jquery.js"></script>
      <script>
        $(function() {
          //속성 선택값
          //<from> 아래에서 사용하는 사용자 입력을 처리하는 태그를 제어할때 사용
           $('ul[id="submenu"] li').css('color', 'red');
           $('ul#submenu li').css('background', 'yellow');           
        });
      
      </script>

    </head>
    <body>
      <div>
        <ul id ="menu">
          <li>첫번째</li>
          <li>두번째</li>
          <li>세번째
            <ul id="submenu">
              <li>3-1</li>
              <li>3-2</li>
              <li>3-3</li>
            </ul>
          </li>
          <li>네번째</li>   
        </ul>
      </div>
    </body>
</html>
```

