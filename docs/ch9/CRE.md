# 5. configure React environment

### install react

```js
npx create-react-app my-app
cd my-app
npm start
```

- create a folder `react-hooks`

- we focus on react-hooks

- npx directly call node_modules's .bin/

![](img/2019-12-21-15-03-01.png)

- cd react-hooks

- run `npm start`
---



### implement an example: calculate numbers of Like 👍

- create a new folder `components` inside src

![](img/2019-12-21-15-12-55.png)  

- LikeButton.js

```js
import React, { useState } from 'react'
const LikeButton = () => {
    const [like, setLike] = useState(0);
    return (
        <button>
            {like} 👍
        </button>
    )
}
export default LikeButton;
```

- update App.js

```js
import React from 'react';
import logo from './logo.svg';
import './App.css';
import LikeButton from './components/LikeButton';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <LikeButton />
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

- import LikeButton into App.js

![](img/2019-12-21-15-49-45.png)
---

### adding a onClick event

```js
const LikeButton = () => {
    const [like, setLike] = useState(0);
    return (
        <button onClick={() => { setLike(like + 1) }}>
            {like} 👍
        </button>
    )
}
```

![](img/2019-12-21-15-55-43.png)

- the numbers of Like is 20

---

### Adding a switch buttons event

- LikeButton.js

```js
//Adding a switch buttons event
import React, { useState } from 'react'

const LikeButton = () => {
    const [like, setLike] = useState(0);
    const [on, setOn] = useState(true);
    return (
        <>
            <button onClick={() => { setLike(like + 1) }}>
                {like} 👍
            </button>
            <button onClick={() => { setOn(!on) }}>
                {on ? 'On' : 'Off'}
            </button>
        </>
    )
}

export default LikeButton;
```

![](img/2019-12-21-16-21-20.png)
---

- 总结： useState, 它可以改变函数内组件状态,并且每次组件更新的时候，都记录这个状态值

---

## Effect Hook



## useEffect, 不需要清除的effect

![](img/2020-04-11-02-35-25.png)
![](img/2020-04-11-02-35-37.png)

- update LikeButton.js

```js
//Adding a switch buttons event
import React, { useState, useEffect } from 'react'

const LikeButton = () => {
    const [like, setLike] = useState(0);
    const [on, setOn] = useState(true);
    useEffect(() => {
        document.title = `Clicked ${like} times`
    })
    return (
        <>
            <button onClick={() => { setLike(like + 1) }}>
                {like} 👍
            </button>
            <button onClick={() => { setOn(!on) }}>
                {on ? 'On' : 'Off'}
            </button>ls

        </>
    )
}

export default LikeButton;
```

![](img/2019-12-23-16-53-20.png)
---

## 需要清除的useEffect()

![](img/2020-04-11-02-40-59.png)
![](img/2020-04-11-02-41-15.png)

- create a MouseTracker.js into components foler

- create MouseTracker.js

```js
import React, { useState, useEffect } from 'react'

const MouseTracker = () => {
    const [positions, setPositions] = useState({ x: 0, y: 0 });
    useEffect(() => {
        const updateMouse = (event) => {
            console.log('inner');
            setPositions({ x: event.clientX, y: event.clientY });
        }
        console.log('add listener');
        document.addEventListener('click', updateMouse);
        return () => {
            console.log('remove listener');
            document.removeEventListener('click', updateMouse);
        }
    })
    return (
        <p>X:{positions.x}, Y:{positions.y}</p>
    )
}

export default MouseTracker;
```

- update App.js

```html
import React from 'react';
import logo from './logo.svg';
import './App.css';
import LikeButton from './components/LikeButton';
import MouseTracker from './components/MouseTracker';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <MouseTracker />
        <LikeButton />
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

![](img/2019-12-23-19-54-50.png)
