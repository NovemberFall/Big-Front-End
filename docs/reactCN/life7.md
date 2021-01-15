## getSnapshotBeforeUpdate News滚动的案例

- 尽管官方文档已经说了 非常少用 `getSnapshotBeforeUpdate`, 但我们还是要解释一下它的用法！

![](img/2021-01-14-23-05-47.png)

- 来写一个类似微信朋友圈列表的新闻

---

### 首先来复习一下，新闻网页结构

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .list{
            width: 200px;
            height: 150px;
            background-color: skyblue;
        }
        .news{
            height:30px;
        }
    </style>
</head>
<body>
    <div class="list">
        <div class="news">新闻7</div>
        <div class="news">新闻6</div>
        <div class="news">新闻5</div>
        <div class="news">新闻4</div>
        <div class="news">新闻3</div>
        <div class="news">新闻2</div>
        <div class="news">新闻1</div>
    </div>
</body>
</html>
```

- 首先每条新闻是 30px, 总共150px height, 所以会有两条溢出

- 添加滚动条 `overflow:auto`


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <style>
        .list{
            width: 200px;
            height: 150px;
            background-color: skyblue;
            overflow: auto;
        }
        .news{
            height:30px;
        }
    
    </style>
</head>
<body>
    <div class="list">
        <div class="news">新闻7</div>
        <div class="news">新闻6</div>
        <div class="news">新闻5</div>
        <div class="news">新闻4</div>
        <div class="news">新闻3</div>
        <div class="news">新闻2</div>
        <div class="news">新闻1</div>
    </div>
</body>
</html>
```


![](img/2021-01-15-01-37-44.png)

![](img/2021-01-15-01-38-53.png)

- 我们不想用滚动条实现，想用js代码实现:


![](img/2021-01-15-01-41-06.png)


---

### 现在回到组件，来看react 的实现

![](img/2021-01-15-10-57-22.png)


```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>4_getSnapShotBeforeUpdate的使用场景</title>
	<style>
		.list{
			width: 200px;
			height: 150px;
			background-color: skyblue;
			overflow: auto;
		}
		.news{
			height: 30px;
		}
	</style>
</head>
<body>
	<!-- 准备好一个“容器” -->
	<div id="test"></div>
	
	<!-- 引入react核心库 -->
	<script type="text/javascript" src="../js/17.0.1/react.development.js"></script>
	<!-- 引入react-dom，用于支持react操作DOM -->
	<script type="text/javascript" src="../js/17.0.1/react-dom.development.js"></script>
	<!-- 引入babel，用于将jsx转为js -->
	<script type="text/javascript" src="../js/17.0.1/babel.min.js"></script>

	<script type="text/babel">
		class NewsList extends React.Component{

			state = {newsArr:[]}

			componentDidMount(){
				setInterval(() => {
					//获取原状态
					const {newsArr} = this.state
					//模拟一条新闻
					const news = '新闻'+ (newsArr.length+1)
					//更新状态
					this.setState({newsArr:[news,...newsArr]})
				}, 1000);
			}

			getSnapshotBeforeUpdate(){
				return this.refs.list.scrollHeight
			}

			componentDidUpdate(preProps,preState,height){
				this.refs.list.scrollTop += this.refs.list.scrollHeight - height
			}

			render(){
				return(
					<div className="list" ref="list">
						{
							this.state.newsArr.map((n,index)=>{
								return <div key={index} className="news">{n}</div>
							})
						}
					</div>
				)
			}
		}
		ReactDOM.render(<NewsList/>,document.getElementById('test'))
	</script>
</body>
</html>
```

- `this.refs.list.scrollTop += this.refs.list.scrollHeight - height`, 这里用 +=, 是因为持续有新闻出来，所以持续往上顶































