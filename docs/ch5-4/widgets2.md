## Dropdown (可折叠的) Architecture | widgets

![](img/2020-08-01-17-09-10.png)

![](img/2020-08-01-17-13-28.png)

---

## Scaffolding(脚手架) the Dropdown

- create `components/Dropdown.js`

```js
import React from 'react';

const Dropdown = () => {
    return <h1>Dropdown</h1>;
};

export default Dropdown;
```

- update `App.js`

```js
import React from 'react';
import Accordion from './components/Accordion';
import Search from './components/Search';
import Dropdown from './components/Dropdown';

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

const options = [
    {
        label: 'The Color Red',
        value: 'red'
    },
    {
        label: 'The Color Green',
        value: 'green'
    },
    {
        label: 'The Color Blue',
        value: 'blue'
    }
];

export default () => {
    return (
        <div>
            {/* <Accordion items={items} /> */}
            {/* <Search /> */}
            <Dropdown options={options} />
        </div>
    );
};
```

---

## A lot of JSX

- update `Dropdown.js`

```js
import React from 'react';

const Dropdown = ({ options }) => {
    const renderedOptions = options.map((option) => {
        return (
            <div key={option.value} className="item">
                {option.label}
            </div>
        );
    });
    return (
        <div className="ui form">
            <div className="field">
                <label className="label">Select a Color</label>
                <div className="ui selection dropdown visible active">
                    <i className="dropdown icon"></i>
                    <div className="text">Select Color</div>
                    <div className="menu visible transition">
                        {renderedOptions}
                    </div>
                </div>
            </div>
        </div>
    );
};

export default Dropdown;
```

![](img/2020-08-01-17-34-17.png)

---

## Selection State | Filtering the Option List

- update `App.js`

```js
import React, { useState } from 'react';
import Accordion from './components/Accordion';
import Search from './components/Search';
import Dropdown from './components/Dropdown';

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

const options = [
    {
        label: 'The Color Red',
        value: 'red'
    },
    {
        label: 'The Color Green',
        value: 'green'
    },
    {
        label: 'The Color Blue',
        value: 'blue'
    }
];

export default () => {
    const [selected, setSelected] = useState(options[0]);
    return (
        <div>
            {/* <Accordion items={items} /> */}
            {/* <Search /> */}
            <Dropdown
                selected={selected}
                onSelectedChange={setSelected}
                options={options}
            />
        </div>
    );
};
```

- update `Dropdown.js`

```js
import React from 'react';

const Dropdown = ({ options, selected, onSelectedChange }) => {
    if (options.value === selected.value) {
        return null;
    }

    const renderedOptions = options.map((option) => {
        return (
            <div
                key={option.value}
                className="item"
                onClick={() => { onSelectedChange(option) }}
            >
                {option.label}
            </div>
        );
    });
    return (
        <div className="ui form">
            <div className="field">
                <label className="label">Select a Color</label>
                <div className="ui selection dropdown visible active">
                    <i className="dropdown icon"></i>
                    <div className="text">{selected.label}</div>
                    <div className="menu visible transition">
                        {renderedOptions}
                    </div>
                </div>
            </div>
        </div>
    );
};
export default Dropdown;
```

![](img/2020-08-01-22-17-47.png)

---

## Hiding and Showing the Option List

- 我们可以通过 `Hook` system, useState 给 当前组件添加 boolean 值， 默认为 `false`
  如果，点击则为 `true`

- update `Dropdown.js`

```js
import React from 'react';

const Dropdown = ({ options, selected, onSelectedChange }) => {
    const [open, setOpen] = useState(false);

    if (options.value === selected.value) {
        return null;
    }

    const renderedOptions = options.map((option) => {
        return (
            <div
                key={option.value}
                className="item"
                onClick={() => { onSelectedChange(option) }}
            >
                {option.label}
            </div>
        );
    });
    return (
        <div className="ui form">
            <div className="field">
                <label className="label">Select a Color</label>
                <div
                    onClick={() => { setOpen(!open) }}
                    className={`ui selection dropdown ${open ? 'visible active' : ''}`}
                >
                    <i className="dropdown icon"></i>
                    <div className="text">{selected.label}</div>
                    <div className={`menu ${open ? 'visible transition' : ''}`}>
                        {renderedOptions}
                    </div>
                </div>
            </div>
        </div>
    );
};
export default Dropdown;
```

![](img/2020-08-02-01-18-32.png)

- now it works!

---



























