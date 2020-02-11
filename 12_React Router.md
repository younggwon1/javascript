# React Router

> SPA에서의 라우팅 문제를 해결하기 위해서 사용되는 네비게이션 라이브러리
>
> 브라우저 내장 객체 사용가능 : location, history
>
> React Router : Web, Native, react-router-dom  라이브러리 필요



vscode에서 Reactjs code snippets 설치 -> rcc , rsc



```js
import React, { Component } from 'react';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import Page1 from './routes/page1';
import Page2 from './routes/page2';
import Page3 from './routes/page3';
import Header from './components/header';



class App extends Component {
  render() {
    return (
      <Router>
        <Header />
        <Route path="/my_note1" component={Page1} />
        <Route path="/my_note2" component={Page2} />
        <Route path="/my_note3" component={Page3} />
      </Router>
    );
  }
}

export default App;
```



```js
import React from 'react';
import { Link } from 'react-router-dom'

const Header = () => {
    return (
        <div>
            <ul>
                <li><Link to="/my_note1">page1</Link></li>
                <li><Link to="/my_note2">page2</Link></li>
                <li><Link to="/my_note3">page3</Link></li>
            </ul>
        </div>
    );
};

export default Header;
```



```js
import React from 'react';

const Page1 = () => {
    return (
        <h1>
            page1
        </h1>
    );
};

export default Page1;
```



```js
import React from 'react';

const Page2 = () => {
    return (
        <h1>
            page2
        </h1>
    );
};

export default Page2;
```



````js
import React from 'react';

const Page3 = () => {
    return (
        <h1>
            page3
        </h1>
    );
};

export default Page3;
````

