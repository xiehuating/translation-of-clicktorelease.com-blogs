

**This article is a Chinese translation version of [Vertex displacement with a noise function using GLSL and three.js](<https://www.clicktorelease.com/blog/vertex-displacement-noise-3d-webgl-glsl-three-js/>) by  [Jaume Sanchez](https://github.com/spite).**



**如果翻译中有谬误之处，请不吝指正~**



------

#### Terms | 术语

- Perlin noise：

------

<br/>

# Vertex displacement with a noise function using GLSL and three.js | 在GLSL和three.js中通过噪点函数实现顶点位移

文章写于2012年12月10日

阅读时间：10分钟

主题： WebGL， GLSL， three.js， shaders

* [**查看DEMO**](<https://www.clicktorelease.com/code/perlin/explosion.html>)
* [**GitHub代码链接**](<https://github.com/spite/vertex-displacement-noise-3d-webgl-glsl-three-js>)

![](/images/vertex-displacement-with-a-noise function/perlin-explosion.jpg)

这篇教程展示了创作一个带有形体变形动画的步骤：使用一个球体作为基本几何体，再使用perlin噪点对球体顶点位置扰乱。同时也教授了如何在扰乱上添加更多的变化，以及如何着色。本文在[Fireball explosion](https://www.clicktorelease.com/code/perlin/explosion.html)、以及[Experiments with Perlin Noise Series](https://www.clicktorelease.com/blog/experiments-with-perlin-noise)中的部分内容为基础写就。








