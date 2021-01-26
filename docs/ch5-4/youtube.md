## Rebuild the Youtube Videos App with Hooks


### Refactor the SearchBar


![](img/2021-01-25-23-15-20.png)


- Remember, Use effect is usually inside of a function component to kind of simulate the use of a lifecycle method.


- searchBar


```js
// Putting it ALL Together
import React, { useState } from 'react';

const SearchBar = ({ onFormSubmit }) => {
    const [term, setTerm] = useState('');

    const onFunctionSubmit = (event) => {
        event.preventDefault();

        //TODO: Make sure we call
        //callback from parent component
        onFormSubmit(term);
    };

    return (
        <div className="search-bar ui segment">
            <form onSubmit={onFunctionSubmit} className="ui form">
                <div className='field'>
                    <label>Video Search</label>
                    <input type="text"
                        value={term}
                        onChange={(event) => setTerm(event.target.value)}
                    />
                </div>
            </form>
        </div>
    );
};

export default SearchBar;
```


- testing, still working

-----

## Refactor App.js


















































