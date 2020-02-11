# React (Redux)

> 리덕스는 자바스크립트를 위한 상태 관리 프레임워크이다.

- 리덕스에서 상태값이 변경되는 과정

![캡처](https://user-images.githubusercontent.com/42603919/74210684-02aca980-4cd0-11ea-9cd4-16809e9a4675.PNG)

1. 액션 : 액션은 type 속성값을 가진 자바스크립트 객체이다. 액션 객체에는 type 속성값 외에도 원하는 속성값을 얼마든지 넣을 수 있다. 애플리케이션의 상태를 변경하기 위해서는 액션을 생성
2. 미들웨어 : 미들웨어는 리듀서가 액션을 처리하기 전에 실행되는 함수이다.
3. 리듀서 : 리듀서는 액션이 발생했을 때 새로운 상태값을 만드는 함수이다.
4. 스토어 : 스토어는 리덕스의 상태값을 갖는 객체이다. 



### Flux

[Flux 이해하기](https://code-cartoons.com/a-cartoon-guide-to-flux-6157355ab207)

- MVC (Model, View, Controller)
- Model에서 Rendering을 위해 View로 데이터 전달
  - view에서 Model 데이터의 업데이트 발생
  - 의존성 문제로 인해 다른 Model 데이터 업데이트

- 문제점
  - 비동기적인 변경 요청에 대응 어려움
  - 하나의 변경이 다수의 변경을 발생할 수 있음
  - 데이터 흐름에 대한 디버깅이 어려움

- 해결책
  - 데이터는 단방향으로 전달
  - 새로운 데이터가 발생되면, 처음부터 흐름이 다시 시작 -> Flux



### Redux

[Redux 이해하기](https://code-cartoons.com/a-cartoon-intro-to-redux-3afb775501a6)

---



## 활용 예제

```
1. reducer 생성
 - Biz logic (데이터 처리, 상태 처리)
 - Root reducer에 Reducer를 추가
 - src/reducers/reducer-books.js
 - src/reducers/reducer-active-books.js

2. src/index.js
 - reducer를 가지고 store 생성
 - App.js 실행 시 store 지정

3. 사용자의 요청 작업 (이벤트 등)
 - src/actions/index.js <- selectBook
 - Action 만들때는 -> type(BOOK_SELECTED), payload 지정(상태값)

4. 사용자 View (or Containers) component 생성
 - src/Containers/book-list.js
 - src/Containers/book-detail.js

5. component하고 Reducer(store)를 연결
 - mapStateToProps(state)
 - mapDispatchToProps(dispatch)
 - connect 함수 사용
   - export default connect(mapStateToProps, mapDispatchToProps)(BookList);
   - export default connect(mapStateToProps)(Bookdetail);
```



```js
# App.js

import React from 'react';
import './App.css';
import BookList from './containers/Book-list';
import Bookdetail from './containers/book-detail';

function App() {
  return (
    <div className="App">
      <header className="App-header">
          <BookList />
          <Bookdetail />
      </header>
    </div>
  );
}

export default App;
```



```
1. reducer 생성
 - Biz logic (데이터 처리, 상태 처리)
 - Root reducer에 Reducer를 추가
 - src/reducers/reducer-books.js
 - src/reducers/reducer-active-books.js
```

```js
# src/reducers/index.js
// root reducer 역할
import { combineReducers } from 'redux';
import BookReducer from './Reducer-books';
import ActiveBook from './reducer-active-book';

const rootReducer = combineReducers({
    books: BookReducer,
    activeBook: ActiveBook,
});

export default rootReducer;

# src/reducers/reducer-books.js
export default function() {
    return [
        {title: 'Javascript', page: '101'},
        {title: 'Docker and kuber', page: '102'},
        {title: 'Java programming', page: '103'},
        {title: 'Microservice', page: '104'}
    ]
}

# src/reducers/reducer-active-books.js
export default function(state = null, action) {
    switch(action.type) {
        case 'BOOK_SELECTED':
            return action.payload;
        default:
            return state;
    }
}
```



```
2. src/index.js
 - reducer를 가지고 store 생성
 - App.js 실행 시 store 지정
```

```js
# src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

import { Provider } from 'react-redux';
import { createStore } from 'redux';
import reducer from './reducers';

const store = createStore(reducer);

ReactDOM.render(
<Provider store = {store}>
<App />
</Provider> , document.getElementById('root'));

```



```
3. 사용자의 요청 작업 (이벤트 등)
 - src/actions/index.js <- selectBook
 - Action 만들때는 -> type(BOOK_SELECTED), payload 지정(상태값)
```

```js
# src/actions/index.js
export function selectBook(book) {
    return {
        type: 'BOOK_SELECTED', //대문자 그리고 _ 를 사용함
        payload: book
    }
}
```





```
4. 사용자 View (or Containers) component 생성
 - src/Containers/book-list.js
 - src/Containers/book-detail.js
 
5. component하고 Reducer(store)를 연결
 - mapStateToProps(state)
 - mapDispatchToProps(dispatch)
 - connect 함수 사용
   - export default connect(mapStateToProps, mapDispatchToProps)(BookList);
   - export default connect(mapStateToProps)(Bookdetail);
```

```js
# src/Containers/book-list.js
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { bindActionCreators } from 'redux';
import { selectBook } from '../actions/index';

class BookList extends Component {

    renderList() {
        return this.props.books.map(book => { // BookList 배열 -> 반복처리
            return (
                <li key={book.title}
                onClick={() => this.props.selectBook(book)}>
                {book.title}
                </li> 
            )
        });

    }

    render() {
        return (
            <ul>
                {this.renderList()}
            </ul>
        );
    }
}

function mapStateToProps(state) {
    return {
        books: state.books
    }
}

function mapDispatchToProps(dispatch) {
    return bindActionCreators({selectBook: selectBook}, dispatch);
}

export default connect(mapStateToProps, mapDispatchToProps)(BookList);


# src/Containers/book-detail.js
import React, { Component } from 'react';
import { connect } from 'react-redux';

class Bookdetail extends Component {
    render() {
        if (!this.props.book) {
            return <div>select a book to get start</div>
        }
        return (
            <div>
                <h3>detail for: </h3>
                <div>title: {this.props.book.title}</div>
                <div>page: {this.props.book.page}</div>
            </div>
        );
    }
}

function mapStateToProps(state) {
    return {
        book: state.activeBook
    }
}

export default connect(mapStateToProps)(Bookdetail);
```



### 평상시 화면

![캡처](https://user-images.githubusercontent.com/42603919/74215421-617c1e00-4ce4-11ea-893c-38c7f7771ebe.PNG)

### 클릭 후


![캡처](https://user-images.githubusercontent.com/42603919/74215429-69d45900-4ce4-11ea-80ce-2dff59dae4a8.PNG)

