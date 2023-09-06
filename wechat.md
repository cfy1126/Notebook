# 1. 初次上手
## 1.1 小程序是什么？
- 小程序可以视为只能用微信打开和浏览的网站
- 小程序页面本质上就是网页

## 1.2 知识准备
- JavaScript 语言：简单的 JS 脚本程序
- css 样式：使用 css 控制网页元素外观
- HTML 标签：网页布局

## 1.3 开发准备
1. 注册[微信公众平台](https://mp.weixin.qq.com/)，申请一个AppID
2. 下载[小程序开发工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)

## 1.4 小程序的项目结构
>顶层的 app 脚本
>页面的 page 脚本
- app.json
- app.js
- app.wxss
- pages
    - home
        - home.wxml
        - home.js

1. ***app.json***: 整个项目的配置文件，常用属性`pages`、`window`、`tarbar`
- ![示例](https://www.wangbase.com/blogimg/asset/202010/bg2020100110.jpg)
- ![示例](https://www.wangbase.com/blogimg/asset/202010/bg2020100111.jpg)
2. ***app.js***: 整个小程序初始化脚本，新建小程序实例对象，设置项目全局变量
3. ***app.wxss***: 全局样式，对所有页面生效
3. ***pages/home***: 小程序页面目录

---

# 2. 页面样式
## 2.1 WeUI
> [效果展示](https://weui.io/)

![WeUI](https://www.wangbase.com/blogimg/asset/202010/bg2020100305.jpg)
![Button](https://www.wangbase.com/blogimg/asset/202010/bg2020100306.jpg)

## 2.2 常用标签
1. `<viw>`: 表示区块，类似 HTML 的`<div>`标签
2. `<text>`: 表示一段行内文本，类似 HTML 的`<span>`标签
3. `<image>`: 展示图片，类似 HTML 的`<img>`标签
4. `<navigator>`: 页面跳转，类似 HTML 的`<a>`标签

# 3. 脚本编程
## 3.1 数据绑定
- 脚本里面的某些数据，会自动成为页面可以读取的全局变量，两者会同步变动
- 页面数据通过脚本传入，通过脚本改变页面，实现动态加载页面

## 3.2 事件
- 事件类型
- 绑定对象
- 事件处理函数

# 4. API 使用
## 4.1 客户端数据储存
1. 小程序允许将一部分数据保存在客户端（即微信 App）的本地储存里面（其实就是自定义的缓存）。下次需要用到这些数据的时候，就直接从本地读取，这样就大大加快了渲染。本节介绍怎么使用客户端数据储存。

## 4.2 远程数据请求
1. `url`和`success()`为必填属性
```js
wx.request({
    url: 'http://localhost:3000/items',
    success(res) {
    that.setData({ items: res.data });
    }
});
```

## 4.5 获取用户个人数据
- 头像、昵称、地区等等
```html
<view>
  <text class="title">hello {{name}}</text>
  <button open-type="getUserInfo" bind:getuserinfo="buttonHandler">
    授权获取用户个人信息
  </button>
</view>
```
```js
Page({
  data: { name: '' },
  buttonHandler(event) {
    if (!event.detail.userInfo) return;
    this.setData({
      name: event.detail.userInfo.nickName
    });
  }
});
```


## 4.6 多页面的跳转
- 组件方式
```html
<view>
  <text class="title">这是第二页</text>
  <navigator url="../home/home">前往首页</navigator>
</view>
```
- 脚本方式
```js
wx.navigateTo({
    url: '../second/second'
});
```


