# JavaScript(조건문)

### if 조건문

```
if (<불 표현식>) {
	<문장>
}
```



### if else 조건문

```
if (<불 표현식>) {
	<문장>
}
else
{
	<문장>	
}
```



### if else if 조건문

```
if (<불 표현식>) {
	<문장>
}
else if
{
	<문장>	
}
else
{
	<문장>
}
```



### switch 조건문

```
switch (<비교할 값>){
	case <값>:
		<문장>
		break;
	case <값>:
		<문장>
		break;
	case <값>:
		<문장>
		break;
}
```



### 간단한 실습

> 국어, 영어, 수학 점수를 받아 평균을 내고 그 평균을 수,우,미,양,가로 표시해라

```html
<!-- if else if 조건문 -->
<!DOCTYPE html>
<html>
    <head>
        <script>
            let korean = prompt("국어 점수를 입력하세요."); //string
            let english = prompt("영어 점수를 입력하세요."); //string
            let math = prompt("수학 점수를 입력하세요."); //string

            let covertekorean = Number(korean)
            let coverteenglish = Number(english)
            let covertemath = Number(math)

            let result = (covertekorean + coverteenglish + covertemath)/3;

            console.log("result=" + result); // string + number = string

            if(result>=80){
                console.log("수 입니다");
            }
            else if(result>=60&&result<80){
                console.log("우 입니다");
            }
            else if(result>=40&&result<60){
                console.log("미 입니다");
            }
            else if(result>=20&&result<40){
                console.log("양 입니다");
            }
            else{
                console.log("가 입니다");
            }

        </script>

    </head>
    <body>

    </body>
</html>
```

```html
<!-- switch 조건문 -->
<!DOCTYPE html>
<html>
    <head>
        <script>
   
            let korean = prompt("국어 점수를 입력하세요."); //string
            let english = prompt("영어 점수를 입력하세요."); //string
            let math = prompt("수학 점수를 입력하세요."); //string

            let covertekorean = Number(korean)
            let coverteenglish = Number(english)
            let covertemath = Number(math)

            let result = (covertekorean + coverteenglish + covertemath)/3;

            console.log("result=" + result); // string + number = string


            switch(true){
                case result>=80:
                console.log("수 입니다");
                break;
                case result>=60&&result<80:
                console.log("우 입니다");
                break;
                case result>=40&&result<60:
                console.log("미 입니다");
                break;
                case result>=20&&result<40:
                console.log("양 입니다");
                break;
                default:
                console.log("가 입니다");
                break;
            }
        </script>

    </head>
    <body>

    </body>
</html>
```

---



### indexOf()

> 앞에 있는 문자열 뒤에 있는 문자열이 포함되어 있을 경우 위치를 출력해주는 메서드이다.

```html
<!DOCTYPE html>
<html>
    <head>
        <script>
            let sayhello = "안녕하세요.";
            
            console.log(sayhello);
            console.log(sayhello.indexOf("안녕"));
            console.log(sayhello.indexOf("하세요"));
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72873965-5745b000-3d34-11ea-8558-85ce65ae76cd.PNG)





