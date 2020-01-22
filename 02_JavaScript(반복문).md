# JavaScript(반복문)

### while 반복문

```
while (<불 표현식>){
	<문장>
}
```



### do while 반복문

```
{
	<문장>
} do while (<불 표현식>)
```



### for 반복문

```
for(var i = 0, i< <반복 횟수>, i++){
	<문장>
}
```



### for in 반복문

```
for(<반복 변수> in <배열 또는 객체>){
	<문장>
}
```

---



### 배열

> 배열은 여러 개의 변수를 한꺼번에 선언해 다룰 수 있는 자료형이다.

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let array = [232,32,103,55,52];
            console.log(array);
            console.log(typeof array);
            console.log(array.length);
            console.log(array[0]);

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72874822-3bdba480-3d36-11ea-8378-2283f4776587.PNG)



#### 반복문 사용

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let array = [232,32,103,55,52];

        for(let i=0; i<5; i++){  
            console.log(array[i]);
        }
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72875155-0a170d80-3d37-11ea-80e1-50ad27f5c20b.PNG)



### 랜덤 게임

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let comNum = Math.floor(Math.random() * 100);
            for(let i=1; i<=100; i++){
                let userNum = Number(prompt("당신의" + i + "번째 예측 숫자는??"));

                if(comNum > userNum){
                    alert("보다 큰 수를 입력해 주세요");
                }
                else if(comNum < userNum){
                    alert("보다 작은 수를 입력해 주세요");
                }
                else{
                    alert("정답입니다."); 
                    break;
                }
                console.log(comNum)
            }
        </script>

    </head>
    <body>

    </body>
</html>
```

