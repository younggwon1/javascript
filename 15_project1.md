```
apidemo>java -jar apidemo-0.2.jar 실행
```



![캡처](https://user-images.githubusercontent.com/42603919/74627764-2c197980-5197-11ea-8fa7-d45e31f34d71.PNG)



## App.js

```js
import React from 'react';
import './App.css';
import { BrowserRouter as Router, Route, Switch} from 'react-router-dom'
import PostNew from './components/posts_new'
import PostShow from './components/posts_show'
import PostIndex from './components/posts_index'



function App() {
  return (
      // /가 계속 걸리므로 실행을 하게 되면 계속 실행이 된다.
      // exact => 딱 하나만 처리할 수 있도록  한다.
      // 아니면 맨 밑으로 배치시킨다.
      <Router>
        <div>
          <Route exact path='/' component={PostIndex} />
          <Route path='/blogs/new' component={PostNew} /> 
          <Route path='/blogs/:id' component={PostShow} /> 
        </div> 
      </Router>
  );
}

export default App;
```



## index.js(src)

```js
// store 생성하는 부분
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { Provider } from 'react-redux'
import { createStore, applyMiddleware } from 'redux';
import promise from 'redux-promise'

import reducers from './reducers'

const createStoreWithMiddle = applyMiddleware(promise)(createStore); //store 생성

ReactDOM.render(
    <Provider store={createStoreWithMiddle(reducers)}>
    <App />
    </Provider>
, document.getElementById('root'));

```



## index.js(src/actions)

```js
import axios from 'axios';

// define action constants
export const FETCH_POSTS = 'fetch_posts';
export const CREATE_POST = 'create_post';
export const FETCH_POST = 'fetch_post';
export const DELETE_POST = 'delete_post';

// define api server address
const ROOT_URL = "http://127.0.0.1:8800/api";


// fetch post
export function fetchPosts() {
    const request = axios.get(`${ROOT_URL}/blogs`); // ``를 사용함으로써 문자열로 변환

    //request -> { 
    //"result": "1",
    // "blogs": [
    //     {
    //         "id": 3,
    //         "category": "music",
    //         "title": "hox3",
    //         "author": "yjs",
    //         "contents": "hohoho",
    //         "link": "",
    //         "is_private": 1,
    //         "cdate": "2020-02-14 16:39:32.728065"
    //     } 
    // request에는 위와 비슷한 형식의 값이 들어가 있다.

    return {
        type: FETCH_POSTS,
        payload: request
    }
}

// create post
export function createPost(values, callback) {
    const request = axios.post(`${ROOT_URL}/blogs`, values).then(() => callback()); //json -> API server

    return {
        type: CREATE_POST,
        payload: request
    }
}

// detail post
export function fetchPost(id) {

    const request = axios.get(`${ROOT_URL}/blogs/${id}`);
    return {
        type: FETCH_POST,
        payload: request
    }
}

// delete post
export function deletePost(id, callback) {
    const request = axios.delete(`${ROOT_URL}/blogs/${id}`).then(() => callback()); //json -> API server

    return {
        type: DELETE_POST,
        payload: id
    }
}
```



## posts_index.js(src/components)

```js
import _ from 'lodash';
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { fetchPosts } from '../actions/index';
import { bindActionCreators } from 'redux';
import { Link } from 'react-router-dom';

class PostsIndex extends Component {
  // define a lifecycle function for retrieve data  

  componentDidMount() { //무조건 실행되는 함수
    console.log("componentDidMount called");
    this.props.fetchPosts();
  }

  renderPosts() {
    // list작업 -> 개별 <li> 태그로 출력
    // console.log(this.props.posts.blogs);
    return _.map(this.props.posts, post => {
      return (
        <li className='list-group-item' key={post.id}>
          <Link to={`/blogs/${post.id}`}>{post.title}</Link>
        </li>
      )
    });  
  }

  render() {
    return (
      <div>
        <div className="text-xs=right">
          <Link className="btn btn-primary" to="/blogs/new">Add a Post</Link>
        </div>
          <h3>Posts</h3>
          <ul className="list-group">
            {this.renderPosts()}
          </ul>
      </div>
    );
  }
}


function mapStateToProps(state) {  // 상태관리함수, store의 state를 컴포넌트의 props에 매핑 시켜준다.
  return { posts: state.posts} // posts: PostsReducer 값을 사용하겠다.(reducer/inidex.js)
}

function mapDispatchToProps(dispatch) { // 액션관리함수, 컴포넌트의 특정 함수형 props를 실행했을 때 개발자가 지정한 action을 dispatch하도록 설정
  return bindActionCreators( {fetchPosts}, dispatch)
}
// connect(상태관리함수, 액션관리함수)(연결컴포넌트)
// or
// connect(null, 액션관리함수)(연결컴포넌트)
export default connect(mapStateToProps, mapDispatchToProps)(PostsIndex); ;

```



## posts_new.js(src/components)

```js
import React, { Component } from 'react';
import { Field, reduxForm } from 'redux-form';
import { Link } from 'react-router-dom';
import { connect } from 'react-redux';
import { createPost } from '../actions';

class PostsNew extends Component {
  renderField(field) {
    const { meta : {touched, error}} = field; //  meta = field.meta 
    // console.log(meta);
    // console.log("touched", touched);
    // console.log("error", error);
    const className = `form-group ${touched && error ? 'has-danger' : ''}`

    return (
      <div className={className}>
        <label>{field.label}</label>
        <input className="form-control" type="text" {...field.input} />
        <div className="text-help">
          {touched ? error : ''}
        </div>
      </div>
    )
  }

  onSubmit(values) {
    // submit values to creatPost function()
    this.props.createPost(values, () => {
      this.props.history.push('/')
    }); //클릭을 하게되면 저장된 값이 API server로 가게 된다.
  }

  render() {
    // const handleSubmit = this.props.handleSubmit;
    const { handleSubmit } = this.props;

    return (
      <form onSubmit={handleSubmit(this.onSubmit.bind(this))}>
        <Field label="Title For Post" name="title" component={this.renderField} />
        <Field label="Category" name="category" component={this.renderField} />
        <Field label="Blog contents" name="contents" component={this.renderField} />

        <button type="submit" className="btn btn-primary">Submit</button>
        <Link to="" className="btn btn-danger">Cancel</Link>
      </form>
    );
  }
}

function validate(values) {
  const errors = {}

  if (!values.title || values.title.length < 3) {
    errors.title = "제목을 3글자 이상 입력해 주세요.";
  }

  if (!values.category) {
    errors.category  = "카테고리를 지정해 주세요.";
  }

  if (!values.contents) {
    errors.contents  = "블로그의 내용을 입력해 주세요.";
  }

  return errors;
}


// export default PostsNew;
export default reduxForm({
   validate: validate,
   form: 'PostsNewForm'
})( connect(null, { createPost } )(PostsNew));
```



## posts_show.js(src/components)

```js
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { Link } from 'react-router-dom';
import { fetchPost, deletePost } from '../actions';

class PostsShow extends Component {
  componentDidMount() {
    // if(!this.props.post) {
      const { id } = this.props.match.params;
      this.props.fetchPost(id);
    // }
  }

  onDeleteClick() {
    const {id} = this.props.match.params;
    this.props.deletePost(id, () => {
      this.props.history.push('/');
    });
  }

  render() {
    const { post } = this.props;
    if(!post){
      return <div>Loading...</div>
    }
    return (
      <div>
        <Link to="/">back to index</Link>
        <button className="btn btn-danger pull-xs-right" 
        onClick={this.onDeleteClick.bind(this)}>delete post</button>

        <h3>{post.title}</h3>
        <h6>category: {post.category}</h6>
        <p>{post.contents}</p>
      </div>
    );
  }
}

function mapStateToProps(state, ownProps) {
  //console.log(state);
  return {
    post: state.posts[ownProps.match.params.id]
  };
}

export default connect(mapStateToProps, {fetchPost, deletePost})(PostsShow);
```



## index.js(src/reducers)

```js
import { combineReducers } from 'redux';
import PostsReducer from './reducer_post';
import { reducer as formReducer } from 'redux-form';

const rootReducer = combineReducers({
    posts: PostsReducer, // reducer_post.js 값을 불러온다.
    form: formReducer
});

export default rootReducer;

```



## reducer_post.js(src/reducers)

```js
import { FETCH_POSTS, CREATE_POST, FETCH_POST, DELETE_POST } from "../actions";
import _ from 'lodash';

export default function(state = {}, action) {
    switch (action.type) {
        case FETCH_POSTS:
            //console.log(action.payload.data);
            // return action.payload.data.blogs;
            return _.mapKeys(action.payload.data.blogs, 'id');
        case FETCH_POST:
            // return action.payload.data;
            
            return {...state, [action.payload.data.blog.id]: action.payload.data.blog}

        //case CREATE_POST:

        //case DELETE_POST:

        default:
            return state;   
    }
}
```

