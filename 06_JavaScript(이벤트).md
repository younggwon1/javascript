# JavaScript(이벤트)

> 키보드를 이용해 버튼을 입력하거나 마우스 클릭과 같이 다른 것에 영향을 미치는 것



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
                
                clock,onclick = function() {
                    clock.style = "color: blue;"
                };
            }
        </script>

    </head>
    <body>
        <h1 id="clock"></h1>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73333433-18bc7200-42ad-11ea-8d43-643a92308358.PNG)

**``클릭하면``**

![캡처](https://user-images.githubusercontent.com/42603919/73333455-270a8e00-42ad-11ea-9040-b33aa7942243.PNG)



#### +버튼을 누르면 +1, -버튼을 누르면 -1

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            window.onload = () => {
                let counter = document.getElementById("counter");
                let plusbtn = document.getElementById("plus");

                plusbtn.onclick = function() {
                    counter.innerText ++;
                }


                let minusbtn = document.getElementById("minus");
                minusbtn.onclick = function() {
                    counter.innerText --;
                }
            }

        </script>

    </head>
    <body>
        <h1 id="counter">0</h1>
        <button id="plus" onclick="plusCounter()">+</button>
        <button id="minus">-</button>
    </body>
</html>
```

---

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
            function saveTemporary() { 
                // 선택된 sns 값 가져오기
                let selectedsns = document.getElementsByName("sns");
                let selectedcount = 0;

                for (let i=0; i<selectedsns.length; i++){
                    if (selectedsns[i].checked){
                        selectedcount++;
                        console.log(selectedsns[i].value);
                        
                    }
                    if (selectedcount == 0) {
                        alert("선택이 안됐습니다. sns를 선택하세요");
                        break;
                        
                    }
                    
                    let inputs = document.getElementsByTagName('input');
                    for (let i=0; i<inputs.length; i++){
                        console.log(inputs[i]);
                    }

                }
            
            }

            window.onload = function() {
                let btnnext = document.getElementById("btnnext");
                btnnext.onclick = function() {
                    let name = document.getElementById("txtname");
                    let id = document.getElementById("txtid");
                    let pwd = document.getElementById("txtpwd");

                    if (name.value == ""){
                        alert("이름은 필수 입력입니다.");
                        return;
                    }

                    if (id.value == ""){
                        alert("아이디는 필수 입력입니다.");
                        return;
                    }

                    if (pwd.value == ""){
                        alert("비밀번호는 필수 입력입니다.");
                        return;
                    }

                    // 다음 단계 or form.action 페이지로 이동
                    let frm = document.getElementById("registform");
                    frm.submit();


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
        <form action="regist.html" method="POST" id="registform">
            이름 : <input type="text" id="txtname" name="name" placeholder="이름을 입력하세요">
            <br/>
            아이디 : <input type="text" id="txtid" name="id" placeholder="아이디를 입력하세요">
            <br/>
            비밀번호 : <input type="password" id="txtpwd" name="pwd" placeholder="비밀번호를 입력하세요">
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
            <input type="button" value="다음단계" id = "btnnext">
            <input type="button" value="임시 저장" onclick="saveTemporary()">           

        </form>
    </body>
</html>
```

---



















