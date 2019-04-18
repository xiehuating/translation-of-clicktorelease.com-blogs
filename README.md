

This article is a Chinese translation version of [Creating a Spherical Reflection/Environment Mapping shader](https://www.clicktorelease.com/blog/creating-spherical-environment-mapping-shader/) by  [Jaume Sanchez](https://github.com/spite).



------

#### Terms | 术语

- [SEM](http://wiki.polycount.com/wiki/Spherical_environment_map): Spherical Reflection/Environment Mapping，译为球面反射/环境贴图。
- [LitSphere](http://wiki.polycount.com/w/index.php?title=Lit_Sphere&redirect=no): Lit Sphere，或Lit spheres，直译为被照亮的球体 。
- [MatCap](http://wiki.unity3d.com/index.php/MatCap): Matcaps，或Material Capture，译为材质捕获。
- [Suzanne](https://en.wikipedia.org/wiki/Blender_(software)#Suzanne): a monkey header 3D model，是一个猴子头部的三维模型。

------



# Creating a Spherical Reflection/Environment Mapping shader | 创建一个SEM着色器

文章写于2014年4月16日
阅读时间：5分钟；
主题： WebGL， GLSL， three.js， shaders

* [**查看DEMO**](https://www.clicktorelease.com/code/spherical-environment-mapping/)
* [**GitHub代码链接**](https://github.com/spite/spherical-environment-mapping)

![](images\spherical-environment-mapping.jpg.webp)

灯光是电脑生成图像最重要的部分之一。为了等到最终真实可信的展示效果，需要进行大量计算、设置以及微调工作。

球面反射/环境贴图技术（SEM）是一种模拟*（译注：此处表达的是伪造、仿造的意思，表示这种技术并没有真正的使用着色器中的光照算法来实现，只是用一张静态的位图来模拟反射光）*光照算法中高光反射的快捷方法，在特定的使用场景中，甚至可以模拟完整光照实现效果。这种技术已经在三维软件中广泛应用，如： [**Pixologic ZBrush**](http://pixologic.com/zbrush/downloadcenter/library/) 和 [**Luxology Modo**](http://docs.luxology.com/modo/701/help/pages/shaderendering/ShaderItems/MatCap.html)。



## LitSphere/MatCap texture maps | 纹理贴图
SEM使用被叫做“lit spheres”或“matcaps”的特制纹理贴图。它们就是基本的球面反射贴图，但是显示效果上有更多漫反射颜色，而不是像下图中最左侧的金属反光球一样将场景清晰的反射出来。这种球面贴图包含了在相机前方展示的所有元素，也就说此贴图包含了入射光线照射到的、面朝相机的球体表面*（译注：另一个意思是背朝相机的那部分反射因为相机没有拍摄到，所以贴图中也没有办法表达）*。这也是它不能作为完美环境贴图*（译注：原文为perfect environment map，应该指的是[Cube map](https://en.wikipedia.org/wiki/Cube_mapping)、[Equirectangular](https://en.wikipedia.org/wiki/Equirectangular_projection)这种捕获到360°的环境贴图方式）*的原因：因为缺失了背朝相机部分的图像信息，所以这种反射不能跟随相机视角旋转而旋转。我们所能模拟的是：相机和灯光是固定不动的，模型自身转动的效果*（译注：类似淘宝商家拍摄360°展示的商品照片，相机是放在三脚架上固定的，灯光也是固定的，就产品在一个转盘上自身旋转。[见示例](images/rotate-example.gif)）*。

![](images\spherical-maps.jpg.webp)


## Setting up the shader | 配置着色器
TBD



## Assigning the material to an object | 将材质指定到几何体
TBD



## Phong (per-fragment) shading | Phong着色器（逐片元）
TBD



## DEMO | 示例
TBD




## Conclusion | 小结
TBD