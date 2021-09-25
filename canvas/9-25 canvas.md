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

首先我们开始第一个demo 画一个半径为50的圆
```JS
/** @type {HTMLCanvasElement} */

    let canvas = document.getElementById("canvas");
    let context = canvas.getContext("2d");
    let cx = canvas.width = 400;
    let cy = canvas.height = 400;

    context.beginPath(); // 起始一条路径,或重置当前路径
    context.arc(100, 100, 50, 0, Math.PI * 2, true); // 创建弧/曲线
    context.closePath(); // 创建从当前点回到起始点的路径
    context.fillStyle = 'rgb(255,255,255)'; // 设置或返回用于填充绘画的颜色 渐变或模式
    context.fill(); // 填充当前绘图(路径)
```
由以上程序我们了解到了在Canvas中绘图的大致步骤,下面我们具体分析

### 绘制弧/曲线
`arc()`方法创建弧/曲线(用于创建圆或部分圆)

`context.arc(x, y, r, sAngle, eAngle, counterclockwise)`

* x: 圆心的x坐标
* y: 圆心的y坐标
* r：圆的半径
* sAngle：起始角，以弧度计（弧的圆形的三点钟位置是 0 度）
* eAngle：结束角，以弧度计
* counterclockwise：可选。规定应该逆时针还是顺时针绘图。false 为顺时针，true 为逆时针

### 绘制直线
```JS
/** @type {HTMLCanvasElement}*/
    let canvas = document.getElementById("canvas");
    let context = canvas.getContext("2d");
    let cx = canvas.width = 400;
    let cy = canvas.height = 400;

    context.beginPath(); // 起始一条路径,或重置当前路径
    context.moveTo(50, 50); // 把路径移动到50*50的位置
    context.lineTo(100, 100); // 在100*100的位置添加一个新点
    context.strokeStyle = "#fff"; // 指定线条颜色
    context.stroke(); // 描绘线条
```
上面程序涉及到的知识点
* stroke() : 描边
  
  这个函数与fill()的区别是 fill()是填充,而stroke()只是描边
* moveTo()：把路径移动到画布中的指定点,不创建线条
* lineTo()：添加一个新点,然后在画布中创建从该点到最后指定点的线条
  
  这里也需要注意几点
  * 如果没有 moveTo，那么第一次 lineTo 的就视为 moveTo
  * 每次 lineTo 后如果没有 moveTo，那么下次 lineTo 的开始点为前一次 lineTo 的结束点。

### 绘制矩形
```JS
/** @type {HTMLCanvasElement}*/
    let canvas = document.getElementById("canvas");
    let context = canvas.getContext("2d");
    let cx = canvas.width = 400;
    let cy = canvas.height = 400;

    context.beginPath();
    context.fillStyle = '#fff';
    context.fillRect(10, 10, 100, 100);
    context.strokeStyle = '#fff';
    context.strokeRect(130, 10, 100, 100);
```
* fillRect(x,y,width,height)：绘制一个实心矩形
* strokeRect(x,y,width,height)：绘制一个空心矩形
## 颜色, 样式和阴影
常见的方法有两个上面我们已经使用了很多遍 `fillStyle()` `strokeStyle()`用来设置填充的颜色和描边的颜色
