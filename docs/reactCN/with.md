## withRouter

- 一般组件是没有 router组件 里的 `history`, 那如何给一般组件也用上 API ?
  - `withRouter` : 第一个字母是小写，则代表**它是函数**，如果第一个字母大写,则是组件。
  - `export default withRouter(Component)`
  - `withRouter` 可以接收一个 一般组件, 然后给一般组件加上，路由组件(Router)身上所特有的三个`API`:
    - 1.`history`, 2.`location`, 3.`match` 
  - `withRouter` 的**返回值**是一个`新组件`
