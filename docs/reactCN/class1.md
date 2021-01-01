## 类式组件

![](img/2020-12-31-22-42-27.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>1_函数式编程</title>
</head>
<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>

    <!-- import core lirbary -->
    <script type="text/javascript" src="../js/react.development.js"></script>

    <!-- import react-dom, is used to support react to operation on DOM -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>

    <!-- import babel, jsx => js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>

    <!-- type="text/babel" 表示现在这里写的是jsx, 不再是js -->
    <script type="text/babel">
        //1. create class式组件
        class MyComponent extends React.Component{//React.Component 是react内置的
            render(){
                return <h2>我是用class定义的组件(适用于[复杂组件]的定义)</h2>
            }
        }

        //2. render 组件到页面
        // ReactDOM.render(类组件, Container)
        ReactDOM.render(<MyComponent/>, document.getElementById('test'))
    </script>
    
</body>
</html>
```


![](img/2020-12-31-22-49-13.png)


































