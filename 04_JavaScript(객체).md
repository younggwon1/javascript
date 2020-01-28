# JavaScript(객체)

> 자바스크립트의 기본 자료형은 숫자, 문자열, 불, 객체, 함수, undefined로 배열은 없다. 배열에는 '인덱스'와 '요소'가 있다. 각각의 요소를 사용하려면 배열 이름 뒤에 인덱스로 접근한다.(array[1] => 사과)
>
> 배열은 객체를 기반으로 만들어졌으므로 배열과 객체는 상당히 비슷하다. 다른 점은 배열은 요소에 접근할 때 인덱스를 사용하지만, 객체는 키를 사용한다.



#### 객체의 요소에 접근하는 방법

- 객체 뒤에 대괄호를 사용하고 키를 표시
  - product['제품명'] = '건조 망고'
- 하지만 다음과 같은 방법을 더 많이 사용
  - product.제품명 = '건조 망고'



**속성** : 객체 내부에 있는 값



```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let person = {
                name: '영권',
                address: '서울',
                eat: function (food){ 
                    console.log(food + "을 먹었습니다.");
                } 
            };


            console.log(person.name);
            person.eat('바나나');

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73226852-d6b00500-41b4-11ea-87d0-a9ecad4bedce.PNG)



```html
<!-- 정적 -->
<!DOCTYPE html>
<html>
    <head>

        <script>
            let school = {
                name: '멀티캠퍼스',
                capacity: [30,30,30],
                grade: '3',
                event: function(month, eventName){
                    console.log(this.name + ' ' + month + " 달에 " + eventName + "행사가 있습니다.");
                }
            };

            console.log(school.name);
            school.event("1월","졸업식");

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73226889-f34c3d00-41b4-11ea-9fa3-0a0b11e323b2.PNG)

### with를 사용

```html
<!-- 동적 -->
<!DOCTYPE html>
<html>
    <head>

        <script>
            let student = {};

            student.name = '영권';
            student.kor = 100;
            student.math = 90;
            student.eng = 80;

            let sum = '';
            let avg = '';

            // 첫번째 방법
            //sum = student.kor + student.math + student.eng;
            //avg = sum/3;

            // 두번째 방법(권장)
            with (student) { 
                sum = kor + math + eng;
                avg = sum/3;
            }

            console.log('총점 :' + sum);
            console.log('평균 :' + avg);

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73226922-0c54ee00-41b5-11ea-9d70-817d47fbdd2a.PNG)



```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let student = [];
            student.push({이름:'aaa',국어:90,수학:50,영어:10});
            student.push({이름:'bbb',국어:85,수학:60,영어:20});
            student.push({이름:'ccc',국어:70,수학:70,영어:30});
            student.push({이름:'ddd',국어:65,수학:80,영어:40});
            student.push({이름:'eee',국어:60,수학:90,영어:50});


            for (let i in student){

                student[i].sum = student[i].국어 + student[i].수학 + student[i].영어;
                student[i].avg = student[i].sum /3;
            }
            for (let i in student){
                with(student[i]){
                    console.log(이름 + ':' + '총점 : ' + sum + '/' + '평균 : ' + avg);

                }
            }

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73228029-c568f780-41b8-11ea-9beb-ab7923364f4c.PNG)

### 위의 코드를 함수 형태로 표현

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let student = [];
            student.push({이름:'aaa',국어:90,수학:50,영어:10});
            student.push({이름:'bbb',국어:85,수학:60,영어:20});
            student.push({이름:'ccc',국어:70,수학:70,영어:30});
            student.push({이름:'ddd',국어:65,수학:80,영어:40});
            student.push({이름:'eee',국어:60,수학:90,영어:50});

            let totalsum = 0;
            let totalavg = 0;

            for (let i in student){

                student[i].sum = function(){
                    return this.국어 + this.수학 + this.영어;
                };

                student[i].avg = function(){
                    return student[i].sum() /3;
                };
            }
            for (let i in student){
                with(student[i]){
                    console.log(이름 + ':' + '총점 : ' + sum() + '/' + '평균 : ' + avg());
                    totalsum += sum();
                }
            }

            //전체 평균 구하기
            console.log("전체 평균: " + (totalsum / student.length)/3)
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73228316-91da9d00-41b9-11ea-81e8-b9bcc74942a6.PNG)

---

### 생성자 함수

> new 키워드를 사용해 객체를 생성할 수 있는 함수

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            function student(name, kor, eng, mat, sci){
                this.이름 = name;
                this.국어 = kor;
                this.영어 = eng;
                this.수학 = mat;
                this.과학 = sci;

                this.sum = function(){
                    return this.국어 + this.영어 + this.수학 + this.과학;
                }

                this.avg = function(){
                    return this.sum() / 4;
                }

            }

            let student1 = new student('홍길동', 100, 90, 80, 70);
            let student2 = new student('이몸룡', 10, 50, 87, 34);

            console.log(student1.sum() + '/' + student1.avg());
            console.log(student2.sum() + '/' + student2.avg());
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73229244-67d6aa00-41bc-11ea-9008-1b04dcd4cd2f.PNG)

---

### 기본 내장 객체

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let objectNumber = new Number(273); //속성, 메소드 추가 o , Number 객체
            let primitiviNumber = 273; //속성, 메소드 추가 x

            Number.prototype.method = function(){
                return "Method on prototype";
            };

            console.log("primitive: " + primitiviNumber);
            console.log("object: " + objectNumber + "/" + objectNumber.method());
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73230192-bb96c280-41bf-11ea-9410-988c5e5d2f17.PNG)



#### toString()

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let myobject1 = new Object();
            let myobject2 = {};

            console.log(myobject1);
            console.log(myobject1.toString());

            //toString() 재정의 (overriding, 함수의 내용을 재정의)
            let student = {
                name: '홍길동',
                grade: '1학년',
                toString: function(){
                    return this.name + "/" + this.grade;
                }
            }
            
            console.log('student:' + student)

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73230758-a58a0180-41c1-11ea-9c7b-613ec8294d99.PNG)





#### Number 객체

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let maxNumber = Number.MAX_VALUE;
            let minNumber = Number.MIN_VALUE;

            console.log(maxNumber);
            console.log(minNumber);
            
            console.log(maxNumber + 1); // MAX_VALUE부터는 무한한 양의 숫자로 인식

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73230980-4a0c4380-41c2-11ea-9a9d-f2667646f749.PNG)



#### string 객체

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let string = "hello world!";

            console.log(string);
            console.log(string.length);
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73231077-a8d1bd00-41c2-11ea-8bfa-6a56ef1a9449.PNG)



#### -> 다음 string 객체의 메서드 기억

- charAt(position) : position에 위치하는 문자를 리턴한다.
- concat(args) : 매개변수로 입력한 문자열을 이어서 리턴한다.
- indexOf(serchString, position) : 앞에서부터 일치하는 문자열의 위치를 리턴한다.
- lastIndexOf(serchString, position) : 뒤에서부터 일치하는 문자열의 위치를 리턴한다.
- substr(start, count) : start부터 count만큼 문자열을 잘라서 리턴한다.
- substring(start,end) : start부터 end까지 문자열을 잘라서 리턴한다.

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let string = "hello world!";

            console.log(string.charAt(4));
            console.log(string.concat(" hi there"));
            console.log(string.indexOf("world"));
            console.log(string.lastIndexOf("world"));

            let ipaddress = "58.29.12.23";
            let values = ipaddress.split('.');

            console.log(typeof values);
            console.log(values[0]);
            console.log(ipaddress.substr(0,3));
            console.log(ipaddress.substring(4,6))

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73231601-2518d000-41c4-11ea-8726-9af363b57db2.PNG)



#### Array 객체

> 여러가지 자료를 쉽게 관리할 수 있게 도와주는 객체

#### -> 다음 Array 객체의 메서드 기억

- pop()* : 배열의 마지막 요소를 제거하고 리턴한다.

- push()* : 배열의 마지막 부분에 새로운 요소를 추가한다.

- slice()* : 요소의 지정한 부분을 리턴한다. 

- sort()* : 배열의 요소를 정렬한다. 

- splice()* : 요소의 지정한 부분을 삭제하고 삭제한 요소를 리턴한다. 

  

#### Date 객체

> 날짜와 시간을 표시하는 객체이다.

- get 형태의 메서드(게터)
- set 형태의 메서드(세터)

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let now = new Date();
            console.log(now);

            for (let i=0; i<10000000; i++){
                ;
            }

            let now1 = new Date('Tue Jan 28 2019 14:20:41');

            console.log(now1);
            console.log(now - now1);
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73237773-058ca200-41da-11ea-82e0-51cd8160c3a0.PNG)

---

### ECMAScript 5 Array 객체

#### forEach()

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let array = [50,203,227,2,158,34,23,6,256,10];

            //순차적으로 출력
            for (let i=0; i<array.length; i++){
                console.log(array[i]);
            }

            console.log("-------------------------")
            // 순차적으로 데이터를 출력 (for문 사용x)
            array.forEach(function(element) {
                console.log(element);
            });
        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73238372-22c27000-41dc-11ea-940f-8ae0ccd6b63c.PNG)



```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let array = [50,203,227,2,158,34,23,6,256,10];
            let newarray = [];
            
            // 홀수만 새로운 배열에 저장하기
            array.forEach(function(element) {
                if (element % 2 == 1)
                    newarray.push(element);
            });

            newarray.forEach(function(element){
                console.log(element);
            });

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73238401-37066d00-41dc-11ea-95ff-8480f32de9bb.PNG)



#### 간단한 예제

> 등급 나누기

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let array = [50,90,27,2,58,34,23,6,56,84];


            let grade = array.map(function(element){
                if (element>=0&&element<20){
                    return "F"
                }
                else if (element>=20&&element<40){
                    return "D"
                }
                else if (element>=40&&element<60){
                    return "C"
                }
                else if (element>=60&&element<80){
                    return "B"
                }
                else{
                    return "A"
                }


            });

            for (let i=0; i<array.length; i++){
                console.log(array[i] + "=>" + grade[i]);
            }



        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73239013-44bcf200-41de-11ea-94df-057faa2f7de8.PNG)



#### filter()

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let jumsu = [50,90,27,2,58,34,23,6,56,84];



            jumsu = jumsu.filter(function(element, index, array){
                return element >= 60;

            });

            jumsu.forEach(function(element){
                console.log(element);
            })

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73240686-0970f200-41e3-11ea-9052-9b893abd6541.PNG)



#### reduce()

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let jumsu = [1,2,3,4,5];

            let result = jumsu.reduce(function(preValue, curValue, index, array){
                console.log(preValue);
                console.log(curValue);
                console.log(index);
                console.log(array);
                console.log("----------------------");
                return preValue + curValue;
            });

            console.log(result);

        </script>


    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73241321-0b3bb500-41e5-11ea-9cb7-8d412dfbe1d4.PNG)



### json

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let json = {
                "id" : 12345,
                "account" : "123-4567-8899",
                "name" : "영권",
                "balance" : 1000,
                "lastTxDate" : "2020-01-20"
            };

            console.log(json);
            console.log(typeof(json));
            console.log(json.name + "/" + json.balance)

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73243105-1b09c800-41ea-11ea-84a5-2488327e02f6.PNG)

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let json = `{
                "id" : 12345,
                "account" : "123-4567-8899",
                "name" : "영권",
                "balance" : 1000,
                "lastTxDate" : "2020-01-20"
            }`;

            console.log(json);
            console.log(typeof(json));
            console.log(json.name + "/" + json.balance)

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73243133-31b01f00-41ea-11ea-85f5-70eb9517266e.PNG)





#### parsedJson

> 문자열을 객체로 변환

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let json = `{
                "id" : 12345,
                "account" : "123-4567-8899",
                "name" : "영권",
                "balance" : 1000,
                "lastTxDate" : "2020-01-20"
            }`;

            let parsedJson = JSON.parse(json);
            console.log(parsedJson);
            console.log(typeof(parsedJson));
            console.log(parsedJson.name + "/" + parsedJson.balance)

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73243614-5a84e400-41eb-11ea-8e1e-83cae4ac51d3.PNG)



#### stringJson

> 객체를 문자열로 변환

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let json = {
                "id" : 12345,
                "account" : "123-4567-8899",
                "name" : "영권",
                "balance" : 1000,
                "lastTxDate" : "2020-01-20"
            };

            let stringJson = JSON.stringify(json);
            console.log(stringJson); // 다른 서비스(서버)에 전달 가능
            console.log(typeof(stringJson));
            console.log(stringJson.name + "/" + stringJson.balance)

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73243650-74bec200-41eb-11ea-9757-36970c808391.PNG)



---

```html
<!DOCTYPE html>
<html>
    <head>

        <script>
            let openapi = `{"coord": { "lon": 139,"lat": 35},
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 281.52,
    "feels_like": 278.99,
    "temp_min": 280.15,
    "temp_max": 283.71,
    "pressure": 1016,
    "humidity": 93
  },
  "wind": {
    "speed": 0.47,
    "deg": 107.538
  },
  "clouds": {
    "all": 2
  },
  "dt": 1560350192,
  "sys": {
    "type": 3,
    "id": 2019346,
    "message": 0.0065,
    "country": "JP",
    "sunrise": 1560281377,
    "sunset": 1560333478
  },
  "timezone": 32400,
  "id": 1851632,
  "name": "Shuzenji",
  "cod": 200
}`
                
            


            console.log(openapi);
            console.log(typeof(openapi));


            let parsedJson = JSON.parse(openapi);
            console.log("현재날씨" + parsedJson.weather[0].main);
            console.log("현재온도" + parsedJson.main.temp);
            console.log("최고온도" + parsedJson.main.temp_max);
            console.log("최저온도" + parsedJson.main.temp_min);

        </script>

    </head>
    <body>

    </body>
</html>
```

![캡처](https://user-images.githubusercontent.com/42603919/73244633-ba7c8a00-41ed-11ea-9c82-0f08ae27c336.PNG)

---