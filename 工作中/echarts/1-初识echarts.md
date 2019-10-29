​	用这个做图形开发效率特别高了，比如需要柱形图，圆饼图什么的，不需要自己用canvas去绘制了，直接引入他的官方库来使用它的这个东西就可以了。

	## 引入方式

```js
1.从官网下载界面选择你需要的版本下载，根据开发者功能和体积上的需求，我们提供了不同打包的下载，如果你在体积上没有要求，可以直接下载完整版本。开发环境建议下载源代码版本，包含了常见的错误提示和警告。

2.在 ECharts 的 GitHub 上下载最新的 release 版本，解压出来的文件夹里的 dist 目录里可以找到最新版本的 echarts 库。

3.通过 npm 获取 echarts，npm install echarts --save，详见“在 webpack 中使用 echarts”

4.cdn 引入，你可以在 cdnjs，npmcdn 或者国内的 bootcdn 上找到 ECharts 的最新版本。
```

## 自定义构建Echarts



## 在webpack中使用Echarts

1.通过这个`npm install echarts --save`安装Echarts

```js
var echarts = require('echarts');

// 基于准备好的dom，初始化echarts实例
var myChart = echarts.init(document.getElementById('main'));
// 绘制图表
let option = {}
myChart.setOption(option);
```

2.按需引入Echarts图标和组件

```js
// 引入 ECharts 主模块
var echarts = require('echarts/lib/echarts');
// 引入柱状图
require('echarts/lib/chart/bar');
// 引入提示框和标题组件
require('echarts/lib/component/tooltip');
require('echarts/lib/component/title');

// 基于准备好的dom，初始化echarts实例
var myChart = echarts.init(document.getElementById('main'));
// 绘制图表
myChart.setOption(option);
```

**注意** 可以按需引入的模块列表见 <https://github.com/ecomfe/echarts/blob/master/index.js> 



## 异步数据加载和更新

1. 可以把这些东西放到异步回调函数中初始化

```js
var myChart = echarts.init(document.getElementById('main'));

$.get('data.json').done(function (data) {
     myChart.setOption(options)
});
```

2. 先设置完其他的样式，显示一个空的直角坐标轴，然后获取数据后填入数据。

```js
var myChart = echarts.init(document.getElementById('main'));
// 显示标题，图例和空的坐标轴
myChart.setOption({
    title: {
        text: '异步数据加载示例'
    },
    tooltip: {},
    legend: {
        data:['销量']
    },
    xAxis: {
        data: []
    },
    yAxis: {},
    series: [{
        name: '销量',
        type: 'bar',
        data: []
    }]
});

// 异步加载数据
$.get('data.json').done(function (data) {
    // 填入数据
    myChart.setOption({
        xAxis: {
            data: data.categories
        },
        series: [{
            // 根据名字对应到相应的系列
            name: '销量',
            data: data.data
        }]
    });
});
```



## loading动画

如果数据加载时间较长，一个空的坐标轴放在画布上也会让用户觉得是不是产生 bug 了，因此需要一个 loading 的动画来提示用户数据正在加载。 

```js
myChart.showLoading();
$.get('data.json').done(function (data) {
    myChart.hideLoading();
    myChart.setOption(...);
});
```



## 数据的动态更新

ECharts 由数据驱动，数据的改变驱动图表展现的改变，因此动态数据的实现也变得异常简单。

所有数据的更新都通过 [setOption](http://echarts.baidu.com/tutorial.html#api.html#echartsInstance.setOption)实现，你只需要定时获取数据，[setOption](http://echarts.baidu.com/tutorial.html#api.html#echartsInstance.setOption) 填入数据，而不用考虑数据到底产生了那些变化，ECharts 会找到两组数据之间的差异然后通过合适的动画去表现数据的变化。 



## 使用dataset管理数据

















