## Hooks System

![](img/2020-07-30-22-58-35.png)

- it is just helping you write reusable code.

![](img/2020-07-30-23-00-30.png)

- `npx create-react-app widgets`

- delete all files from `src`


- create `App.js`

```js
import React from 'react';

export default () => {
    return <h1>Widgets App</h1>;
};
```


- create `index.js`

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.querySelector('#root'));
```

![](img/2020-07-30-23-28-26.png)

---

## Communicating the items Prop


- create `components/Accordion.js`

```js
import React from 'react';

const Accordion = () => {
    return <h1>Accordion</h1>;
};

export default Accordion;
```

- update App.js

```js
import React from 'react';
import Accordion from './components/Accordion';

export default () => {
    return (
        <div>
            <Accordion />
        </div>
    );
};
```

![](img/2020-07-30-23-47-26.png)

- update App.js

```js
import React from 'react';
import Accordion from './components/Accordion';

const items = [
    {
        title: 'What is React?',
        content: 'React is a front end javascript framework',
    },
    {
        title: 'Why use React?',
        content: 'React is a favorite JS library among engineers',
    },
    {
        title: 'How do you use React?',
        content: 'You use React by creating components',
    }
];

export default () => {
    return (
        <div>
            <Accordion items={items} />
        </div>
    );
};
```

- update `Accordion.js`

```js
import React from 'react';

const Accordion = ({ items }) => {
    return <h1>{items.length}</h1>;
};

export default Accordion;
```

![](img/2020-07-31-00-09-37.png)

---

## Building and Styling the Accordion

- update Accordion.js

```js
import React from 'react';

const Accordion = ({ items }) => {
    const renderedItems = items.map(item => {
        return (
            <div key={item.title}>
                <div className="title active">
                    <i className="dropdown icon"></i>
                    {item.title}
                </div>

                <div className="content active">
                    <p>{item.content}</p>
                </div>
            </div>
        );
    });
    return <div className="ui styled accordion">{renderedItems}</div>;
};

export default Accordion;
```

![](img/2020-07-31-00-21-53.png)

- import `semantic` css for `public/index.html`

```html
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css"
    />    
```

![](img/2020-07-31-00-33-19.png)


- update `Accordion.js`

```js
import React from 'react';
const Accordion = ({ items }) => {
    const renderedItems = items.map(item => {
        return (
            <React.Fragment key={item.title}>
                <div className="title active">
                    <i className="dropdown icon"></i>
                    {item.title}
                </div>

                <div className="content active">
                    <p>{item.content}</p>
                </div>
            </React.Fragment>
        );
    });
    return <div className="ui styled accordion">{renderedItems}</div>;
};
export default Accordion;
```

![](img/2020-07-31-00-43-04.png)


---

## Helper Functions in Function Components

- update `Accordion.js`

```js
import React from 'react';

const Accordion = ({ items }) => {
    const renderedItems = items.map((item, index) => {
        return (
            <React.Fragment key={item.title}>
                <div className="title active"
                    onClick={() => { console.log("Title clicked", index) }}
                >
                    <i className="dropdown icon"></i>
                    {item.title}
                </div>

                <div className="content active">
                    <p>{item.content}</p>
                </div>
            </React.Fragment>
        );
    });

    return <div className="ui styled accordion">{renderedItems}</div>;
};

export default Accordion;
```




![](img/2020-07-31-00-49-19.png)





