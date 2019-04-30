

**This article is a Chinese translation version of [Experiments with Perlin noise](https://www.clicktorelease.com/blog/experiments-with-perlin-noise/) by  [Jaume Sanchez](https://github.com/spite).**



<br/>

**如果翻译中有谬误之处，请不吝指正~**

<br/>



------

# Experiments with Perlin noise | Perlin噪点实验

文章发表于2012年6月30日

阅读时间：1分钟

主题： WebGL， GLSL， three.js， Perlin noise 

* [**GitHub代码链接**](<https://github.com/spite/perlin-experiments>)

<br/>

通过使用 **WebGL** 框架 **three.js** 在顶点着色器和片元着色器中尝试 **perlin noise** 。通过在顶点着色器中使用3D噪点进行大量的位移映射。

<br/>

## Chrome | 镀铬效果

使用Perlin Noise来扰乱球体表面，并且扭曲幅度会随时间而变化。在环境贴图上使用等距柱状（[equirectangular](https://en.wikipedia.org/wiki/Equirectangular_projection)）全景着色器，lambert + specular着色会基于全景图中探测到的光源进行着色。

![](/images/experiments-with perlin-noise/perlin-chrome.jpg)

这是最终效果，使用 [**three.js**](https://github.com/mrdoob/three.js/) 和  [**ashima noise**](https://github.com/ashima/webgl-noise/) 完成。

> [**点击查看镀铬金属蠕动球体**](https://www.clicktorelease.com/code/perlin/chrome.html)

<br/>

## Lights

此实验使用较低频率的 Perlin Noise 来扰乱球体，片元着色器使用三种类似的噪点来创建RGB颜色组合。此外，还有一个后处理渲染通道，执行了径向或缩放模糊。

![](/images/experiments-with perlin-noise/perlin-lights.jpg)

这是最终效果，使用 [**three.js**](https://github.com/mrdoob/three.js/) 、 [**ashima noise**](https://github.com/ashima/webgl-noise/) 以及 [**evanw's zoom blur**](https://github.com/evanw/webgl-filter) 完成。

> [**点击查看辉光蠕动球体**](https://www.clicktorelease.com/code/perlin/lights.html)

<br/>

## Explosion | 爆炸效果

这个示例中，球体在顶点着色器中被更激烈的3D噪点扰动。我截取了一张爆炸图片的一部分，以获得一个渐变图像，该图像在片元着色器中根据到达爆炸中心的距离进行采样*（译注：原文为 I **sampled** a picture of an explosion to obtain a gradient image that is sampled in the fragment shader depending on the distance to the center of the explosion. 此处第一sampled翻译成截取，因为在本文末尾作者推荐的博文中就是这么描述的，这里作者的做法可能是参考爆炸的图片，使用平面绘图软件将爆炸的颜色取出，然使用绘图软件做成这样[一张细长条的图片](/images/experiments-with perlin-noise/explosion.jpg)，也可能是直接在爆炸图片上截取一部分）*。越接近中心，越亮。

![](/images/experiments-with perlin-noise/perlin-explosion.jpg)

这是最终效果，使用 [**three.js**](https://github.com/mrdoob/three.js/) 、 [**ashima noise**](https://github.com/ashima/webgl-noise/) ，并使用了 [**evanw's random function**](https://github.com/evanw/webgl-filter) 在最终效果上添加了一些噪点。

> [**点击查看Perlin火球爆炸**](https://www.clicktorelease.com/code/perlin/explosion.html)

<br/>

## That's all! | 就这样！

您可能还对[**Vertex displacement with a noise function using GLSL and three.js**](https://www.clicktorelease.com/blog/vertex-displacement-noise-3d-webgl-glsl-three-js)（译注：[此文中文翻译](https://github.com/xiehuating/translation-of-clicktorelease.com-blogs/blob/master/Vertex%20displacement%20with%20a%20noise%20function%20using%20GLSL%20and%20threejs.md)）感兴趣，这篇博文详细介绍了如何创建此效果。

<br/>

------

<br/>

<br/>

<br/>

Interpreted by [Xie Huating](https://github.com/xiehuating/), 2019-04-22

转载此文请注明 [**原文出处**](https://www.clicktorelease.com/blog/creating-spherical-environment-mapping-shader/) 与 [**翻译出处**](https://github.com/xiehuating/creating-spherical-environment-mapping-shader)

<br/>

<br/>

<br/>