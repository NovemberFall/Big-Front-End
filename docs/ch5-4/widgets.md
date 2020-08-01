
## Create Additional Widgets

- project overview:

![](img/2020-07-31-12-02-25.png)

![](img/2020-07-31-12-03-37.png)

![](img/2020-07-31-12-03-55.png)

![](img/2020-07-31-12-04-04.png)

---

## The Search Widget Architecture(架构) 

![](img/2020-07-31-12-13-07.png)

- import `wiki API`

![](img/2020-07-31-12-13-46.png)

- first, how do we use the `Wikipedia API` ?
  - this is probably the easiest API that we're going to use in this entire course because
    it doesn't require any authentication, any API keys 

![](img/2020-07-31-12-18-19.png)

- we're going to build everything inside of one single search component

- the search component itself will have two pieces of state:
  - first, we'll have a term which is whatever user is typing into that text input, 
    we're going to send that to the `Wiki API` and do a search, that's going to 
    give us back some results. 

---

## Scaffolding(脚手架) [ˈskæfəldɪŋ]  the Widget

- create `components/Search.js`

```js
import React from 'react';

const Search = () => {
    return <h1>Search</h1>;
};

export default Search;
```

- update `App`

```js
import React from 'react';

import Search from './components/Search';

export default () => {
    return (
        <div>
            {/* <Accordion items={items} /> */}
            <Search />
        </div>
    );
};
```

![](img/2020-07-31-13-31-28.png)


---

## Text Inputs with Hooks

- update `Search.js`

```js
import React from 'react';

const Search = () => {
    return (
        <div>
            <div className="ui form">
                <div className="field">
                    <label>Enter Search Term</label>
                    <input className="input" />
                </div>
            </div>
        </div>
    );
};
export default Search;
```

![](img/2020-07-31-13-35-59.png)


---

## Text Inputs with Hooks

- update Search.js

```js
import React, { useState } from 'react';

const Search = () => {
    const [term, setTerm] = useState('');

    return (
        <div>
            <div className="ui form">
                <div className="field">
                    <label>Enter Search Term</label>
                    <input
                        value={term}
                        onChange={(e) => setTerm(e.target.value)}
                        className="input"
                    />
                </div>
            </div>
        </div>
    );
};
export default Search;
```

![](img/2020-07-31-13-45-33.png)

---

## When do we Search?

## The useEffect Hook

![](img/2020-07-31-13-52-39.png)

![](img/2020-07-31-17-55-20.png)



## Testing Exceution





