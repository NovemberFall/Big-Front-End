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
































