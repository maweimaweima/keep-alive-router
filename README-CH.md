# keep-alive-router-view
扩展vue的keep-alive and router-view，可以自动判断是否需要使用缓存功能。

如果页面使用了keep-alive和router-view，好处是在下一个页面操作返回时快速恢复了上一步的操作状态，这样的体验非常好。

但是也有另外一个问题，当用户从导航菜单或面包削等入口进入页面，是需要一个全新页面的，但实际上还是使用了缓存的页面，这样的结果不是我们想要的。

keep-alive-router-view解决了这样问题，只在你操作$router.back和$router.go默认返回页面使用缓存，
$router.push默认不使用缓存。

### 安装
```npm i keep-alive-router-view```

### 使用步骤

#### 第一步 先引用模块

```
import 'keep-alive-router-view';
```

#### 第二步 使用keep-alive-router-view组件代替keep-alive和router-view

keep-alive-router-view内部封装了keep-alive和router-view，所以你只要写keep-alive-router-view组件元素。

disabled属性，用来设置禁止使用页面缓存。

```
<div id="app">
    <keep-alive-router-view :disabled="!$route.meta.keepAlive" />
</div>
```

#### 第三步 必须使用vue-router实例的方法，只有在$router.go、$router.back调用后，才默认使用缓存页面。

### keep-alive-router-view属性说明

| 属性 | 说明 | 类型 | 可选值 | 默认值 |
| --- | --- | --- | --- | --- |
| disabled | 是否禁止页面缓存 | Boolean  | true/false | true |
| name | router-view名称 | String  | - | - |
| include | 只有名称匹配的组件会被缓存 | RegExp  | - | - |
| exclude | 任何名称匹配的组件都不会被缓存 | RegExp  | - | - |
| max | 最多可以缓存多少组件实例 | Number  | - | - |


### vue-router接口扩展

#### $router.push
push接口展示的页面默认不使用缓存功能。如果需要使用，配置keepAlive为true
```javascript
this.$router.push({
  name: 'list',
  keepAlive: true
});
```
#### $router.back
back接口展示的页面默认使用缓存功能。如果禁止使用，配置keepAlive为false
```javascript
this.$router.back({
  keepAlive: false
});
```

#### $router.go
go接口展示的页面默认使用缓存功能。如果禁止使用，配置keepAlive为false
```javascript
this.$router.go(-1, {
  keepAlive: false
});
```