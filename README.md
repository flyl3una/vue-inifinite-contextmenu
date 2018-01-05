# vue-inifinite-contextmenu

> Vue2 无限级右键菜单组件，菜单内容，图标，点击事件可自定义

截图如下
![](https://github.com/flyl3una/vue-inifinite-contextmenu/raw/master/src/assets/1.png)

## 开发安装

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

## 使用

**props**

| 参数     | 说明           | 类型     | 可选值        | 默认值   |
| ------ | ------------ | ------ | ---------- | ----- |
| list   | 右键菜单显示内容数据列表 | 数组     | -          | []    |
| show   | 子菜单是否显示      | bool   | true,false | false |
| startX | 子菜单显示的X轴位置   | String | -          | '0'   |
| startY | 子菜单显示的X轴位置   | String | -          | '0'   |

**events**

| 参数              | 说明                                     | 参数            |
| --------------- | -------------------------------------- | ------------- |
| openContextMenu | 右键点击事件,param可以包含点击右键的dom属性             | $event, param |
| clickEvent      | 右键菜单点击某一个选项触发的事件，可以在此获取点击选项的clickIndex。对点击选项进行逻辑处理 |               |

**list数据说明**

- list为一个数组，每一个元素包含一个选项的属性。
- clickIndex为每一个选项的点击索引，必须保证索引唯一性。
- headIcon为选项开头的图标类名。
- tailIcon为选项结尾的图标类型。
- label为选项显示文字内容。
- divide如果为true，则在该选项的下方显示一个水平分割线。
- childrens中的内容为该选项的子菜单。

**框架**

- vue2.5
- vue-router3.0.1

## 模板

```vue
<infinite-right-menu 
    :list="lists" 
    :startX="this.rightMenuX+'px'"
    :startY="this.rightMenuY+'px'"
    :show="this.show" 
    @refreshbizlines="clickEvent">
</infinite-right-menu>
```

## License

[MIT license](https://github.com/mauricius/vue-draggable-resizable/blob/master/LICENSE)