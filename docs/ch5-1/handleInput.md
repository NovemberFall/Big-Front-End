# 7. Handing UserInput With FormsAndEvents

## create a project named pics

```js
npx create-react-app my-app
cd my-app
npm start
```

![](img/2019-12-22-07-00-35.png)

- delete all files in src

- create folder components

![](img/2019-12-22-06-51-40.png)

- index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './components/App';

ReactDOM.render(
    <App />,
    document.querySelector('#root')
);
```

- App.js

```js
import React from 'react';

const App = () => {
    return <div>App</div>;
};

export default App;
```

![](img/2019-12-22-06-55-53.png)
---

## Showing Forms to the User

![](img/2019-12-22-06-59-56.png)

- update SearchBar.js, App.js

```js
import React from 'react';

class SearchBar extends React.Component {
    render() {
        return (
            <div>
                Search Bar
            </div>
        );
    }
}
export default SearchBar;


///////////


import React from 'react';
import SearchBar from './SearchBar';

const App = () => {
    return (
        <div>
            <SearchBar />
        </div>
    );
};

export default App;
```

![](img/2019-12-22-07-07-52.png)
---

#### update SearchBar.js

```js
import React from 'react';

class SearchBar extends React.Component {
    render() {
        return (
            <div>
                <form>
                    <input type="text" />
                </form>
            </div>
        );
    }
}
export default SearchBar;

// we add a input text into our component
```

![](img/2019-12-22-07-12-13.png)
---

## Adding a Touch of style

- import semantic-ui

- `https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css`

- add into index.html

![](img/2019-12-22-07-17-52.png)

- update App.js

```js
const App = () => {
    return (
        <div className="ui container" style={{ marginTop: '10px' }}>
            <SearchBar />
        </div>
    );
};

export default App;
```

- SearchBar.js

```js
class SearchBar extends React.Component {
    render() {
        return (
            <div className="ui segment">
                <form className="ui form">
                    <div className="field">
                        <label>Image Search</label>
                        <input type="text" />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```
---

## Creating Event Handler

- update SearchBar.js

```js
import React from 'react';

class SearchBar extends React.Component {
    onInputChange(event) {
        console.log(event.target.value);
    }
    render() {
        return (
            <div className="ui segment">
                <form className="ui form">
                    <div className="field">
                        <label>Image Search</label>
                        <input type="text" onChange={this.onInputChange} />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```

![](img/2019-12-22-07-31-29.png)
---

![](img/2019-12-22-07-33-21.png)
---

- update SearchBar.js

```js
class SearchBar extends React.Component {
    onInputChange(event) {
        console.log(event.target.value);
    }

    onInputClick() {
        console.log('Input was clicked');
    }
    render() {
        return (
            <div className="ui segment">
                <form className="ui form">
                    <div className="field">
                        <label>Image Search</label>
                        <input type="text"
                            onClick={this.onInputClick}
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

![](img/2019-12-22-07-38-12.png)
---


## Alternate Event Handle Syntax

- update searchbar.js

```js
class SearchBar extends React.Component {
    onInputChange(event) {
        console.log(event.target.value);
    }

    render() {
        return (
            <div className="ui segment">
                <form className="ui form">
                    <div className="field">
                        <label>Image Search</label>
                        <input type="text"
                            onChange={(e) => { console.log(e.target.value) }}
                        />
                    </div>
                </form>
            </div>
        );
    }
}
export default SearchBar;
```

![](img/2019-12-22-07-44-43.png)
---


## Uncontrolled VS Controlled Elements

- update SearchBar.js

```js
import React from 'react';

class SearchBar extends React.Component {
    state = { term: '' };

    render() {
        return (
            <div className="ui segment">
                <form className="ui form">
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

- so what is the point of all this stuff that we just added?

- Why are we using state?

- Why are we updating state whenever we change the input?

- Why are we passing something called value back into the input?

## More on Controlled Element

![](img/2019-12-22-08-02-45.png)

- for react world, we prefect `value={this.state.term}`

![](img/2019-12-22-08-18-09.png)
---

## Handing Form Sumbitted

- update SearchBar.js

```js
import React from 'react';

class SearchBar extends React.Component {
    state = { term: 'Hi there!' };

    onFormSubmit(event) {
        event.preventDefault();
        console.log(this.state.term);
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

- when we submitted

![](img/2019-12-22-08-31-33.png)

- but here has error

- there will be q quick and easy fix but understanding the fix can be just a little bit challenging sometimes.
---


## Understanding 'this' in JavaScript

![](img/2019-12-22-08-57-04.png)

- look at this example:

![](img/2019-12-22-09-09-13.png)
---


## Solving Context Issue

![](img/2019-12-22-09-32-14.png)

- so we can use ES6 arrow function to do so

- update SearchBark.js

```js
//2nd way to solve `this`, by using arrow function
import React from 'react';

class SearchBar extends React.Component {
    state = { term: 'Hi there!' };

    onFormSubmit = (event) => {
        event.preventDefault();
        console.log(this.state.term);
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

![](img/2019-12-22-09-34-57.png)

- now we see the error has gone!
---

### the 2nd way to solve `this`

- update searchbar.js

```js
//one way for solve `this`
import React from 'react';

class SearchBar extends React.Component {
    state = { term: 'Hi there!' };

    onFormSubmit(event) {
        event.preventDefault();
        console.log(this.state.term);
    }
    render() {
        return (
            <div className="ui segment">
                <form onSubmit={(event) => this.onFormSubmit(event)} className="ui form">
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

- still work
---


## Communicating Child to Parent

![](img/2019-12-22-09-46-15.png)

- we can only pass info from the app component down to SearchBar through `props`.


## Invoking Callbacks in Children

![](img/2019-12-22-09-52-31.png)

- update SearchBar.js

```js
//2nd way to solve `this`, by using arrow function
import React from 'react';

class SearchBar extends React.Component {
    state = { term: 'Hi there!' };

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

- update App.js

```js
class App extends React.Component {
    onSearchSubmit(term) {
        console.log(term);
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

![](img/2019-12-22-10-06-17.png)

- still work!