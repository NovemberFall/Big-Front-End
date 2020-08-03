## Building the Convert Component | Google translate API

- create `components/Convert.js`

```js
import React, { useState, useEffect } from 'react';

const Convert = ({ language, text }) => {
    useEffect(() => {
        console.log('New language or text');
    }, [language, text]);

    return <div />;
};

export default Convert;
```

- update `Translate.js`

```js
//AIzaSyCHUCmpR7cT_yDFHC98CZJy2LTms-IwDlM
import React, { useState } from 'react';
import Dropdown from './Dropdown';
import Convert from './Convert';

const options = [
    {
        label: 'Chinese',
        value: 'zh'
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
    },
    {
        label: 'Dutch',
        value: 'nl'
    }
];

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
            <hr />
            <h3 className="ui header">Output</h3>
            <Convert text={text} language={language} />
        </div>
    );
}

export default Translate;
```

![](img/2020-08-02-17-15-22.png)

---

## Using the Google Translate API

- install `axios`

- `npm install axios`

- use `post` method
  - `axios.post('https://translation.googleapis.com/language/translate/v2') ` 
  - this line here is pretty much not going to change in any number of years at all.


![](img/2020-08-02-18-32-22.png)

- recall: 具体各国语言的代表，可以参考 `language support`

![](img/2020-08-02-20-27-42.png)


- update `convert.js`

```js
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const Convert = ({ language, text }) => {
    useEffect(() => {
        // console.log('New language or text');
        axios.post('https://translation.googleapis.com/language/translate/v2',
            {},
            {
                params: {
                    q: text,
                    target: language.value,
                    key: 'XXXXXXXXXXXXXXXXXXXXXX'
                }
            }
        );
    }, [language, text]);

    return <div />;
};
export default Convert;
```

![](img/2020-08-02-20-31-00.png)






