# Fabric.js简介第5部分
在前面的系列文章中，我们已经介绍了很多主题；从基本的对象操作到动画、事件、过滤器、组和子类。但还有一些非常有趣和有用的东西需要讨论！

## 缩放和平移

让我们看看如何通过鼠标交互实现缩放和平移的基本系统。我们将使用鼠标滚轮在画布上缩放至 20 倍（2000%），并使用 Alt + 单击操作进行拖动。
我们开始连接基本控件：

```javascript
canvas.on('mouse:wheel', function(opt) {
  var delta = opt.e.deltaY;
  var zoom = canvas.getZoom();
  zoom *= 0.999 ** delta;
  if (zoom > 20) zoom = 20;
  if (zoom < 0.01) zoom = 0.01;
  canvas.setZoom(zoom);
  opt.e.preventDefault();
  opt.e.stopPropagation();
})

```
效果图

![Alt text](image-51.png)

实例
[放大缩小](./demo1.html)



























[下一节](./part5.md)