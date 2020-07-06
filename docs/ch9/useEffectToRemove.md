# useEffect need to remove

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
