# 8. Making_API_Requests With React

## Fetching Data

![](img/2019-12-30-14-24-31.png)

- `https://unsplash.com/developers` api

- click `Register as a developer`

![](img/2019-12-30-14-32-38.png)

- click `your apps`

- `new application`

![](img/2019-12-30-14-41-09.png)
---

## Axios vs Fetch

![](img/2019-12-30-14-47-04.png)
![](img/2019-12-30-14-47-53.png)

- for axios is third party API, so we need to install

- the other option is the `fetch` function, which is a singular function that is build into almost all modern browsers.
 
- install axios

- `npm install --save axios`

---


### Viewing Request Results

- how to use API

- click `Documentaion`

- on the left navigation bar,

![](img/2019-12-30-15-10-18.png)

- `Schema`-> `location`

- The API is available at `https://api.unsplash.com/`. Responses are sent as JSON.
 
- update App.js in `pics` project

```js
//Axios vs Fetch, Viewing Request Results
import React from 'react';
import axios from 'axios';
import SearchBar from './SearchBar';
class App extends React.Component {
    onSearchSubmit(term) {
        axios.get('https://api.unsplash.com/search/photos', {

        });
    }

    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar
                    onSubmit={this.onSearchSubmit}
                />
            </div >
        );
    }
};
export default App;
```

- we have to actually identify ourselves and who is trying to access the Sunsplash API.

- the instruction: `https://unsplash.com/documentation#authorization`

![](img/2019-12-30-15-42-05.png)

- put our ACCESS_KEY into APP.js, go back to `Your apps` to find our key

![](img/2019-12-30-15-48-40.png)

- copy our `Access Key`

- go to `Search`-> `Search photos`

- update App.js

```js
//Axios vs Fetch, Viewing Request Results
import React from 'react';
import axios from 'axios';
import SearchBar from './SearchBar';
class App extends React.Component {
    onSearchSubmit(term) {
        axios.get('https://api.unsplash.com/search/photos', {
            params: { query: term },
            headers: {
                Authorization: 'Client-ID 06162288b9848c9af42616ef69fd67b3c13761510fc01192ffa9aaabef240ffb'
            }
        });
    }
    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar
                    onSubmit={this.onSearchSubmit}
                />
            </div >
        );
    }
};
export default App;
```
![](img/2019-12-30-16-01-38.png)

- input `cars`

- we get those pthotos

---

## Handling Request with Async Await

![](img/2019-12-30-16-10-25.png)
![](img/2019-12-30-16-11-10.png)

- in the original plan we put together we had said that we would make a new component called `imageList`

- App.js

```js
class App extends React.Component {
    onSearchSubmit(term) {
        axios.get('https://api.unsplash.com/search/photos', {
            params: { query: term },
            headers: {
                Authorization: 'Client-ID 06162288b9848c9af42616ef69fd67b3c13761510fc01192ffa9aaabef240ffb'
            }
        }).then((response) => {
            console.log(response);
        });
    }

    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar
                    onSubmit={this.onSearchSubmit}
                />
            </div >
        );
    }
};
```

![](img/2019-12-30-16-17-33.png)

- update

```js
    onSearchSubmit(term) {
        axios.get('https://api.unsplash.com/search/photos', {
            params: { query: term },
            headers: {
                Authorization: 'Client-ID 06162288b9848c9af42616ef69fd67b3c13761510fc01192ffa9aaabef240ffb'
            }
        }).then((response) => {
            console.log(response.data.results);
        });
    }
```

![](img/2019-12-30-16-19-00.png)

- this is first method to use, return a promise that is object, and call .then() method

- 2nd method, by using Async Await

- App.js

```js
class App extends React.Component {
    async onSearchSubmit(term) {
        const response = await axios.get('https://api.unsplash.com/search/photos', {
            params: { query: term },
            headers: {
                Authorization: 'Client-ID 06162288b9848c9af42616ef69fd67b3c13761510fc01192ffa9aaabef240ffb'
            }
        });
        console.log(response.data.results);
    }
    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar
                    onSubmit={this.onSearchSubmit}
                />
            </div >
        );
    }
};
```

- same results

---

## Setting State After Async Requests

- SearchBar.js

```js
//2nd way to solve `this`, by using arrow function
import React from 'react';

class SearchBar extends React.Component {
    state = { term: '' };

    onFormSubmit = (event) => {
        event.preventDefault();
        this.props.onSubmit(this.state.term);
    }
    render() {
        return (
            <div className="ui segment">
                <form onSubmit={this.onFormSubmit} className="ui form">
                    <div className="field">
                        <label>Image Search</label>
                        <input type="text"
                            value={this.state.term}
                            onChange={(e) => this.setState({ term: e.target.value })}
                        />
                    </div>
                </form>
            </div>
        );
    }

}
export default SearchBar;
```

- App.js

```js
import React from 'react';
import axios from 'axios';
import SearchBar from './SearchBar';
class App extends React.Component {
    state = { images: [] }

    async onSearchSubmit(term) {
        const response = await axios.get('https://api.unsplash.com/search/photos', {
            params: { query: term },
            headers: {
                Authorization: 'Client-ID 06162288b9848c9af42616ef69fd67b3c13761510fc01192ffa9aaabef240ffb'
            }
        });

        this.setState({ images: response.data.results });
    }

    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar onSubmit={this.onSearchSubmit} />
                Found: {this.state.images.length} images;
            </div >
        );
    }
};
export default App;
```

![](img/2019-12-30-16-54-07.png)

- here is error

---


## Binding Callbacks

- update App.js

```js
//Binding Callbacks
import React from 'react';
import axios from 'axios';
import SearchBar from './SearchBar';
class App extends React.Component {
    state = { images: [] }

    onSearchSubmit = async (term) => {
        const response = await axios.get('https://api.unsplash.com/search/photos', {
            params: { query: term },
            headers: {
                Authorization: 'Client-ID 06162288b9848c9af42616ef69fd67b3c13761510fc01192ffa9aaabef240ffb'
            }
        });

        this.setState({ images: response.data.results });
    }

    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar onSubmit={this.onSearchSubmit} />
                Found: {this.state.images.length} images;
            </div >
        );
    }
};
export default App;
```

![](img/2019-12-30-16-58-46.png)
---

## Creating Custom Clients

- create a new floder api/unpslash.js

![](img/2019-12-30-17-09-48.png)

- update App.js

```js
//Creating Custom Clients
import React from 'react';
import unsplash from '../api/unpslash';
import SearchBar from './SearchBar';
class App extends React.Component {
    state = { images: [] }

    onSearchSubmit = async (term) => {
        const response = await unsplash.get('search/photos', {
            params: { query: term }
        });

        this.setState({ images: response.data.results });
    }

    render() {
        return (
            <div className="ui container" style={{ marginTop: '10px' }}>
                <SearchBar onSubmit={this.onSearchSubmit} />
                Found: {this.state.images.length} images;
            </div >
        );
    }
};
export default App;
```

![](img/2019-12-30-17-11-01.png)
