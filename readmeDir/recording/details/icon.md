# React-Native 图标

<a href='https://github.com/oblador/react-native-vector-icons'>官方链接</a>

## 安装
```
react-native link react-native-vector-icons
//或者使用yarn安装
npm install -g yarn
yarn add react-native-vector-icons
```

## 自动配置
````
// iOS和安卓关联该库
react-native link
````

## 使用方法
1、先引用
````
import Icon from 'react-native-vector-icons/FontAwesome';
````

2、再使用
````
// size:代表矢量图的大小；name:代表Ionicons库中图标的名字；color:代表矢量图样式
<Icon
    name='search'
    size={18}
    color='#000'
/>
````

官方查找所有矢量图的<a href='https://oblador.github.io/react-native-vector-icons/'>链接</a>
