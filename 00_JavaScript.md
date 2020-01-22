# JavaScript

> 웹 브라우저에서 많이 사용하는 프로그래밍 언어, Java와 별개의 프로그래밍 언어이다.



### HTML 기본적인 구조

```html
<!DOCTYPE html>
<html>
    <head>

    </head>
    <body>
        
    </body>
</html>
```



### 창 띄어보기

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
            var name = "world"
            alert("hello" + name); // alert 경고 상자
                                   // ()는 함수, 산술연산을 할 때 사용
                                   // +는 덧셈 또는 문자열 결합의 의미가 있다.
        </script>

    </head>
    <body>
        
    </body>
</html>

```

![캡처](https://user-images.githubusercontent.com/42603919/72856635-804b4e00-3cfe-11ea-91be-091bcaa0dfcf.PNG)

#### 개발자 모드

ctrl + shift + i 가 단축키 이다.(F12)

- console.log -> console창에 나타난다.

![캡처](https://user-images.githubusercontent.com/42603919/72857527-331cab80-3d01-11ea-9187-e6d32d483e44.PNG)

![캡처](https://user-images.githubusercontent.com/42603919/72857543-46c81200-3d01-11ea-8c4d-b1819e6afac7.PNG)

- Application
  - local storage
  - sesstion storage



## 문법

- 키워드

  > 자바스크립트가 처음 만들어질 때 정해진 특별한 의미가 있는 단어

- 식별자

  > 자바스크립트에서 이름을 붙일 때 사용, 키워드 사용x

- 주석

  > 프로그램 진행에 영향을 끼치지 않음, 코드의 특정 부분을 설명, <!-- -->를 이용하여 사용한다.
  >
  > // => 라인주석,  /* */ => 여러줄 주석

### 주석 처리

![캡처](https://user-images.githubusercontent.com/42603919/72858208-5cd6d200-3d03-11ea-8bd3-0b33b3be41d9.PNG)

![캡처](https://user-images.githubusercontent.com/42603919/72858237-74ae5600-3d03-11ea-8b25-9f29606326bd.PNG)





### " " 사용

![캡처](https://user-images.githubusercontent.com/42603919/72858553-8e9c6880-3d04-11ea-8a16-f295cbebae15.PNG)





### 비교 연산자

```
== : 값이 같다.

!= : 값이 다르다.

=== : 값도 같고 데이터 타입도 같다

!== : 값도 다르고 데이터 타입도 다르다
```



![캡처](https://user-images.githubusercontent.com/42603919/72858876-8264db00-3d05-11ea-8dac-e51c4312c7fc.PNG)

![캡처](https://user-images.githubusercontent.com/42603919/72858917-9c9eb900-3d05-11ea-9d32-c44c55de7900.PNG)





---

### 간단한 실습 예제

> 짝수인지 홀수인지 판단하기

![캡처](https://user-images.githubusercontent.com/42603919/72859385-fe135780-3d06-11ea-9ff8-6bb3bcb81cbc.PNG)

---



### 논리연산자

```
! : 논리 부정 연산자
&& : 논리곱 연산자(둘 다 동시에)
|| : 논리합 연산자(둘 중 하나만)
```



### 변수선언

> **var**(일반변수, 중복선언 가능->사용권장x), **let**(로컬변수, 중복선언 불가능->사용권장o) , **const**(상수선언, 고정값)  



---

### 간단한 실습 예제

window.onload에 의해서 웹 페이지에 글자가 나타난다.

![캡처](https://user-images.githubusercontent.com/42603919/72860920-ad522d80-3d0b-11ea-9469-3795bad2c76d.PNG)

---



### Table 생성하기

<td></td> : 글씨

<th></th> : 진한 글씨, 가운데 정렬

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
        </script>
    </head>
    <body>
        <table width="50%" border="1"> 
            <tr> 
                <th>name</th>
                <th>phone</th>
                <th>address</th>
                <th>class</th>
            </tr>
            <tr> 
                <td>a</td>
                <td>b</td>
                <td>c</td>
                <td>d</td>
            </tr>
            <tr> 
                <td>e</td>
                <td>f</td>
                <td>g</td>
                <td>h</td>
            </tr>
            <tr> 
                <td>i</td>
                <td>j</td>
                <td>k</td>
            </tr>
            <tr> 
                <td>l</td>
                <td>m</td>
                <td>n</td>
                <td>o</td>
                <td>p</td>
            </tr>
        </table>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72865200-45efaa00-3d1a-11ea-801b-3c2813f7a1d5.PNG)

- **colspan** : 개수만큼 가로로 테이블 병합

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
        </script>
    </head>
    <body>
        <table width="50%" border="1"> 
            <tr> 
                <th>name</th>
                <th>phone</th>
                <th>address</th>
                <th>class</th>
            </tr>
            <tr> 
                <td>a</td>
                <td>b</td>
                <td colspan="2">c</td> <!-- colspan : 개수만큼 테이블 병합 -->
            </tr>
            <tr> 
                <td>e</td>
                <td>f</td>
                <td>g</td>
                <td>h</td>
            </tr>
        </table>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72865354-dcbc6680-3d1a-11ea-904b-a4f20ea89d0b.PNG)

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
        </script>
    </head>
    <body>
        <table width="50%" border="1"> 
            <tr> 
                <th>name</th>
                <th>phone</th>
                <th>address</th>
                <th colspan="2">class</thcolspan="2">
            </tr>
            <tr> 
                <td>a</td>
                <td>b</td>
                <td>c</td>
                <td colspan="2">d</td>
            </tr>
            <tr> 
                <td>e</td>
                <td>f</td>
                <td>g</td>
                <td colspan="2">h</td>
            </tr>
            <tr> 
                <td>i</td>
                <td>j</td>
                <td colspan="3">k</td>
            </tr>
            <tr> 
                <td>l</td>
                <td>m</td>
                <td>n</td>
                <td>o</td>
                <td>p</td>
            </tr>
        </table>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72865386-fc538f00-3d1a-11ea-8c79-f905f8e7f98d.PNG)

- **rowspan** : 개수만큼 세로로 테이블 병합

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
        </script>
    </head>
    <body>
        <table width="50%" border="1"> 
            <tr> 
                <th>name</th>
                <th>phone</th>
                <th>address</th>
                <th colspan="2">class</thcolspan="2">
            </tr>
            <tr> 
                <td rowspan="2">a</td>
                <td>b</td>
                <td>c</td>
                <td colspan="2">d</td>
            </tr>
            <tr> 

                <td>f</td>
                <td>g</td>
                <td colspan="2">h</td>
            </tr>
            <tr> 
                <td rowspan="2">i</td>
                <td>j</td>
                <td colspan="3">k</td>
            </tr>
            <tr> 

                <td>m</td>
                <td>n</td>
                <td>o</td>
                <td>p</td>
            </tr>
        </table>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72865482-57858180-3d1b-11ea-852a-23e195c278df.PNG)



### 간단한 실습 해보기

> 이력서 만들어 보기

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
        </script>
    </head>
    <body>
        <table width="50%" border="1"> 
            <tr> 
                <th rowspan="4">사진</th>
                <th colspan="4">이력서</th>
            </tr>
            <tr> 
                <td rowspan="2">성명</td>
                <td rowspan="2" >인</td>
                <td colspan="2">주민등록번호</td>
            </tr>
            <tr> 
                <th colspan="2"> - </td>
            </tr>
            <tr> 
                <td rowspan="2">생년월일</td>
                <td colspan="4" rowspan="2">19 년 월 일생 (만 세)</td>

            </tr>
            <tr> 
                
            </tr>
            <tr> 
                <th>주소</th>
                <td colspan="5"> </td>
            </tr>
            <tr> 
                <th>호적관계</th>
                <td>  </td>
                <td>  </td>
                <td>  </td>
                <td>  </td>
            </tr>
        </table>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72866624-5d7d6180-3d1f-11ea-9d44-aa3acef5c3b6.PNG)





```html
<!DOCTYPE html>
<html>
    <head>
        <script>
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
            <input type="checkbox" name="sns"> Facebook
            <input type="checkbox" name="sns"> Instargram
            <input type="checkbox" name="sns"> Google
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
            <input type="button" value="임시 저장">           

        </form>
    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72869221-ded8f200-3d27-11ea-844b-27f3d452e9c5.PNG)

---

### Number()

![캡처](https://user-images.githubusercontent.com/42603919/72870332-3dec3600-3d2b-11ea-8498-e32b58d41732.PNG)

**-> Number 적용 후**

![캡처](https://user-images.githubusercontent.com/42603919/72870364-5b210480-3d2b-11ea-8c8c-73b87e9ad932.PNG)



