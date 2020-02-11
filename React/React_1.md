# jQuery 복습
## 선택자 
- `$("무엇")`

## 메소드(값 & 화면을 제어)
- `.css('color', 'blue')`
- `.text(값)`
- `.html(값)`
	- html 속성이 들어감
- `.attr('속성이름', '행위')`
- `.val()`
	- value에는 \<input>, \<textarea>, \<select> 등

> 이 메소드들은 만약 선택자가 선택한 것이 \<div> 태그였다면 \<html>의 \<div> 태그 안에 속성값으로 color가 들어가든, 값이 들어가든 하게 해줌

## 복수의 값제어
- `each(function(index, item){})`

##  클릭
- `.click(function(){...})`
- `.change(function(){...})`

이 뒤에는 갖다 쓰는 것
## UI plugin
- `$("div").tab();`
- `$("div").dialog();`
- 해당하는 사이트에 가서 파일을 다운받아서 프로젝트에 넣으면 됨. 대부분 npm기반 `npm install [해당하는 모듈명]` 해서 갖고 와서 `<script src="/node_module/.../.js></script` 넣어주고 대부분 style이 같이옴 이때 `<link ref="stylesheet" href="...">`

여기까지는 화면 뒤에는 통신
## $.ajax
- 서버에 요청해서 갖고 올때 통신방법에 ajax를 사용. javascript를 이용한 비동기 통신을 ajax라 하고 서버에서 클라이언트에 데이터를 주는 형태는 json(javascript객체모델)을 많이 씀

# 갑분 jQuery로 LAB 만들기
```
사이트 미리 보기를 제작

-   jquery UI에서 제공하는 TAB 위젯을 이용
-   미리 보기 사이트 명과 주소(URL)은 ajax 통신으로 가져오기
-   /preview.html ⇒ 미리 보기 사이트
-   /siteinfo.html ⇒ 미리 보기 사이트 명과 주소를 포함한 JSON 형식의 파일
```
풀이
`<siteinfo.html>` 파일
```json
//siteinfo.html
{
    "sites" :
    [  
        {"name" : "네이버", "url" : "http://www.naver.com"},
        {"name" : "다음", "url" : "http://www.daum.net"},
        {"name" : "구글", "url" : "http://www.google.com"}
    ]
}
```
`<preview.html>` 파일
```javascript
//preview.info
<!DOCTYPE html>
<html>
<head>

    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
    <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>

    <script>
      $(function() {
	    // 탭 위젯을 생성
		$('tabs').tabs();
		
        $.ajax({
            //url : 서버로 요청하는 주소
            url: "http://localhost:8080/siteinfo.html",
            //data: { userid: "aaa", usrpw: "bb" } 이렇게 추가해도 됨
            //type : 요청 방식(get, post 등)
            type: "GET",
            dataType: "json"
          })
          //.done(data => { });
          .done(function(res){  //res = response 
            console.log(res);
            console.log(res.sites);

            for(let index in res.sites){
                //class 안 넣었다면 후손 및 자손 선택
                //$('#tabs > ul > li > a').eq(0)

                //제목 가져오기
                let x = res.sites[index];
                
                //$('#tabs > ul > li > a').eq(index).text(x.name); // 방법1
                $('.title').eq(index).text(x.name);

                $.ajax({
                    url : x.url,
                    dataType : "html"
                })
                .done((html) => {
                    
                    //$('#tabs > div').eq(index).html(html);    //방법1
                    $('.content').eq(index).html(html); //방법2
                })
            }
            
          });
        /*
        $('#tabs').tabs().click(function() {
           console.log("A")

        });
        */
     });
      
      
    </script>
    <style>  
       
    </style>
</head>
<body>
    
    <div id="tabs">
        <ul>
          <li><a href="#tabs-1" class="title">Nunc tincidunt</a></li>
          <li><a href="#tabs-2" class="title">Proin dolor</a></li>
          <li><a href="#tabs-3" class="title">Aenean lacinia</a></li>
        </ul>
        <div id="tabs-1" class="content">
          
        </div>
        <div id="tabs-2" class="content">
            
        </div>
        <div id="tabs-3" class="content">
            
        </div>
      </div>
</body>
</html>
```

**ON**
```javascript
//전체문서에 대해서 a 태그에 click이 생기는지 확인.
$('#tabs').on('click', 'a', function() {
	let  href = $(this).attr("href");
	console.log(href);
})
```

**동적으로 생긴 contents에 대해 이벤트 붙인 것**(on)
**강사님 `preview.html` 코드**
```javascript
<!DOCTYPE html>
<html>
<head>
    <!-- 필요한 JS 파일과 CSS 파일을 임포트 -->
    <script src="jquery-ui-1.12.1/external/jquery/jquery.js"></script>
    <script src="jquery-ui-1.12.1/jquery-ui.js"></script>
    <link rel="stylesheet" href="jquery-ui-1.12.1/jquery-ui.css">

    <!-- 처리 기능 -->
    <script>
        $(function () {
            //   서버로부터 미리보기(이름, 주소) 정보를 가져와서 출력
            //   참조 => https://api.jquery.com/jquery.ajax/
            $.ajax({
                url: "http://localhost:8080/siteinfo.html",
                /* type: "get", */
                dataType: "json",
            })
            /* 정상적인 경우 */
            .done(data => {
                data.sites.forEach(site => {
                    let name = site.name;
                    let url = site.URL;
                    /* 서버로부터 전달받은 데이터를 이용해서 화면을 구성 */
                    let id = $('li').length + 1;
                    let li = `<li><a href="#tab${id}" url="${url}">${name}</a></li>`;
                    let div = `<div id="tab${id}">탭 내용 ${id}</div>`;

                    $('#tabs > ul').append(li);
                    $('#tabs').append(div);
                });   
                
                //   탭 위젯을 생성
                $('#tabs').tabs();
            })
            /* 예외가 발생한 경우 */
            .fail(function (jqXHR, textStatus, errorThrown) {
                console.log(errorThrown);
            });

            /*
            $('a').click(function() {
                let href = $(this).attr("href");
                console.log(href);
            });
            */
            $('#tabs').on('click', 'a', function() {
                let href = $(this).attr('href');
                let url = $(this).attr('url');
                $(href).load(url);
            });
            
        });
    </script>
</head>
<body>
    <!-- 탭 UI를 적용할 태그 -->
    <div id="tabs">
        <!-- 탭 제목 -->
        <ul>
        </ul>
        <!-- 탭 본문 -->
    </div>
</body>
</html>
```
**![](https://lh4.googleusercontent.com/LuaWoOwQE7-kjP2AeiHVytlaN-cvjxoQ8NFEqUS2uUmZmqhrSOdPAwlp8rslA4vlD4U2OGhh2pED0rCfPVDgMdJypscJPG9c65ZWDkXkdPbWixZXHTu7-iUdtZm2Td1Zos7MUZoG)**

### CORS란?
- 이전에 웹이라는 것은..!
	- 교차 자원 요청(cross resource sharing)이 가능하다
	- 내 파일에서 네이버를 요청함. 껍데기는 naver에서 갖고 왔지만 문서 안에 있는 이미지는 이미지라는 태그(img src)를 통해 새롭게 가져오는 것. 문서에 포함된 그 이미지가 naver.com에서 가져 올 수도 있고 아니면 다른 사이트에 있는 것을 가져올 수도 있음. main.jsp를 제공한 naver에서 갖고 올수도 있고 jquery.com에서도 가져올 수 있음. 웹은 기본철학이 공유이기 때문에 어떤 화면을 보여주는데 필요로하는 resource가 짜집기해서 보여줄 수 있다. (교차 자원 요청) 이게 기본 철학
	- 근데 보안때문에 딱 한군데 막혀있음. 그게 뭐냐면 javascript를 이용해서 다른 곳에서 가져온 자원은 쓸 수 없도록 만들어 놓음. `SOP(Same Origin Policy, 동일 기원(출처) 정책)` 
- Origin
	- 스킴 + 호스트 + 포트
	- 이게 같으면 Same Origin
	- 다르면 동일 출처가 아님
- main.jsp는 naver.com에서 80 포트를 가지고 내려온 문서임. 내꺼에서 main.jsp의 이미지를 갖고 올때는 http://abc.com/xyz.gif 에서 갖고올 수 있음. 웹에서는 다른 주소라도 괜찮은데 javascript를 이용해서 갖고올때는 동일출처가 아니기 때문에 안됨!!
- ajax는 XMLhttp Request(XHR)가 근본 기술임. 웹이라는 것은 교차자원요청이 가능하나 javascript를 이용해서(XHR 자원) 갖고오게하는건 금지되어있다 
- 근데 살다 보니 웹이 엄청 많이 쓰임. 클라이언트에서 요청하는게 엄청 많아지고 있는데 이거 금지하면 확장해서 서비스 하는거 힘듦. 그래서 SOP정책 완화해달라 해서나온게 `CORS`(Cross-Origin-Resource-Sharing, 교차 기원(출처) 자원 공유) 가 가능하게 하겠다.
- 브라우저의 보안기술(SOP), 그럼 브라우저에서 못쓰는데 abc.com, jquery.com, naver.com이 합의가 되면 내가 주는 기술 너가 쓸 수 있게 해줄게 이게 CORS. 응답헤더에 `Access-Control-Allow-Origin`이라는 헤더에 어떤 값을 줌. 대표적으로 `*`.  이 Origin에 대해 접근을 허한다. abc.com, jquery가 나한테 자원을 주면서 헤더에 저런거 넣어주면 내 브라우저가 사용을 한다 만다 판단해서 사용하는 과정이 `CORS`

- 우리가 지금 ajax를 이용해서 naver.com을 읽으려고 하는데 우리 PC `http://localhost:8080`이 Origin인데 문서를 갖고오려고하는건 `http://www.naver.com` 완전 다름. 그래서 보여주거나 실행하는게 막힘. 거기까지 `SOP` 그걸 허락하는게 제공해주는 쪽에서 `Access-Controll_allow-Origin` 을 넣어줘야하는데 naver가 넣어줄까? NO. 그러면 뭘하냐, 그럼 브라우저(naver)에서 data가 내려올때 저걸 끼워넣어주도록 하는게 있다. 그게 확장프로그램!!

> **사이트가 다르다 == Origin이 다르다**
- Json 포맷 확인 사이트
**[https://jsonformatter.curiousconcept.com](https://jsonformatter.curiousconcept.com/)** 
---
## React 용어
- `property` : 속성
	- 객체를 표현하려고 할때 필요한 것
	- 객체를 표현하려고 할때 속성 뿐만 아니라 동작도 필요한데 그게 `method`
	- class라는 것은 어떤 데이터와 데이터를 처리하는 함수들의 집합.  
	- 자식이 부모로 부터 전달받은 값을 property라 함
	```html
	//부모 Board, 자식 Square
	<Board>
		<Square> value </Square>
	</Board>
	```
- `state` : 상태


