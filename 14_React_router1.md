![캡처](https://user-images.githubusercontent.com/42603919/74495391-1f88ed00-4f1b-11ea-9656-f2bd691b0904.PNG)

```js
# App.js

import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import About from './routes/About'
import Home from './routes/Home'
import Header from './components/header';
import Posts from './routes/Posts';
import Login from './routes/Login';
import MyProfile from './routes/MyProfile';
import Search from './routes/Search';
import NotFound from './routes/NotFound';

const App = () => {
  return (
    <Router>
      <Header />
      <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/about/:userid" component={About} />
      <Route path="/posts" component={Posts} />
      <Route path="/search" component={Search} />
      <Route path="/login" component={Login} />
      <Route path="/myprofile" component={MyProfile} />
      <Route component={NotFound} />
      </Switch>
    </Router>    
  );
};

export default App;
```



```js
# header.js 

import React from 'react';
import { NavLink } from 'react-router-dom'
import './Header.css'

const Header = () => {
    return (
        <div className='header'>
            <NavLink exact to="/" className='item'>Home</NavLink>
            <NavLink to="/about/younggwon" className='item'>About</NavLink>
            <NavLink to="/posts" className='item'>posts</NavLink>
            <NavLink to="/login" className='item'>login</NavLink>
            <NavLink to="/myprofile" className='item'>myprofile</NavLink>
            <NavLink to="/search" className='item'>search</NavLink>
        </div>
    );
};

export default Header;

```



```js
# About.js

import React from 'react';

const About = ({match}) => {
    return (
        <div>
            {match.params.userid}'s Profile
        </div>
    );
};

export default About;
```



```js
# Home.js

import React from 'react';

const Home = () => {
    return (
        <div>
            Home
        </div>
    );
};

export default Home;
```



```js
# Login.js

import React from 'react';

const Login = () => {
    return (
        <div>
            login
        </div>
    );
};

export default Login;
```



```js
# MyProfile.js

import React from 'react';
import { Redirect } from 'react-router-dom'

const isLogged = true;

const MyProfile = () => {
    return (
        <div>
            {
                !isLogged && <Redirect to="/login" />
            }
        </div>
    );
};

export default MyProfile;
```



```js
# NotFound.js

import React from 'react';

const NotFound = () => {
    return (
        <div>
            페이지가 존재하지 않습니다.
        </div>
    );
};

export default NotFound;
```



```js
# Posts.js

import React from 'react';
import { Link, Route } from 'react-router-dom';

const Post = ({match}) => {
    return (
        <h3>{match.params.title}</h3>
    )
}

const Posts = () => {
    return (
        <div>
            <h2>Posts</h2>
            <ul>
            <li><Link to='/posts/java'>java programming</Link></li>
            <li><Link to='/posts/react'>react programming</Link></li>
            <li><Link to='/posts/js'>javascript</Link></li>
            <li><Link to='/posts/msa'>microservice</Link></li>

            <Route path="/posts/:title" component={Post} />
            </ul>
        </div>
    );
};

export default Posts;
```



```js
# Search.js

import React from 'react';

const Search = ({location}) => {
    return (
        <div>
            {/*Search keyword: {location.search}*/}
            Search keyword: {new URLSearchParams(location.search).get("keyword")}
        </div>
    );
};

export default Search;
```



