# Cesium气泡窗插件
### [在线体验](http://mapgl.com/shareCode/#/Heatmap?downUrl=)  
gitee：[https://gitee.com/caozl1132/cesiumExp-heatmap](https://gitee.com/caozl1132/cesiumExp-heatmap)  
github：[https://github.com/gitgitczl/cesiumExp-heatmap](https://github.com/gitgitczl/cesiumExp-heatmap)

***
ps：如果可以的话，希望大家能给我个star，好让我有更新下去的动力；
***
实现原理： 
核心是使用了heatmap.js这个库，这个库生成的热力图是用canvas绘制的，那么在Cesium中，我们只要将canvas转图片，当初材质贴到我们的对象上就行。其中Cesium加载热力图canvas生成的图片有两种方式，第一种是通过material来贴到entity或者geometry上，第二种是通过imageryprovider当作图层来加入，目前我这边以第一种方式来引入。

***
调用方法：
1、固定位置气泡窗：
```
new Heatmap(viewer, {
        list: list
    })
```
***
支持原heatmap.js的参数传参，具体可见src/js/heatmap.js类

其它：     
qq群：606645466（GIS之家共享交流群）

[更多案例地址](http://mapgl.com/shareCode/)&nbsp;&nbsp;&nbsp; [更多免费数据](http://mapgl.com/shareData/)&nbsp;&nbsp;&nbsp; [开发文档说明](http://mapgl.com/3dapi/)   

[其它源码下载（标绘、量算、动态材质、漫游、地图分析等）](http://mapgl.com/introduce/)
