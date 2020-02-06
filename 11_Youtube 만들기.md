# Youtube 만들기

[google API Developer](https://console.developers.google.com/) -> YouTube Data API v3 -> api key 발급 받기



```js
# index.js

import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import YTSearch from 'youtube-api-search'
import SearchBar from './components/search_bar';
import VideoList from './components/video_list';
import VideoDetail from './components/video_detail';

const API_KEY = 'AIzaSyDhsBfgni4JKKwE0h_WU2hIBxgD28lCwxs';

class App extends Component {
  constructor(props) {
    super(props);   // 부모의 생성자 함수를 호출

    this.state = {
      videos: [],
      selectedVideo: null
    }

    YTSearch({ key: API_KEY, term: 'soccer' }, (data) => {
      this.setState({
        videos: data,
        selectedVideo: data[0]
      });
    });
  }

  videoSearch() {

  }

  handleSelect =(selectedVideo) => {
    // 선택된 video를 detail에 표시
    this.setState({
      selectedVideo: selectedVideo
    })
  }

  render() {
    return (
      <div>
        <SearchBar />
        <VideoDetail video={this.state.selectedVideo} />
        <VideoList 
          onVideoSelect={this.handleSelect}
          videos={this.state.videos} />
      </div>
    );
  }
}

ReactDOM.render(<App />, document.querySelector('.container'));
```



```js
# search_bar.js

import React, { Component } from 'react';

class SearchBar extends Component {
    constructor(props) {
        super(props);

        this.state = {
            term: ''
        }
    }

    onInputChange = (e) => {
        this.setState({
            term: e.target.value
        })
    }


    render() {
        return (
            <div className="search-bar">
                <input className="search-bar input"
                    onChange={this.onInputChange} />
            </div>
        );
    }
}
export default SearchBar;
```



```js
# video_list

import React from 'react';
import VideoListItem from './video_list_item';

const VideoList = (props) => {

    const videoItems = props.videos.map((video) => {
        return (
            <VideoListItem
                onVideoSelect={props.onVideoSelect}
                key={video.etag}
                video={video} />
        );
    });

    return (
        <ul className="col-md-4 list-group">
            {videoItems}
        </ul>
    )
}

export default VideoList;
```



```js
# video_detail.js

import React from 'react';

const VideoDetail = ({ video }) => { //root component = 부모
    if (!video) {
        return <div>Loading....</div>
    }

    const videoId = video.id.videoId;
    const url = `https://www.youtube.com/embed/${videoId}`;

    return (
        <div className="video-detail col-md-8">
            <div className="embed-responsive embed-responsive-16by9">
                <iframe className="embed-responsive-item" src={url} />
            </div>
            <div className="details">
                <div>{video.snippet.title}</div>
                <div>{video.snippet.description}</div>
            </div>
        </div>
    );
}

export default VideoDetail;
```



```js
# video_list_item.js

import React from 'react';


const VideoListItem = ({ video, onVideoSelect }) => {

    const imageUrl = video.snippet.thumbnails.default.url;
    //console.log(imageUrl);
    return (
        <li onClick={() => onVideoSelect(video)} className="list-group-item">
            <div className="video-list media">
                <div className="media-left">
                    <img className="media-object" src={imageUrl} />
                </div>
                <div className='media-body'>
                    <div className='media-heading'>
                        {video.snippet.title}
                    </div>
                </div>
            </div>
            {video.snippet.title}
        </li>
    )
}

export default VideoListItem;
```

