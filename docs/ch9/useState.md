# useState Hook


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