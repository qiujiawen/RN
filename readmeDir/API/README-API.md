# React Native API 学习

## React Native背景

#### React

1、React 是由Facebook推出的一个JavaScript框架，主要用于前段开发。

2、React 采用组件化方式简化Web开发

    a、DOM:每个HTML界面可以看做一个DOM

    b、原生的web开发方式，HTML一个文件，javaScript一个文件，文件分开，就会导致修改起来比较麻烦。

    c、可以把一组相关的HTML标签和JavaScript单独封装到一个组件类中，便于复用，方便开发。


3、React 可以高效的绘制界面

    a、原生的Web,刷新界面(DOM)，需要把整个界面刷新.

    b、React只会刷新部分界面，不会整个界面刷新。

    c、因为React独创了Virtual DOM机制。Virtual DOM是一个存在于内存中的JavaScript对象，它与DOM是一一对应的关系，当界面发送变化时，React会利用DOM Diff算法，把有变化的DOM进行刷新。


4、React是采用JSX语法，一种JS语法糖，方便快速开发。


#### 常见的五种App开发模式

常见的开发模式有5种：Native App,Web App,Hybrid App,Weex,React Native

##### Native App

Native App:指使用原生API开发App,比如iOS用OC语言开发

优点：性能高

缺点：开发维护成本高，养一个原生开发工程师需要很多钱，最重要iOS版本更新也成问题

##### Web App

Web App:指使用Html开发的移动端网页App,类似微信小程序，整个App都是网页。

优点：用户不需要安装，不会占用手机内存

缺点：用户体验不好，不能离线，必须联网

##### Hybrid APP

Hybrid App:混合开发模式，原生Api+Html共同开发，比如iOS,用html写好界面，用UIWebView展示。

优点:界面复用性强，一个界面，iOS和安卓都可以使用

缺点:相对于原生，性能相对有所损害

##### Weex

Weex:基于Vue(JS框架)的语法开发的App,底层会自动把JS代码解析成对应平台(iOS,安卓)的原生API，本质还是原生API开发，只不过表面是用Vue开发。

优点:可以做到一套代码，跨平台执行，底层会自动判断当前是哪个平台，转换为对应平台的原生API代码。

缺点：开源较晚，互联网上相关资料还比较少，社区规模较小

##### React Native

React Native:基于React开发的App

优点：

*    跨平台开发

*    跳过App Store审核，远程更新代码，提高迭代频率和效率，既有Native的体验，又保留React的开发效率。

缺点:对于不熟悉前端开发的人员上手比较慢，不能真正意义上做到跨平台，使用后，对app体积增加。

## React Native原理

React Native原理其实跟Weex差不多，底层也会把React转换为原生API

React Native和Weex区别在于跨平台上面，Weex只要写一套代码，React Native需要iOS,安卓都写，说明React Native底层解析原生API是分开实现的，iOS一套，安卓一套。

## React Native 如何把 React 转化为原生API

React Native会在一开始生成OC模块表，然后把这个模块表传入JS中，JS参照模块表，就能间接调用OC的代码。

相当于买了一个电器（OC），对应一份说明书（模块表），程序员用 JS 参照说明书去操作电器。

## JS 和 OC 交互

