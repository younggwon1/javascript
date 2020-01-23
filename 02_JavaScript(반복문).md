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



#### for 반복문 사용

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



#### while 반복문 예제

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            var value = 0;
            var startTime = new Date().getTime();

            while (new Date().getTime() < startTime + 1000){
                value++;
            }
            alert(value);
        </script>

    </head>
    <body>

    </body>
</html>
```



### 중첩 반복문 예제

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let output = "";
            /*
                *
                **
                ***
                ****
                *****
                ******
            */

            for (let row = 1; row < 10; row++){
                for (let col = 1; col <= row; col++){
                    output += "*";
                }
                output += "\n";
                
            }
            console.log(output);

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72948975-40ea3380-3dca-11ea-9827-c4c04582ff03.PNG)



```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let output = "";
            /*
                ********
                *******
                ******
                *****
                ****
                ***
                **
                *
            */

            for (let row = 10; row > 0; row--){
                for (let col = 1; col <= row; col++){
                    output += "*";
                }
                output += "\n";
                
            }
            console.log(output);

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72949083-90c8fa80-3dca-11ea-9a1e-70eab6d5544e.PNG)

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let output = "";
            /*
                    *
                   ***
                  *****
                 *******
                *********
               ***********    
            */
            for (let i = 0; i < 15; i++){
                for (let j = 15; j > i; j--){
                    output += ' ';
                }
                for (let k = 0; k < 2 * i -1; k++){
                    output += '*';
                }
                output += '\n';
            }
            console.log(output);

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/72949737-7d1e9380-3dcc-11ea-8fb3-93bfbe471f44.PNG)

**소수 출력하기**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let output = 0;

            for (let  i =2; i <= 100; i++){
                let isPrime = true;
                for (let j = 2; j < i; j++){
                    if (i % j == 0){
                        isPrime = false;
                        break;
                    }
                }
                if (isPrime){
                    console.log(i);
                }
            }


        </script>

    </head>
    <body>

    </body>
</html>
```



### 간단한 연습문제

> [52, 273, 103, 32, 57, 103, 31, 2]와 같은 숫자 배열이 주어질 때, 배열 내부에서의 최대값과 최소값을 찾는 코드를 작성해보세요.

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let array = [52, 273, 103, 32, 57, 103, 31, 2];
            let max = array[0];
            let min = array[0];

            for (let i = 0; i < array.length; i++){
                if (max < array[i]){
                    max = array[i];
                }
                if (min > array[i]){
                    min = array[i];
                }

            }
            console.log("최대값" + max);
            console.log("최소값" + min);
        </script>

    </head>
    <body>

    </body>
</html>
```













