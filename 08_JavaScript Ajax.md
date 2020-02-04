# JavaScript Ajax

```html
<!DOCTYPE html>
<html>
    <head>

        <!--<script src="../jquery/jquery.js"></script>-->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <script>
            $(document).ready(function() {
                 

                // $('#btnsubmit').onclick();
                $('#btnsubmit').on('click',function(){
                    let city = $('#city').val(); //데이터 존재유무 확인
                    
                if (city != null && city !=''){
                $.ajax({
                    url: "http://api.openweathermap.org/data/2.5/forecast",
                    type: "GET",
                    data: {
                        q: city,
                        APPID:"da2990f54bae2cfa73059c88df0290a2",
                        units:"metric"
                    },
                    success: function(data){
                        $('#contents').empty();
                        //let parsed = JSON.parse(data);
                        $.each(data.list, function(index, item) {
                        let _image = document.createElement("img");
                        _image.src = "http://openweathermap.org/img/wn/" 
                        + item.weather[0].icon +"@2x.png";

                        let _divhtml = item.dt_txt;
                        _divhtml += ", 기온:" + item.main.temp;
                        _divhtml += " <span style='color:blue;'>" + item.main.temp_min + "</span>";
                        _divhtml += "/<span style='color:red;'>" + item.main.temp_max + "</span>";
                        _divhtml += ", " + item.weather[0].description;

                        let imageSpan = document.createElement("span");
                        imageSpan.appendChild(_image);
                        let infoSpan = document.createElement("span");
                        infoSpan.innerHTML = _divhtml;

                        let div = document.createElement("div");
                        div.appendChild(imageSpan);
                        div.appendChild(infoSpan);

                        
                        $('#contents').append(div);
                        });
                    }, 

                });
                }
            });
            });
        
        </script>

    </head>
    <body>

        <input type="text" name="city" id="city" placeholder="도시를 입력하세요">
        <!--<input type="button" id="btnsubmit" value="검색">--> 
        <button id="btnsubmit">검색</button>
        
        <div id="contents"></div>
    </body>
</html>
```



```html
<!DOCTYPE html>
<html>
    <head>

        <!--<script src="../jquery/jquery.js"></script>-->
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <script>
            $(document).ready(function() {
                // $('#btnsubmit').onclick();
                $('#btnsubmit').on('click',function(){
                    // let city = $('#city').val(); //데이터 존재유무 확인
                    let city = $('#city > option:selected').val(); // option에서 선택된 값을 출력
                //if (city != null && city !=''){
                $.ajax({
                    url: "http://api.openweathermap.org/data/2.5/forecast",
                    type: "GET",
                    data: {
                        q: city,
                        APPID:"da2990f54bae2cfa73059c88df0290a2",
                        units:"metric"
                    },
                    success: function(data){
                        $('#contents').empty(); // 누적되는 데이터를 삭제해주는 코드
                        //let parsed = JSON.parse(data);
                        $.each(data.list, function(index, item) {
                        let _image = document.createElement("img");
                        _image.src = "http://openweathermap.org/img/wn/" 
                        + item.weather[0].icon +"@2x.png";

                        let _divhtml = item.dt_txt;
                        _divhtml += ", 기온:" + item.main.temp;
                        _divhtml += " <span style='color:blue;'>" + item.main.temp_min + "</span>";
                        _divhtml += "/<span style='color:red;'>" + item.main.temp_max + "</span>";
                        _divhtml += ", " + item.weather[0].description;

                        let imageSpan = document.createElement("span");
                        imageSpan.appendChild(_image);
                        let infoSpan = document.createElement("span");
                        infoSpan.innerHTML = _divhtml;

                        let div = document.createElement("div");
                        div.appendChild(imageSpan);
                        div.appendChild(infoSpan);

                        
                        $('#contents').append(div);
                        });
                    }, 

                });
                
            });
            });
        
        </script>

    </head>
    <body>

        <select id="city">
            <option value="seoul">서울</option>
            <option value="london">런던</option>
            <option value="tokyo">도쿄</option>
        </select>
        
        <!--<input type="text" name="city" id="city" placeholder="도시를 입력하세요">-->
        <!--<input type="button" id="btnsubmit" value="검색">--> 
        <button id="btnsubmit">검색</button>
        
        <div id="contents"></div>
    </body>
</html>
```

