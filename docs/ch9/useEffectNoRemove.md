# useEffect don't need to remove

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