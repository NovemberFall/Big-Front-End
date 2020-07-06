# 11. YouTubeBrowser App

## App Overview

![](img/2019-12-31-13-35-10.png)
---

## Component Design

![](img/2019-12-31-13-35-59.png)
![](img/2019-12-31-13-54-13.png)
---

## Scaffolding the App

- create a new project named `videos`

- `npx create-react-app videos`

- delete all files from src folder

- create index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './components/App';

ReactDOM.render(<App />, document.querySelector('#root'));
```

- create App.js, index import App

```js
import React from 'react';
import SearchBar from './SearchBar';
class App extends React.Component {
    render() {
        return <div><SearchBar /></div>;
    }
}
export default App;
```

- create SearchBar.js

```js
import React from 'react';

class SearchBar extends React.Component {
    render() {
        return <div>SearchBar</div>;
    }
}
export default SearchBar;
```

![](img/2019-12-31-16-44-10.png)
---


## Reminder on Event Handlers

- import semantic.css into index.html

- `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css" />`
 
- update SearchBar.js

```js
//Reminder on Event Handlers
import React from 'react';

class SearchBar extends React.Component {
    render() {
        return (
            <div className="search-bar ui segment">
                <form className="ui form">
                    <div className='field'>
                        <label>Video Search</label>
                        <input type="text" />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```

- update App

```js
//Reminder on Event Handlers
import React from 'react';
import SearchBar from './SearchBar';
class App extends React.Component {
    render() {
        return (
            <div className="ui container">
                <SearchBar />
            </div>
        );
    }
}
export default App;
```

![](img/2019-12-31-20-59-21.png)
---

- update SearchBar

```js
//Reminder on Event Handlers
import React from 'react';

class SearchBar extends React.Component {
    state = { term: 'Hello world!' }
    render() {
        return (
            <div className="search-bar ui segment">
                <form className="ui form">
                    <div className='field'>
                        <label>Video Search</label>
                        <input type="text" value={this.state.term} />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```

![](img/2019-12-31-21-06-26.png)

- the warning states that we should provide a `onChange`

---

## Handling Form Submittal

- update SearchBar

```js
//Reminder on Event Handlers
import React from 'react';

class SearchBar extends React.Component {
    state = { term: '' }

    onInputChange = (event) => {
        this.setState({ term: event.target.value })
    };

    onFormSubmit = (event) => {
        event.preventDefault();

        //TODO: Make sure we call
        //callback from parent component
    };

    render() {
        return (
            <div className="search-bar ui segment">
                <form onSubmit={this.onFromSubmit} className="ui form">
                    <div className='field'>
                        <label>Video Search</label>
                        <input type="text"
                            value={this.state.term}
                            onChange={this.onInputChange}
                        />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```

---


## Accessing the Youtube API

![](img/2019-12-31-22-31-01.png)

- go to google API

- `console.developers.google.com`

![](img/2019-12-31-22-36-46.png)
![](img/2019-12-31-22-37-12.png)

- click `NEW PROJECT`

![](img/2019-12-31-22-39-24.png)

- click `create`

![](img/2019-12-31-22-41-26.png)

- choose and click `videos browser `

![](img/2019-12-31-22-42-15.png)

- click `ENABLE APIS AND SERVICES`

![](img/2019-12-31-22-51-48.png)

- on search bar, input `youtube`

![](img/2019-12-31-22-52-24.png)

- choose `YouTube Data API v3`

- click

![](img/2019-12-31-22-55-37.png)

- click `ENABLE`

![](img/2019-12-31-22-56-57.png)
![](img/2019-12-31-22-59-47.png)
![](img/2019-12-31-23-01-01.png)

- copied this key

- go back to our app

![](img/2019-12-31-23-02-29.png)

- create `apis` -> `youtube.js`

- pass current copied key into `youtube.js`

---

## Searching for Videos

- google search `youtube api search`

![](img/2020-01-01-10-22-51.png)

- `GET https://www.googleapis.com/youtube/v3/search`

- the base URL is : `https://www.googleapis.com/youtube/v3/`

- create youtube.js

```js
import axios from 'axios';
const KEY = 'AIzaSyCKFtJ8pTpAqg2JVfyPMfUzMS-LKX9qr2E';
export default axios.create({
    baseURL: 'https://www.googleapis.com/youtube/v3/',
    params: {
        part: 'snippet',
        maxResults: 5,
        key: KEY
    }
});
```

- install axios

- `npm install --save axios@0.18.1`

---


## Adding a Video Type

- At some point in the course you may end up getting **Warning: Each child in a list should have a unique "key" prop** 
  even after we add a key prop in the "Fixing a Few Warnings" lecture. 
  To ensure that this is not an issue, we should add a type parameter 
  to our axios config object to only search for videos.

- update youtube.js

```js
import axios from 'axios';
const KEY = 'AIzaSyCKFtJ8pTpAqg2JVfyPMfUzMS-LKX9qr2E';

export default axios.create({
    baseURL: 'https://www.googleapis.com/youtube/v3/',
    params: {
        part: 'snippet',
        type: 'video',
        maxResults: 5,
        key: `${KEY}`
    }
});
```

---

## Putting it ALL Together

- update App

```js
//Putting it ALL Together
import React from 'react';
import SearchBar from './SearchBar';
class App extends React.Component {
    onTermSubmit = (term) => {
        console.log(term);
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
            </div>
        );
    }
}
export default App;
```

- update SearchBar

```js
// Putting it ALL Together
import React from 'react';

class SearchBar extends React.Component {
    state = { term: '' }

    onInputChange = (event) => {
        this.setState({ term: event.target.value })
    };

    onFormSubmit = (event) => {
        event.preventDefault();

        //TODO: Make sure we call
        //callback from parent component
        this.props.onFormSubmit(this.state.term);
    };

    render() {
        return (
            <div className="search-bar ui segment">
                <form onSubmit={this.onFormSubmit} className="ui form">
                    <div className='field'>
                        <label>Video Search</label>
                        <input type="text"
                            value={this.state.term}
                            onChange={this.onInputChange}
                        />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```

- Note: without `event.preventDefault();`, it can't print msg that you input

![](img/2020-01-01-11-41-35.png)

- update App

```js
//Putting it ALL Together
import React from 'react';
import SearchBar from './SearchBar';
import youtube from '../apis/youtube';

class App extends React.Component {
    onTermSubmit = (term) => {
        youtube.get('/search', {
            params: {
                q: term
            }
        });
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
            </div>
        );
    }
}
export default App;
```

![](img/2020-01-01-12-44-56.png)
![](img/2020-01-01-12-45-49.png)

---

## Updating State with Fetched Data

- update App

```js
class App extends React.Component {
    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });

        console.log(response);
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
            </div>
        );
    }
}
```

![](img/2020-01-01-12-52-07.png)

- note: the `items` is an array(5)
 
- update App

```js
class App extends React.Component {
    state = { videos: [] };

    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });
        // console.log(response);
        this.setState({ videos: response.data.items });
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
                I have {this.state.videos.length} videos.
            </div>
        );
    }
}
```

![](img/2020-01-01-12-57-30.png)
![](img/2020-01-01-12-57-49.png)
![](img/2020-01-01-12-58-43.png)
---

## Passing State as Props

- now let's review the plan agian:

![](img/2020-01-01-13-37-49.png)
![](img/2020-01-01-13-38-49.png)

- create VideoList.js

```js
import React from 'react';

const VideoList = (props) => {
    //props.videos
    return <div>{props.videos.length}</div>;
}
export default VideoList;
```

- update App

```js
//Passing State as Props
import React from 'react';
import SearchBar from './SearchBar';
import youtube from '../apis/youtube';
import VideoList from './VideoList';

class App extends React.Component {
    state = { videos: [] };

    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });
        // console.log(response);
        this.setState({ videos: response.data.items });
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
                <VideoList videos={this.state.videos} />
            </div>
        );
    }
}
export default App;
```

![](img/2020-01-01-13-46-43.png)

- Note: we pass props ` <VideoList videos={this.state.videos} />`  to child `VideoList`

---


## Rendering a List of Videos

- ` <VideoList videos={this.state.videos} />`, we receive props from parent `App`

- update VideoList

```js
//Rendering a List of Videos
import React from 'react';

const VideoList = ({ videos }) => {
    //props.videos
    return <div>{videos.length}</div>;
}
export default VideoList;
```

- create VideoItem.js

```js
import React from 'react';

const VideoItem = (props) => {
    return <div>Video Item</div>;
};
export default VideoItem;
```

- for every video inside VideoList there we will render one signle video item component

- update VideoList.js

```js
//Rendering a List of Videos
import React from 'react';
import VideoItem from './VideoItem';

const VideoList = ({ videos }) => {
    const renderedList = videos.map((video) => {
        return <VideoItem />;
    });
    //props.videos
    return <div>{renderedList}</div>;
}
export default VideoList;
```

![](img/2020-01-01-13-58-30.png)

- there is warnning

---

## Rendering Video Thumbnails

- we can pass props from VideoList to VideoItem

- update VideoList.js

```js
//Rendering Video Thumbnails
import React from 'react';
import VideoItem from './VideoItem';

const VideoList = ({ videos }) => {
    const renderedList = videos.map((video) => {
        return <VideoItem video={video} />;
    });
    //props.videos
    return <div>{renderedList}</div>;
}
export default VideoList;
```

- note: we pass props `video` to child `VideoItem`

![](img/2020-01-01-14-05-38.png)

- update VideoItem.js

```js
//Rendering Video Thumbnails
import React from 'react';

const VideoItem = ({ video }) => {
    return <div>{video.snippet.title}</div>;
};
export default VideoItem;
```

![](img/2020-01-01-14-26-26.png)

- but we need to print `thumbnail`

![](img/2020-01-01-14-30-40.png)

- update VideoItem

```js

//Rendering Video Thumbnails
import React from 'react';

const VideoItem = ({ video }) => {
    return (
        <div>
            <img src={video.snippet.thumbnails.medium.url} />
            {video.snippet.title}
        </div>
    );
};
export default VideoItem;
```

![](img/2020-01-01-14-34-19.png)
---

## Styling a List

![](img/2020-01-01-14-36-27.png)

- go to semantic-UI

- view `List`, to copy the example's source code

- update VideoList

```js
const VideoList = ({ videos }) => {
    const renderedList = videos.map((video) => {
        return <VideoItem video={video} />;
    });
    //props.videos
    return <div className="ui relaxed divided list">{renderedList}</div>;
}
```

- update VideoItem

```js
const VideoItem = ({ video }) => {
    return (
        <div className="item">
            <img src={video.snippet.thumbnails.medium.url} />
            {video.snippet.title}
        </div>
    );
};
```

- we added two className

- then we go down to looking for `Image` on Semantic UI

![](img/2020-01-01-14-42-14.png)

- view its source code

- update VideoItem

```js
//Styling a List
import React from 'react';
import './VideoItem.css';

const VideoItem = ({ video }) => {
    return (
        <div className="video-item item">
            <img className="ui image" src={video.snippet.thumbnails.medium.url} />
            <div className="content">
                <div className="header">{video.snippet.title}</div>
            </div>
        </div>
    );
};
export default VideoItem;
```

- create VideoItem.css

```css
.video-item{
    display: flex !important;
    align-items: center !important;
    cursor: pointer;
}

.video-item.item img{
    max-width: 180px;
}
```

![](img/2020-01-01-15-19-49.png)
---

## Communicating from Child to Parent

![](img/2020-01-01-15-22-00.png)

![](img/2020-01-01-15-27-28.png)

---

## Deeply Nested Callbacks

- the idea is `Communicating from Child to Parent`

- App using `this.state.value` to assign to children

- update App.js

```js
//Deeply Nested Callbacks
import React from 'react';
import SearchBar from './SearchBar';
import youtube from '../apis/youtube';
import VideoList from './VideoList';

class App extends React.Component {
    state = { videos: [], selectedVideo: null };

    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });
        // console.log(response);
        this.setState({ videos: response.data.items });
    };

    onVideoSelect = (video) => {
        console.log('From the App!', video);
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
                <VideoList onVideoSelect={this.onVideoSelect} videos={this.state.videos} />
            </div>
        );
    }
}
export default App;
```

- assign props.value `onVideoSelect={this.onVideoSelect}` to child `VideoList`

- update VideoList

```js
//Deeply Nested Callbacks
import React from 'react';
import VideoItem from './VideoItem';

const VideoList = ({ videos, onVideoSelect }) => {
    const renderedList = videos.map((video) => {
        return <VideoItem onVideoSelect={onVideoSelect} video={video} />;
    });
    //props.videos
    return <div className="ui relaxed divided list">{renderedList}</div>;
}
export default VideoList;
```

- VideoList pass props to child `VideoItem`

- VideoItem receive `onVideoSelect` from props

- update VideoItem

```js
//Deeply Nested Callbacks
import React from 'react';
import './VideoItem.css';

const VideoItem = ({ video, onVideoSelect }) => {
    return (
        <div onClick={() => { onVideoSelect(video) }} className="video-item item">
            <img className="ui image" src={video.snippet.thumbnails.medium.url} />
            <div className="content">
                <div className="header">{video.snippet.title}</div>
            </div>
        </div>
    );
};
export default VideoItem;
```

![](img/2020-01-01-15-57-59.png)
![](img/2020-01-01-16-14-51.png)

- Remember! we passing props to child VideoList and down to VideoItem, 
  hen whenever a user clicked on a video item we invoked that callback 
  which essentially sent some communication back to the app component**

---

## Conditional Rendering

![](img/2020-01-01-17-26-04.png)

- create VideoDetail.js

```js
//Conditional Rendering
import React from 'react';
const VideoDetail = ({ video }) => {
    if (!video) {
        return <div>Loading...</div>
    }
    return <div>{video.snippet.title}</div>
}
export default VideoDetail;
```

- update App

```js
//Conditional Rendering
import React from 'react';
import SearchBar from './SearchBar';
import youtube from '../apis/youtube';
import VideoList from './VideoList';
import VideoDetail from './VideoDetail';

class App extends React.Component {
    state = { videos: [], selectedVideo: null };

    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });
        // console.log(response);
        this.setState({ videos: response.data.items });
    };

    onVideoSelect = (video) => {
        this.setState({ selectedVideo: video })
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
                <VideoDetail video={this.state.selectedVideo} />
                <VideoList onVideoSelect={this.onVideoSelect} videos={this.state.videos} />
            </div>
        );
    }
}
export default App;
```

![](img/2020-01-01-17-37-36.png)
---


## Styling the VideoDetail

- update VideoDetail

```js
//Styling the VideoDetail
import React from 'react';
const VideoDetail = ({ video }) => {
    if (!video) {
        return <div>Loading...</div>
    }
    return (
        <div>
            <div className="ui segment">
                <h4 className="ui header">{video.snippet.title}</h4>
                <p>{video.snippet.description}</p>
            </div>
        </div>
    );
}
export default VideoDetail;
```

![](img/2020-01-01-17-42-22.png)
---

## Displaying a Video Player

- let's review diagram again

![](img/2020-01-01-17-43-50.png)

- go to youtube

- find a vedio, and click `SHARE`

![](img/2020-01-01-19-11-33.png)

- click `Embed`

![](img/2020-01-01-19-14-07.png)

- update VideoDetail

```js
//Displaying a Video Player
import React from 'react';
const VideoDetail = ({ video }) => {
    if (!video) {
        return <div>Loading...</div>
    }

    const videoSrc = `https://www.youtube.com/embed/${video.id.videoId}`
    return (
        <div>
            <div className="ui embed">
                <iframe src={videoSrc} />
            </div>
            <div className="ui segment">
                <h4 className="ui header">{video.snippet.title}</h4>
                <p>{video.snippet.description}</p>
            </div>
        </div>
    );
}
export default VideoDetail;
```

![](img/2020-01-01-19-36-08.png)
---

## Fixing a Few Warnings

![](img/2020-01-01-19-40-06.png)

- update VideoDetail

```js
//Fixing a Few Warnings
import React from 'react';
const VideoDetail = ({ video }) => {
    if (!video) {
        return <div>Loading...</div>
    }

    const videoSrc = `https://www.youtube.com/embed/${video.id.videoId}`
    return (
        <div>
            <div className="ui embed">
                <iframe title="video player" src={videoSrc} />
            </div>
            <div className="ui segment">
                <h4 className="ui header">{video.snippet.title}</h4>
                <p>{video.snippet.description}</p>
            </div>
        </div>
    );
}
export default VideoDetail;
```

- update VideoItem.js

```js
//Fixing a Few Warnings
import React from 'react';
import './VideoItem.css';

const VideoItem = ({ video, onVideoSelect }) => {
    return (
        <div onClick={() => { onVideoSelect(video) }} className="video-item item">
            <img alt={video.snippet.title} className="ui image" src={video.snippet.thumbnails.medium.url} />
            <div className="content">
                <div className="header">{video.snippet.title}</div>
            </div>
        </div>
    );
};
export default VideoItem;
```

![](img/2020-01-01-19-53-18.png)

- now we still have a warning in VideoList

- update VideoList

```js
//Deeply Nested Callbacks
import React from 'react';
import VideoItem from './VideoItem';

const VideoList = ({ videos, onVideoSelect }) => {
    const renderedList = videos.map((video) => {
        return <VideoItem key={video.id.videoId} onVideoSelect={onVideoSelect} video={video} />;
    });
    //props.videos
    return <div className="ui relaxed divided list">{renderedList}</div>;
}
export default VideoList;
```

![](img/2020-01-01-19-59-35.png)

- there is no warnning

- now we try to list other videos on right hand side

![](img/2020-01-01-20-02-45.png)

- import semantic UI's Grid

![](img/2020-01-01-20-04-21.png)

- update App.js

```js
//Fixing a Few Warnings
import React from 'react';
import SearchBar from './SearchBar';
import youtube from '../apis/youtube';
import VideoList from './VideoList';
import VideoDetail from './VideoDetail';

class App extends React.Component {
    state = { videos: [], selectedVideo: null };

    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });
        // console.log(response);
        this.setState({ videos: response.data.items });
    };

    onVideoSelect = (video) => {
        this.setState({ selectedVideo: video })
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
                <div className="ui grid">
                    <div className="ui row">
                        <div className="eleven wide column">
                            <VideoDetail video={this.state.selectedVideo} />
                        </div>
                        <div className="five wide column">
                            <VideoList
                                onVideoSelect={this.onVideoSelect}
                                videos={this.state.videos}
                            />
                        </div>

                    </div>
                </div>
            </div>
        );
    }
}
export default App;
```

- according to Semantic UI, we know there are totally default 16 column wide

- thus, VideoDetail component occupied 11 wide, VideoList occupied 5 wide

![](img/2020-01-01-20-31-11.png)
---


## Defaulting Video Selection

- since we don't have a default videon on our searcBar page

- so we need to set a default video

- update App.js

```js
//Defaulting Video Selection
import React from 'react';
import SearchBar from './SearchBar';
import youtube from '../apis/youtube';
import VideoList from './VideoList';
import VideoDetail from './VideoDetail';

class App extends React.Component {
    state = { videos: [], selectedVideo: null };

    componentDidMount() {
        this.onTermSubmit('buildings');
    }

    onTermSubmit = async (term) => {
        const response = await youtube.get('/search', {
            params: {
                q: term
            }
        });
        // console.log(response);
        this.setState({
            videos: response.data.items,
            selectedVideo: response.data.items[0]
        });
    };

    onVideoSelect = (video) => {
        this.setState({ selectedVideo: video })
    };

    render() {
        return (
            <div className="ui container">
                <SearchBar onFormSubmit={this.onTermSubmit} />
                <div className="ui grid">
                    <div className="ui row">
                        <div className="eleven wide column">
                            <VideoDetail video={this.state.selectedVideo} />
                        </div>
                        <div className="five wide column">
                            <VideoList
                                onVideoSelect={this.onVideoSelect}
                                videos={this.state.videos}
                            />
                        </div>

                    </div>
                </div>
            </div>
        );
    }
}
export default App;
```

![](img/2020-01-01-21-36-48.png)

- now, everytime we rerender this page, it will display buildings