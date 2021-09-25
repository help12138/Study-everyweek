# Canvas 定义
canvas是 HTML5 新增的元素，可用于通过使用 JavaScript 中的脚本来绘制图形。例如，它可以用于绘制图形、制作照片、创建动画，甚至可以进行实时视频处理或渲染。

注意： canvas只是一个画布,本省并不具有绘图的能力, 绘图必须用JS等脚本语言

我们可以认为 canvas标签只是一个矩形的画布,JS就是画笔,负责在画布上画画

一句话总结就是： Canvas是为了解决Web页面中只能显示静态图片这个问题而提出的,一个可以使用JS等脚本语言向其中绘制图像的HTML标签

## Canvas的使用
创建画布
```JS
<body>
  <canvas id="canvas"></canvas>

  <!--脚本-->
  <script>
  // 注意 下面这个注释行在VSCode中可以让Canvas代码实现自动补全
    /** @type {HTMLCanvasElement} */
  </script>

  <!--样式-->
  <style>
    #canvas{
      background: #000;
    }
  </style>
</body>
```
上面代码会因为没有写出宽高的值,所以会创建一个默认的300 * 150 大小的画布