# React

> Facebook에서 개발하고 관리하는 UI 라이브러리, Component 기반, HTTP 클라이언트, 라우터, 상태관리 등의 기능이 내장되어 있지 않기 때문에, 자유롭게 사용가능 하며, 직접 라이브러리 용이

- 데이터의 Mutation
  - 특정 이벤트 -> 모델 변화 -> DOM에 데이터 반영

- 가상 돔을 통해서 UI를 빠르게 업데이트 (바뀐 부분만 바꾼다.)

- 함수형 프로그래밍을 적극적으로 활용한다.
- 높은 자유도



### React Project에 필요한 것

- Node.js
- Yarn : Facebook에서 만든 자바스크립트 패키지 매니저
- Webpack : 여러가지 파일을 한개로 결합하기 위한 도구
- Babel : 최신 사양의 자바스크립트 코드를 IE나 구형 브라우저에서도 동작하는 ES5 이하의 코드로 변환

```javascript
// 최신 사양의 자바스크립트 코트
[1,2,3].map(n => n**n)

// ES5 이하의 코드
[1,2,3].map(fuction (n){
	return Math.pow(n,n);
});
```



[react-app](https://github.com/facebook/create-react-app) <- facebook이 제공하는 것

[babel](https://babeljs.io/repl)



**App.js에서 시작한다.(React file)**

```javascript
import React from 'react';


function App() { // 컴포넌트 생성 -> class or fuction 내부에서 JSX를 반환
  return (
    <div className="App">
      <header className="App-header">
        Hello, World
      </header>
    </div>
  );
}

export default App; //외부에서 사용할 수 있도록 선언
```

![캡처](https://user-images.githubusercontent.com/42603919/73709069-71738b00-4743-11ea-9638-4d1de1306a91.PNG)



```js
import React, { Component } from 'react'; //component는 class를 사용하기 위해서 필요

class App extends Component {
  render() {
    return ( 
      <div>

        Hello, World

      </div>
    );
  }
}

export default App;

// 위의 코드와 같은 코드

//function App() {
//  return (
//    <div>
//        Hello, World
//    </div>
//  );
//}
// export default App;
```



#### return은 태그가 하나만 와야한다.(root element가 하나만)

```javascript
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div>
      <div>
        Hello, World
      </div>
      <div>
        Hello, World
      </div>
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73713701-b1416f00-4751-11ea-83ee-196a401fca0c.PNG)





#### Class 적용

```css
.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
```



```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className='App-header'> // class 적용
        <h1>
          Hello, World
      </h1>
        <h1>
          Hello, World
      </h1>
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73713958-a0452d80-4752-11ea-9567-6f24fa093bd4.PNG)



#### Closer를 갖고 있어야한다.

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className='App-header'>
        <h1>
          Hello, World
      </h1>
        <h1>
          Hello, World
      </h1>
      <input type='text'></input> // Closer
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73714066-0762e200-4753-11ea-9464-54ce8308cdfc.PNG)



#### 데이터 호출

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    const name = "younggwon";
    return (
      <div className='App-header'>
        <h1>
          Hello, World {name} //데이터 호출
      </h1>
        <h1>
          Hello, World
      </h1>
      <input type='text'></input>
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73714104-32e5cc80-4753-11ea-8f13-976792b2c56c.PNG)





#### 삼항 연산자

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    const time = 10;
    const name = "younggwon";
    return (
      <div className='App-header'>
        {
          time < 15 ? (<h1>hello, {name}</h1>) : (<h1>bye, {name}</h1>)
        }
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73714342-f1a1ec80-4753-11ea-9925-a9d8ef486165.PNG)

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    const time = 17;
    const name = "younggwon";
    return (
      <div className='App-header'>
        {
          time < 15 ? (<h1>hello, {name}</h1>) : (<h1>bye, {name}</h1>)
        }
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73714367-07171680-4754-11ea-9473-a45ca9765450.PNG)



#### 함수로 표기 (삼항연산자)

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    const time = 17;
    const name = "younggwon";
    return (
      <div className='App-header'>
        {
          (function(){
            if(time <12) return (<div>good morning, {name}</div>);
            if(time <18) return (<div>good afternoon, {name}</div>);
            if(time <22) return (<div>good evening, {name}</div>);
            
          })()
        }
      </div>
    );
  }
}

export default App;
```



#### 스타일 적용

**- className, style을 이용하여 적용한다.**

```css
.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
```



```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    const name = 'React'
    const css ={
      color: 'red',
      background: 'black',
      padding: '20px',
      fontSize:'40px'
    }

    return (
      <div className='App-header'>
        {
          <div style={css}>hello</div>
        }
      </div>
    );
  }
}

export default App;
```

![캡처](https://user-images.githubusercontent.com/42603919/73715024-fff10800-4755-11ea-82e6-7eecbe7eeff3.PNG)

### props, state

- props
  - 부모 컴포넌트가 자식 컴포넌트에게 전달하는 값
  - 자식 컴포넌트에서는 props값을 수정할 수 없음
  - props값은 **``this.``** 키워드를 이용하여 사용

- state
  - 컴포넌트 내부에 선언하여 사용되는 보관용 데이터 값
  - 동적인 데이터 처리

![캡처](https://user-images.githubusercontent.com/42603919/73716244-ccb07800-4759-11ea-9e6e-bbf70369e588.PNG)



#### props(단일값 전달)

```js
// 부모 컴포넌트
import React, { Component } from 'react';
import Myintro from './Myintro';


class App extends Component {
  render() {
    const name = "younggwon"
    return (

      <Myintro name={name} /> // 임의의 값을 전달

    );
  }
}

export default App;

// 자식 컴포넌트
import React, { Component } from 'react';


class Myintro extends Component {
    render() {
        const css = {
            color: 'blue',
            fontSize: '40px'
        }
        return (
            <div style={css}>
                안녕하세요, 제 이름은 <b>{this.props.name}</b> 입니다.
            </div>
        );
    }
}

export default Myintro;
```

![캡처](https://user-images.githubusercontent.com/42603919/73717221-7f81d580-475c-11ea-86ae-8e1f3e642089.PNG)



#### props(여러개 값 전달)

```js
// 부모 컴포넌트
import React, { Component } from 'react';
import Myintro from './Myintro';


class App extends Component {
  render() {
    const card = {
      name: "younggwon",
      email: "abc123@naver.com",
      phone: "010-1234-5678"
    }

    return (

      <Myintro card={card} /> // 어러개의 값을 전달

    );
  }
}

export default App;
```



```js
// 자식 컴포넌트
import React, { Component } from 'react';


class Myintro extends Component {
    render() {
        const css = {
            color: 'blue',
            fontSize: '40px'
        }
        return (
            <div style={css}>
                안녕하세요, 제 이름은 <b>{this.props.card.name}</b> 입니다. 
                이메일은 <b>{this.props.card.email}</b>입니다.
                전화번호는 <b>{this.props.card.phone}</b>입니다.
            </div>
        );
    }
}

export default Myintro;
```

![캡처](https://user-images.githubusercontent.com/42603919/73717894-5febac80-475e-11ea-8bba-15f21c76c643.PNG)



#### ``함수``를 사용하여 props

```js
// 부모 컴포넌트
import React, { Component } from 'react';
import Myintro1 from './Myintro1';


class App extends Component {
  render() {
    const card = {
      name: "younggwon",
      email: "abc123@naver.com",
      phone: "010-1234-5678"
    }

    return (

      <Myintro1 card={card} /> // 어러개의 값을 전달

    );
  }
}

export default App;
```

```js
// 자식 컴포넌트
import React from 'react'; 


const Myintro1 = function({card}){
    return (
        <div>
            안녕하세요, 제 이름은
            <b>
                {card.name},
                {card.email},
                {card.phone}

            </b> 입니다.

        </div>
    )
}

export default Myintro1;
```

![캡처](https://user-images.githubusercontent.com/42603919/73719053-8ced8e80-4761-11ea-9c3c-4b33dd38e86c.PNG)



#### State

```js
// 부모 컴포넌트
import React, { Component } from 'react';
import Counter from './Counter';


class App extends Component {
  render() {


    return (
      <Counter />
    );
  }
}

export default App;
```

```js
// 자식 컴포넌트
import React, { Component } from 'react';


class Counter extends Component {
    state = {
        count: 0
    }

    handleincreaseClick = () => {   // handleincreaseClick = function()과 동일
        this.setState({
            count: this.state.count + 1
    });
}

    handledecreaseClick = () => {   // handledecreaseClick = function()과 동일
        this.setState({ 
            count: this.state.count - 1
    });
}

    render() {
        return (
            <div>
                <h1>Counter</h1>
                <h2>{this.state.count}</h2>
                <button onClick={this.handleincreaseClick}>+</button>
                <button onClick={this.handledecreaseClick}>-</button>
            </div>
        );
    }
}

export default Counter;
```

#### **-> setState는 state의 값을 변경하기 위해 사용하는 것**



#### 전개 연산자

```js
    handlechangeClick = () => {
        this.setState({
            name: this.state.info.name = 'younggwon',
        });
    }

	// 전개 연산자 사용
    handlechangeClick = () => {
        this.setState({
            ...this.state.info,
            name:'younggwon'
        });
    } 
```



#### Life Cycle

> 모든 컴포넌트는 다음과 같이 세 단계를 거친다.
>
> - 초기화 단계
> - 업데이트 단계
> - 소멸 단계

```js
constructor(props) {
        super(props);
        this.state.count = this.props.init;
        console.log('call construct');
    }

    componentDidMount() {
        console.log('componentDidMount');
    }

    shouldComponentUpdate(nextprops, nextState) {
        console.log('shouldComponentUpdate');
        if (nextState.count % 5 === 0) return false;
        return true;
    }

    componentWillUpdate(nextprops, nextState) {
        console.log('componentWillUpdate');
    }

    componentDidUpdate(preprops, preState) {
        console.log('componentDidUpdate');
    }
```



#### 에러 코드

```js
// 부모 컴포넌트
import React, { Component } from 'react';
import Counter from './Counter';


class App extends Component {
  render() {
    const count = 200

    return (
      <Counter init = {count}/>
    );
  }
}

export default App;


// 자식 컴포넌트
import React, { Component } from 'react';

const ErrorObject = () => {
    throw (new Error('에러 발생'));
}

class Counter extends Component {
    state = {
        count: 0,
        error: false,
        info: {
            name: 'React',
            age: 10
        }
    }

    componentDidCatch(error, info){
        this.setState({
            error: true
        })
    }

    handleIncrease = () => {
        this.setState({
            count: this.state.count + 1
        });
    }

    handleDecrease = () => {
        this.setState({
            count: this.state.count - 1
        });
    }

    handleChangeInfo = () => {
        this.setState({
            info: {
                ...this.state.info,
                name: 'Dowon'
            }
        });
    }

    render() {

        if(this.state.error) return(<h1>에러가 발생했습니다.</h1>);
        return (
            <div>
                <h1>Counter</h1>
                <h2>{this.state.count}</h2>
                {this.state.count == 3 && <ErrorObject />}

                <button onClick={this.handleIncrease}>+</button>
                <button onClick={this.handleDecrease}>-</button>
                <button onClick={this.handleChangeInfo}>Change info name</button>

                {this.state.info.name}/{this.state.info.age}
            </div>
        );
    }
}

export default Counter;
```



















