# gallery-by-react

使用新版本 webpack(v1.12.0) 和 react(v15.0.0) 制作的 gallery-by-react

---

## 课程

一开始是跟着 Materliu 在慕课网上的视频制作，发现 webpack 和 react 都已经和视频里的版本不同了，用法当然和视频里也不同了。

视频地址：

- [React实战--打造画廊应用（上）](http://www.imooc.com/learn/507)
- [React实践图片画廊应用（下）](http://www.imooc.com/learn/652)

## 参考项目

在 github 上搜索到 wangyongzhi 写的 [gallery-by-react](https://github.com/wangyongzhi/gallery-by-react)，是在2016年10月份制作完成的，
也有些部分和现在不同，不过参考了他的代码，我终于坚持做完了这个 gallery-by-react。

和 wangyongzhi 不同，我没有使用 sass 和 postcss。因为要安装 sass-loader 时，发现必须使用 2.0.0 以上版本的 webpack，
但是在安装了 2.2.1 版本的 webpack后，又有其他安装的包报错，提示需要 1.14.0 版本以下的 webpack，所以最后我直接使用原生 css。
没有使用 postcss，是因为总是有我看不懂的报错，我只能放弃使用 postcss 了。

另外和 wangyongzhi 不同的是，我使用了一些 ES6 语法。

在 react 中使用 ES6 有一些需要注意的问题：

- [初始化 state](https://facebook.github.io/react/docs/react-without-es6.html#setting-the-initial-state)：

```js
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  // ...
}
// 而不是使用 getInitialState 函数。
```

- [使用 handleClick](https://facebook.github.io/react/docs/react-without-es6.html#autobinding)：

```js
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Hello!'};
    // This line is important!
    this.handleClick = this.handleClick.bind(this); // 需要给 handleClick 函数绑定 this
  }

  handleClick() {
    alert(this.state.message);
  }

  render() {
    // Because `this.handleClick` is bound, we can use it as an event handler.
    return (
      <button onClick={this.handleClick}>
        Say hello
      </button>
    );
  }
}
```

## 发布

最后运行`npm run dist`生成 dist 版本之前，需要修改一些配置文件：

1. 修改 cfg/defaults.js 文件中的发布路径，即`publicPath`属性，由`'/assets/'`改为`'assets/'`
2. 修改 cfg/base.js 文件中`devServer.publicPath`属性值，改为`'/' + defaultSettings.publicPath`
3. 修改 src/index.html 文件中加载的 js 脚本路径，`src`的值改为`"assets/app.js"`

这样修改之后，再运行`npm run dist`命令，就可以达到课程视频最后的效果。
