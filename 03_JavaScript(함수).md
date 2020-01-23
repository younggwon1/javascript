# JavaScript(함수)

> 코드의 집합



### 익명 함수

```
var(let) 함수 = function() {

};
```



```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let func = function() {
                let ouotput = prompt("숫자를 입력해 주세요.");
                alert(output);
            };
            func();

        </script>

    </head>
    <body>

    </body>
</html>
```



### 선언적 함수

```
function 함수() {

}
```



```html
<!DOCTYPE html>
<html>
    <head>

        <script>

            function func2(name){
                alert("hello" + name);
            }

            func2("younggwon");
        </script>

    </head>
    <body>

    </body>
</html>
```



### return

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let add = function(a,b){
                return a+b;
            }
            let subtract = function(a,b){
                return a-b;
            }

            let addresult = add(10,5);
            let subresult = subtract(10,5);

            console.log(addresult);
            console.log(subresult);

        </script>

    </head>
    <body>

    </body>
</html>

-> 15, 5
```

---

```html
<!-- 가변 배열, 정적 배열 -->
<!DOCTYPE html>
<html>
    <head>

        <script>
            let myArray1 = ["apple", "banana", "orange"]; // 정적데이터, 크기가 정해져있음
            let myArray2 = new Array(); //배열 사이즈가 동적으로 바뀐다. 가변 데이터
            myArray2[0] = "grape";
            myArray2[1] = "lemon";

            console.log(myArray1);
            console.log(myArray2);

        </script>

    </head>
    <body>

    </body>
</html>
```

---

### 

### 타이머 변수

- setTimeout : 일정시간 후 함수를 한 번 실행한다. 
- setInterval : 일정 시간마다 함수를 반속해서 실행한다.
- clearTimeout : 일정 시간 후 함수를 한 번 실행하는 것을 중지한다.
- clearInterval : 일정 시간마다 함수를 반복하는 것을 중단한다.



### 코드 실행 함수

> 문자열을 코드로 실행할 수 있는 특별한 함수, **eval(string)**

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let  willeval = "";
            willeval += "var number = 10;";
            willeval += "console.log(number);";

            eval(willeval);
        </script>

    </head>
    <body>

    </body>
</html>

-> 10
```

