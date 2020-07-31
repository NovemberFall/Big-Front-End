## Understanding useState

![](img/2020-07-31-10-50-44.png)

- javascript `destructure`

![](img/2020-07-31-10-55-43.png)


```js
const Accordion = ({ items }) => {
    // const things = useState(null);
    // const activeIndex = things[0];
    // const setActiveIndex = things[1];

    const [activeIndex, setActiveIndex] = useState(null);

    const onTitleClick = (index) => {
        setActiveIndex(index);
    };
```

---

```js
    const things = useState(null);
    const activeIndex = things[0];
    const setActiveIndex = things[1];


    //以上这三句，是等价于 
    const [activeIndex, setActiveIndex] = useState(null);
```

![](img/2020-07-31-11-01-48.png)


- example 1:
  
![](img/2020-07-31-11-02-17.png)


- example 2:

![](img/2020-07-31-11-02-42.png)


- `Class Components` VS `Function Components`

![](img/2020-07-31-11-03-45.png)


- example:

![](img/2020-07-31-11-06-12.png)


---

## Setter Function

- `const [activeIndex, setActiveIndex] = useState(null);`
  - Anytime we call `useState(null)`, we get back that array, 
  - And the second argument inside of it is always going to be `setter`


