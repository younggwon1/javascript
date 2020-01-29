# JavaScript(객체 모델)

### 브라우저 객체 모델

> 브라우저 관련 객체 정리, 웹 브라우저와 관련된 객체의 집합을 의미한다.

- window 객체 : window 객체의 속성과 메서드 출력, 코드를 실행(익스플로러, 크롬에서는 확인x -> 파이어폭스4나 오페라 브라우저를 사용하면 결과 확인 가능)
- location 객체
- navigator 객체
- history 객체
- screen 객체
- document 객체



#### window 객체

- **open**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.open("https://www.naver.com","mynaver","width=600,height=400",true);

        </script>

    </head>
    <body>
        <ul>
            <li>
                <a href="http://www.naver.com">naver</a>
            </li>
            <li>
                <a href="http://www.daum.net">daum</a>
            </li>
            <li>
                <a onclick=" alert('google을 클릭했습니다.')">google</a> <!--클릭을 했을 때 alert상자가 띄어짐-->
            </li>
            <li>
                <a onclick=" window.open('https://www.kdata.or.kr')">한국데이터진흥원</a> <!--클릭을 했을 때 페이지가 열림-->
            </li>
        </ul>
    </body>
</html>
```

- 함수를 사용

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            function myopen(url) {
                window.open(url, '_black', "width=600,height=400");
            }

        </script>

    </head>
    <body>
        <ul>
            <li>
                <a onclick="myopen('https://www.naver.com')">naver</a>
            </li>
            <li>
                <a onclick="myopen('https://www.daum.net')">daum</a>
            </li>
            <li>
                <button onclick="myopen('https://www.google.com')">google</button>
            </li>
        </ul>
    </body>
</html>
```



- **location**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            function mylocation(url){
                location.href="https://www.multicampus.com";
            }
        </script>

    </head>
    <body>
        <ul>
            <li>
                <button onclick="mylocation()">multicampus</button>
            </li>
        </ul>
    </body>
</html>
```



- **navigator**

> 웹 페이지를 실행하고 있는 브라우저에 대한 정보가 있다.

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            console.log(navigator.appCodeName);
            console.log(navigator.appName);
            console.log(navigator.appVersion);
            console.log(navigator.platform);
            console.log(navigator.userAgent);


            function mylocation(url){
                location.href="https://www.multicampus.com";
            }
        </script>

    </head>
    <body>
        <ul>
            <li>
                <button onclick="mylocation()">multicampus</button>
            </li>
        </ul>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73319884-06c4da00-4281-11ea-856c-bfa7766d77d4.PNG)



- **onload**

> html 페이지가 모두 load된 이후 제일 마지막에 실행

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = function() {
                console.log("process - 0");
            }
        </script>

    </head>
    <body>
        <h1>process - 1</h1>
        <script>console.log("process - 1");</script>
        <h1>process - 2</h1>
        <script>console.log("process - 2");</script>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73320218-ecd7c700-4281-11ea-96cd-cc465670db2d.PNG)

---

### 문서 객체 모델

> 웹 브라우저가 html 페이지를 인식하는 방식

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = function() {
                let h1_tag = document.createElement("h1");
                let greeting_text = document.createTextNode("Hi, there");
                h1_tag.appendChild(greeting_text);
                document.body.appendChild(h1_tag);
            }
        </script>

    </head>
    <body>
        <h1>hello, dom</h1>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73321428-c582f900-4285-11ea-9586-e50644652e9b.PNG)

```html
    <body>
        <ul>
        	<li>naver</li>
        	<li>daum</li>
        </ul>
    </body>

    과 동일한 코드(동적형태로)
    
    <!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = function() {
                let _ul = document.createElement("ul");
                let _li1 = document.createElement("li");
                let _li2 = document.createElement("li");
                let _naver = document.createTextNode("naver");
                let _daum = document.createTextNode("daum");

                _li1.appendChild(_naver);
                _li2.appendChild(_daum);

                _ul.appendChild(_li1);
                _ul.appendChild(_li2);

                document.body.appendChild(_ul);
            }
        </script>

    </head>
    <body>
        <h1>link</h1>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73322407-1267cf00-4288-11ea-940e-b4243fd67204.PNG)



- **img**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = function() {
                //img 태그 추가

                let myImg = document.createElement("img");
                myImg.src = "googlelogo.png";
                myImg.width = 400;
                myImg.height = 250;



                document.body.appendChild(myImg);
            }
        </script>

    </head>
    <body>
        <h1>img</h1>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73323000-5ad3bc80-4289-11ea-9770-35d4b156abc3.PNG)



- **innerHTML**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = function() {
                //img 태그 추가

                let myImg = document.createElement("img");
                myImg.src = "googlelogo.png";
                myImg.width = 400;
                myImg.height = 250;



                document.body.appendChild(myImg);

                let div1 = document.getElementById("mydiv1");

                div1.innerHTML = "<h1 style='color: blue;'>Hello, my world</h1>";
            }
        </script>

    </head>
    <body>
        <h1>innerHTML</h1>

        <div id="mydiv1">
            ~~~ here
        </div>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73323378-a044b980-428a-11ea-8ec4-da2a33bd3633.PNG)



- **innerText**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = function() {
                //img 태그 추가

                let myImg = document.createElement("img");
                myImg.src = "googlelogo.png";
                myImg.width = 400;
                myImg.height = 250;



                document.body.appendChild(myImg);
                // document.body.innerHTML = "<h1 style='color: blue;'>Hello, my world</h1>";
                let div1 = document.getElementById("mydiv1");

                div1.innerText = "<h1 style='color: blue;'>Hello, my world</h1>";
            }
        </script>

    </head>
    <body>
        <h1>innerHTML</h1>

        <div id="mydiv1">
            ~~~ here
        </div>

    </body>
</html>

```

![캡처](https://user-images.githubusercontent.com/42603919/73323454-d2eeb200-428a-11ea-8593-f5dae47808b7.PNG)

---

#### 선택된 sns 값 가져오기

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
            function saveTemporary() { 
                // 선택된 sns 값 가져오기
                let selectedsns = document.getElementsByName("sns");
                for (let i=0; i<selectedsns.length; i++){
                    if (selectedsns[i].checked){
                        console.log(selectedsns[i].value);
                    }
                        
                }
            
            }
        </script>
    </head>
    <body>
        <!-- 
            POST : 클라이언트가 입력한 내용을 서버에 전달할 때 사용(가입, 저장) 
                    request body
            GET : 사용자가 서버의 resource를 요청할 때 사용
                    웹 브라우저 -> URL요청
         -->
        <form action="regist.html" method="POST">
            이름 : <input type="text" name="name" placeholder="이름을 입력하세요">
            <br/>
            아이디 : <input type="text" name="id" placeholder="아이디를 입력하세요">
            <br/>
            비밀번호 : <input type="password" name="pwd" placeholder="비밀번호를 입력하세요">
            <br/>
            
            남성 : <input type="radio" name="gender">
            여성 : <input type="radio" name="gender">
            <br/>

            사용하는 SNS : 
            <input type="checkbox" name="sns" value="facebook"> Facebook
            <input type="checkbox" name="sns" value="instagram"> Instargram
            <input type="checkbox" name="sns" value="google"> Google
            <br/>

            연령 : 
            <select name="age">
                <option value="10">10대</option>
                <option value="20">20대</option>
                <option value="30">30대</option>
            </select>
            <br/>

            사진 : 
            <input type="file" name="profile">    
            <br/>
            
            자기소개
            <textarea name="intro">

            </textarea>
            <br/>

            <input type="submit" value="회원 가입">
            <input type="reset" value="초기화">
            <input type="button" value="임시 저장" onclick="saveTemporary()">           

        </form>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73324095-2235e200-428d-11ea-9374-10362a855702.PNG)

---



#### 날씨 api를 가지고 해보기

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let weather_json = `
            {
                "weather": [
                {
                "main": "Clouds",
                "description": "overcast clouds",
                "icon": "04d"
                }
                ],

                "main": {
                "temp": 9.27,
                "temp_min": 9,
                "temp_max": 10,
                "humidity": 41
 
                },
                "wind": {
                "speed": 1.86

                },

                "dt": 1580272501
            }

            `;
            window.onload = function() {
                let _img = document.getElementById("_img");
                let _temp = document.getElementById("_temp");
                let _temp_min = document.getElementById("_temp_min");
                let _temp_max = document.getElementById("_temp_max");
                let _wind = document.getElementById("_wind");
                // json 파일의 값을 각 tag 값에 지정
                // text(json) -> object(jsin) : JSON.parse
                // object(jsin) -> text(json) : JSON.stringify()

                let parsedJson = JSON.parse(weather_json);

                // 이미지 객체 생성
                let _image = document.createElement("img");
                _image.src = "";
                // _img에 추가
                _image.src = "http://openweathermap.org/img/wn/" + parsedJson.weather[0].icon + "@2x.png";
                _img.appendChild(_image);

                _temp.innerText = "현재온도 " + parsedJson.main.temp + "도" + "," + parsedJson.weather[0].main;

                _temp_min.innerText = "최저온도 : " + parsedJson.main.temp_min 
                _temp_max.innerText = "최고온도 : " + parsedJson.main.temp_max

                _wind.innerText = "풍속 : " + parsedJson.wind.speed + "습도 : " + parsedJson.main.humidity

            }

            

        </script>
    </head>
    <body>
        <table>
            <tr>
                <td rowspan="2" id="_img"></td>
                <td colspan="2" id="_temp"></td>
                <!--<td></td>-->
            </tr>
            <tr>
                <!--<td></td>-->
                <td id="_temp_min_max">
                    <span id = _temp_min style="color: blue;">

                    </span>
                    <span id = _temp_max style="color: red;">

                    </span>
                </td>
                <td id="_wind"></td>
            </tr>
        </table>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73332579-874c0080-42aa-11ea-8ae7-adcfbeb40c02.PNG)



#### 시계 만들기

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = () => {
                let clock = document.getElementById("clock");
                setInterval(function() {
                    clock.innerHTML = new Date().toString();
                }, 1000);
                
            }
        </script>

    </head>
    <body>
        <h1 id="clock"></h1>
    </body>
</html>
```

