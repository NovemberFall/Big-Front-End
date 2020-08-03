## The Tranlate Widget

![](img/2020-08-02-15-53-41.png)

![](img/2020-08-02-15-54-44.png)


## Scaffolding the Translate Component

- create `components/Translate.js`

```js
import React, { useState } from 'react';
import Dropdown from './Dropdown';

const options = [
    {
        label: 'Chinese',
        value: 'ch'
    },
    {
        label: 'Afrikaans',
        value: 'af'
    },
    {
        label: 'Arabic',
        value: 'ar'
    },
    {
        label: 'Hindi',
        value: 'hi'
    }
];

const Translate = () => {
    const [language, setLanguage] = useState(options[0]);

    return (
        <div>
            <Dropdown
                label="Select a Language"
                selected={language}
                onSelectedChange={setLanguage}
                options={options}
            />
        </div>
    );
}

export default Translate;
```

## Adding the Language Input

- update `Translate.js`

```js
const Translate = () => {
    const [language, setLanguage] = useState(options[0]);
    const [text, setText] = useState('');

    return (
        <div>
            <div className="ui form">
                <div className="field">
                    <label>Enter Text</label>
                    <input value={text} onChange={(e) => { setText(e.target.value) }} />
                </div>
            </div>

            <Dropdown
                label="Select a Language"
                selected={language}
                onSelectedChange={setLanguage}
                options={options}
            />
        </div>
    );
}

export default Translate;
```

![](img/2020-08-02-16-28-03.png)

---

## Understanding the Convert Component

- reacall:

![](img/2020-08-02-16-28-56.png)

![](img/2020-08-02-16-29-40.png)

#### How to use Google Translate API

![](img/2020-08-02-16-32-48.png)

- but this  is `paid API`, it only work on `localhost:3000`
  - that means, we must run on `localhost:3000`, otherwise it doesn't work


- input `cloud.google.com/translate/docs`

![](img/2020-08-02-16-47-42.png)

- click `APIs and reference` -> `REST reference` -> `Basic` -> `translate`

![](img/2020-08-02-16-49-24.png)

---


## Google Translate API key

- 具体看我的印象笔记

















