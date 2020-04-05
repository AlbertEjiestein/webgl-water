# WebGL Water Demo

## 项目说明:

Demo基于Evan Wallace项目，地址：http://madebyevan.com/webgl-water/
浏览器要求：Chrome 13.0+, Firefox 5.0+, Safari 5.1+
Demo信息：
这个Demo需要一个相当好的显卡和最新的显卡驱动。

该Demo结合了基于高度的水面渲染、反射与折射(reflections & refractions)、基于统计的漫反射遮挡(Analytic AO)及平滑的实时软阴影生成技术、向我们呈现了一个非常逼真的局部水体环境的渲染解决方案。这个Demo的亮点在于将多项常用图形渲染技巧精彩完美得结合在一起，并使用WebGL技术在网页前端展示出来，同时也验证了基于浏览器前端硬件加速能力的WebGL应用，已经可以达到非常高质量的实时环境渲染水平了。

## 操作说明：

  + 拖拽水体来生成水纹涟漪
  + 拖动背景来转换相机视角
  + 按空格键来暂停/开始
  + 拖拽圆球移动它
  + 按L键设置光线方向
  + 按G键来设置重力
  + 鼠标滚轮控制缩放

## 使用到的技术：

  + 光线追踪的反射和折射
  + 基于统计的漫反射遮挡
  + 基于高度的水体模拟（需要OES_texture_float扩展）
  + 软阴影
  + 焦散效果（需要OES_texture_standard_derivatives扩展，目前只有Google Chrome浏览器支持这一扩展）

## 文件说明:

+ main.js
  + 文件的入口，包括事件监听，动画渲染

+ renderer.js负责渲染，
  + 包括光线的更新，updateCaustics，水、立方体、球的渲染


+ lightgl.js负责生成webgl上下文以及基于webgl的各种类:
  + create:生成webgl上下文;
  + keys:一个字典，键盘码到布尔型映射，代表当前按键是否按下;
  + 导出外部类:
    + Matrix,定义了webgl中常用的矩阵运算方法；
    + Indexer：为对象集合中的对象添加唯一索引，用来生成网格；
    + Buffer:用来上传数据到GPU，buffer分为顶点缓冲区和索引缓冲区；
    + Mesh：网格用来展现一个vertex buffer和index buffer的集合，每一个vertex buffer有一个网格实例中的
    + 数据数组名，还有一个在vertex shader中的GLSL名，同样，有两个index buffer，triangles和lines，默认triangles。
    + HitTest,Raytracer：射线的追踪，用于对每一个像素产生射线
    + Shader：将顶点和片源着色器封装在一起
    + Texture：渲染纹理,
    + Vector：向量的一些计算


+ water.js

  + The data in the texture is (position.y, velocity.y, normal.x, normal.z),以RGBA编码；
  + dropShader:计算下落后水的高度，
  + updateShader:更新shader的高度和速度，
  + normalShader:计算并更新高度和速度变化后的法向量，
  + sphereShader：计算球的新位置

## UI框架

用到轻量级UI框架--[dat.gui](https://github.com/dataarts/dat.gui)

