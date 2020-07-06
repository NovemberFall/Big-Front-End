# 6. Understanding Lifecycle Methods

![](img/2019-12-28-10-56-33.png)

- added lifecycle function

- update index.js

```js
//Conditionally Rendering Content
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
    constructor(props) {
        super(props);

        //THIS IS THE ONLY TIME we do direct assignment to this.state
        this.state = { lat: null, errorMessage: '' };

        window.navigator.geolocation.getCurrentPosition(
            (position) => {
                //we called setState
                this.setState({ lat: position.coords.latitude });

                //we never do this:
                // this.state.lat = position.coords.latitude;
            },
            (err) => {
                this.setState({ errorMessage: err.message });
            }
        );
    };

    //life cycle function
    componentDidMount() {
        console.log('My component was rendered to the screen');
    }

    componentDidUpdate() {
        console.log('My component was just updated - it rerendered!');
    }


    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <div>Latitude: {this.state.lat}</div>
        }

        return <div>Loading!</div>
    }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

![](img/2019-12-28-12-24-33.png)
---

## Why Lifecycle Methods?

![](img/2019-12-28-12-26-23.png)
---


## Refactoring Data Loading to Lifecycle Methods

- update index.js

```js
//Refactoring Data Loading to Lifecycle Methods
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
    constructor(props) {
        super(props);

        //THIS IS THE ONLY TIME we do direct assignment to this.state
        this.state = { lat: null, errorMessage: '' };


    };

    //life cycle function
    componentDidMount() {
        window.navigator.geolocation.getCurrentPosition(
            (position) => { this.setState({ lat: position.coords.latitude }); },
            (err) => { this.setState({ errorMessage: err.message }); }
        );
    }

    componentDidUpdate() {
        console.log('My component was just updated - it rerendered!');
    }


    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <div>Latitude: {this.state.lat}</div>
        }

        return <div>Loading!</div>
    }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

![](img/2019-12-28-14-34-52.png)
---

## Alternate State Intialization

- index.js

```js
class App extends React.Component {
    state = { lat: null, errorMessage: '' };//dont need to `this.state =`

    ... ... ...
    ... ...
    ... 
```

- same result

---

## Passing State as Props

- unpdate index.js

```js
//Passing State as Props
import React from 'react';
import ReactDOM from 'react-dom';
import SeasonDisplay from './SeasonDisplay';

class App extends React.Component {
    state = { lat: null, errorMessage: '' };//dont need to `this.state =`

    //life cycle function
    componentDidMount() {
        window.navigator.geolocation.getCurrentPosition(
            (position) => { this.setState({ lat: position.coords.latitude }); },
            (err) => { this.setState({ errorMessage: err.message }); }
        );
    }

    componentDidUpdate() {
        console.log('My component was just updated - it rerendered!');
    }


    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <SeasonDisplay lat={this.state.lat} />
        }

        return <div>Loading!</div>
    }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

- update SeasonDisplay.js

```js
import React from 'react';

const SeasonDisplay = (props) => {
    console.log(props.lat);
    return <div>Seanson Display</div>;
};
export default SeasonDisplay;
```

![](img/2019-12-28-14-59-54.png)
---

## Determining Season

![](img/2019-12-28-15-00-42.png)

- in console, typing `new Date().getMonth()`

![](img/2019-12-28-15-04-26.png)

- index.js

```js
//Determining Season
import React from 'react';
import ReactDOM from 'react-dom';
import SeasonDisplay from './SeasonDisplay';

class App extends React.Component {
    state = { lat: null, errorMessage: '' };//dont need to `this.state =`

    //life cycle function
    componentDidMount() {
        window.navigator.geolocation.getCurrentPosition(
            (position) => { this.setState({ lat: position.coords.latitude }); },
            (err) => { this.setState({ errorMessage: err.message }); }
        );
    }

    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <SeasonDisplay lat={this.state.lat} />
        }

        return <div>Loading!</div>
    }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

- update SeasonDisplay.js

```js
import React from 'react';

const getSeason = (lat, month) => {
    if (month > 2 && month < 9) {
        return lat > 0 ? 'summer' : 'winter';
    } else {
        return lat > 0 ? 'winter' : 'summer';
    }
};

const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    console.log(season);

    return <div>Seanson Display</div>;
};
export default SeasonDisplay;
```

![](img/2019-12-28-15-17-35.png)
---


## Ternary Expressions in JSX

![](img/2019-12-28-15-19-06.png)

- update SeasonDisplay

```js
//Ternary Expressions in JSX
import React from 'react';

const getSeason = (lat, month) => {
    if (month > 2 && month < 9) {
        return lat > 0 ? 'summer' : 'winter';
    } else {
        return lat > 0 ? 'winter' : 'summer';
    }
};

const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    console.log(season);

    return <div>{season === 'winter' ? 'Burr, it is chilly' : 'Lets hit the beach'}</div>;
};
export default SeasonDisplay;
```

![](img/2019-12-28-15-24-01.png)
---


## Showing Icons

- Semantic UI

- update SeasonDisplay

```js
import React from 'react';

const getSeason = (lat, month) => {
    if (month > 2 && month < 9) {
        return lat > 0 ? 'summer' : 'winter';
    } else {
        return lat > 0 ? 'winter' : 'summer';
    }
};

const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    const text = (season === 'winter' ? 'Burr, it is chilly' : 'Lets hit the beach');
    const icon = (season === 'winter' ? 'snowflake' : 'sun');

    return (
        <div>
            <i className={`${icon} icon`} />
            <h1>{text}</h1>
            <i className={`${icon} icon`} />
        </div>
    );
};
export default SeasonDisplay;
```

![](img/2019-12-28-15-36-26.png)
---

## Extracting Options to Config Objects

- update SeasonDisplay.js

```js
//Extracting Options to Config Objects
import React from 'react';

const seasonConfig = {
    summer: {
        text: 'Lets hit the beach!',
        iconName: 'sun'
    },
    winter: {
        text: 'Burr it is cold!',
        iconName: 'snowflake'
    }
};

const getSeason = (lat, month) => {
    if (month > 2 && month < 9) {
        return lat > 0 ? 'summer' : 'winter';
    } else {
        return lat > 0 ? 'winter' : 'summer';
    }
};

const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    const { text, iconName } = seasonConfig[season];

    return (
        <div>
            <i className={`${iconName} icon`} />
            <h1>{text}</h1>
            <i className={`${iconName} icon`} />
        </div>
    );
};
export default SeasonDisplay;
```

![](img/2019-12-28-15-46-03.png)
---


## Adding Some Styling

- in SeasonDisplay

```js
    return (
        <div>
            <i className={`massive ${iconName} icon`} />
            <h1>{text}</h1>
            <i className={`massive ${iconName} icon`} />
        </div>
    );
```

![](img/2019-12-28-15-50-16.png)

- create a .css file

![](img/2019-12-28-15-52-39.png)

- SeasonDisplay.css

```css
.icon-left{
    position: absolute;
    top: 10px;
    left: 10px;
}

.icon-right{
    position: absolute;
    bottom:10px;
    right: 10px;
}
```

- update SeasonDisplay.js

```js
const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    const { text, iconName } = seasonConfig[season];

    return (
        <div>
            <i className={`icon-left massive ${iconName} icon`} />
            <h1>{text}</h1>
            <i className={`icon-right massive ${iconName} icon`} />
        </div>
    );
};
```

![](img/2019-12-28-15-57-53.png)
---

- update SeansonDisplay.css

```css
.icon-left{
    position: absolute;
    top: 10px;
    left: 10px;
}

.icon-right{
    position: absolute;
    bottom:10px;
    right: 10px;
}

.season-display.winter i{
    color: blue;
}

.season-display.summer i{
    color: red;
}

.season-display{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.winter{
    background-color: aliceblue;
}

.summer{
    background-color: orange;
}
```

- update SeansonDisplay.js

```js
//Adding Some Styling
import React from 'react';
import './SeasonDisplay.css';

const seasonConfig = {
    summer: {
        text: 'Lets hit the beach!',
        iconName: 'sun'
    },
    winter: {
        text: 'Burr it is cold!',
        iconName: 'snowflake'
    }
};

const getSeason = (lat, month) => {
    if (month > 2 && month < 9) {
        return lat > 0 ? 'summer' : 'winter';
    } else {
        return lat > 0 ? 'winter' : 'summer';
    }
};

const SeasonDisplay = (props) => {
    const season = getSeason(props.lat, new Date().getMonth());
    const { text, iconName } = seasonConfig[season];

    return (
        <div className={`season-display ${season}`}>
            <i className={`icon-left massive ${iconName} icon`} />
            <h1>{text}</h1>
            <i className={`icon-right massive ${iconName} icon`} />
        </div>
    );
};
export default SeasonDisplay;
```

![](img/2019-12-28-16-14-32.png)

- let's change to Southern Hemisphere

![](img/2019-12-28-16-21-03.png)
---

## Showing a Loading Spinner

- create a `Spinner.js`

```js
import React from 'react';

const Spinner = () => {
    return (
        // using Semantic UI
        <div className="ui active dimmer"> 
            <div className="ui big text loader">
                Loading...
            </div>
        </div>
    );
};
export default Spinner;
```

- inside index.js, import Spinner

```js
//Determining Season
import React from 'react';
import ReactDOM from 'react-dom';
import SeasonDisplay from './SeasonDisplay';
import Spinner from './Spinner';

class App extends React.Component {
    state = { lat: null, errorMessage: '' };//dont need to `this.state =`

    //life cycle function
    componentDidMount() {
        window.navigator.geolocation.getCurrentPosition(
            (position) => { this.setState({ lat: position.coords.latitude }); },
            (err) => { this.setState({ errorMessage: err.message }); }
        );
    }

    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <SeasonDisplay lat={this.state.lat} />
        }

        return <Spinner />; //import Spinner
    }
}

ReactDOM.render(<App />, document.getElementById('root'));
```

![](img/2019-12-28-16-47-36.png)
---

## Specifying Default Props

- in idnex.js

- `return <div>Loading!</div>`, is hard code

- so we try to pass props from index to Spinner

- Spinner.js

```js
const Spinner = (props) => {
    return (
        // using Semantic UI
        <div className="ui active dimmer">
            <div className="ui big text loader">
                {props.message}
            </div>
        </div>
    );
};
```

- index.js

```js
    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <SeasonDisplay lat={this.state.lat} />
        }

        return <Spinner message="Please accept locaiton request" />
    }
```

![](img/2019-12-28-16-57-53.png)
---

## Specifying Default Props (Part B)

- or if index don't pass value to props, to Spinner

- index.js

```js
    render() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }
        if (!this.state.errorMessage && this.state.lat) {
            return <SeasonDisplay lat={this.state.lat} />
        }

        return <Spinner />
    }
```

- Spinner.js

```js
const Spinner = (props) => {
    return (
        // using Semantic UI
        <div className="ui active dimmer">
            <div className="ui big text loader">
                {/* {props.message} */}
                {props.message || 'Hello World!'}
            </div>
        </div>
    );
};
```

- since parent `index` didn't pass any message to child `Spinner`, so message is null means false

- but there is still ` {props.message || 'Hello World!'}`

- so it print `Hello World`

![](img/2019-12-28-17-05-33.png)

- now we also can use `Spinner.defaultProps`

- update Spinner

```js
//Specifying Default Props
import React from 'react';
const Spinner = (props) => {
    return (
        // using Semantic UI
        <div className="ui active dimmer">
            <div className="ui big text loader">
                {props.message}
                {/* {props.message || 'Hello World!'} */}
            </div>
        </div>
    );
};
Spinner.defaultProps = {
    // message: 'Loading...'
    message: 'Loading...'
};
export default Spinner;
```

![](img/2019-12-28-17-07-09.png)
---

## Avoiding Conditionals in Render

- To avoid conditionals in Render

- we create a hlper function in index.js's render() 

- to do so:

```js
//Avoiding Conditionals in Render
import React from 'react';
import ReactDOM from 'react-dom';
import SeasonDisplay from './SeasonDisplay';
import Spinner from './Spinner';

class App extends React.Component {
    state = { lat: null, errorMessage: '' };//dont need to `this.state =`

    //life cycle function
    componentDidMount() {
        window.navigator.geolocation.getCurrentPosition(
            (position) => { this.setState({ lat: position.coords.latitude }); },
            (err) => { this.setState({ errorMessage: err.message }); }
        );
    }

    //helper function
    renderContent() {
        if (this.state.errorMessage && !this.state.lat) {
            return <div>Error: {this.state.errorMessage}</div>
        }

        if (!this.state.errorMessage && this.state.lat) {
            return <SeasonDisplay lat={this.state.lat} />
        }

        return <Spinner message="Please accept locaiton request" />
        // return <Spinner />
    }

    render() {
        return (
            <div className="border red">
                {this.renderContent()}
            </div>
        );
    }
}
ReactDOM.render(<App />, document.getElementById('root'));
```

- remember: we don't have `<div className="border red">` in render()
---

## Breather and Review