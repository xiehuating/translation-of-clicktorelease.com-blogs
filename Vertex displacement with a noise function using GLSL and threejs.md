

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

![](/images/vertex-displacement-with-a-noise-function/perlin-explosion.jpg)

这篇教程展示了创作一个带有形体变形动画的过程：使用一个球体作为基本几何体，使用perlin噪点对球体顶点位置扰乱。同时也教授了如何在扰乱上添加更多的变化以及如何添加着色。本文在[Fireball explosion](https://www.clicktorelease.com/code/perlin/explosion.html)示例，以及[Experiments with Perlin Noise Series](https://www.clicktorelease.com/blog/experiments-with-perlin-noise)示例中的部分内容为基础写就。

我使用[three.js](https://github.com/mrdoob/three.js/)创建几何体并配置场景，但GLSL代码可以使用任何其他WebGL或OpebGl的库。我可以肯定它也能相当直接的转换成HLSL语言。

![](/images/vertex-displacement-with-a-noise-function/keyboard.svg)

我将在本教程中假定你已经掌握了一定WebGl的知识或其他你偏爱的同类3D库的知识。我将使用three.js编写必要的代码来配置场景，但不会做过多的讲解。[**市面上已经有很多此类例子和文档了。**](https://threejs.org/)_您可能需要先查看本文的示例链接，我会尽量保持这些示例非常基础。_

<br/>

## Creating the scene: a sphere and a camera | 创建场景：一个球体和一个摄像机

在开始前我们需要做几件事，包括：引入three.js，然后创建`renderer`，`scene`，`camera`，`material`和`mesh`。我们的`scene`将包含`mesh`和`camera`，并且`camera`镜头将会正对`mesh`。*如果你要使用键盘或鼠标控制摄像机的移动，你可以查看本文中的其中任何一个示例代码是怎么做的。*

我们将使用球体几何体来创建`mesh`，因为使用它能很方便满足我们的需求。在我们进行更复杂的着色前，可以把`material`暂时设置为线框着色器。*带有鲜艳颜色的线框是调试3D的好帮手。*

以下是起步阶段的代码：

```
// Basic page | 基础页面
// HTML - index.html | index.html页面中的HTML代码

<!doctype html>
<html lang="en">
  <head>
    <title>Perlin noise | Fireball explosion</title>
    <meta charset="utf-8">
  </head>

  <body>
    <div id="container"></div>
  </body>

  <script src="js/three.min.js"></script>

  <script type="x-shader/x-vertex" id="vertexShader">
  // Put the Vertex Shader code here
  </script>

  <script type="x-shader/x-vertex" id="fragmentShader">
  // Put the Fragment Shader code here
  </script>

  <script type="text/javascript" id="mainCode">
  // Put the main code here
  </script>

</html>
```

然后把以下JavaScript代码添加到id为`mainCode`的`script`标签中。

```
// Three.js boilerplate | Three.js引用
// JavaScript - index.html | index.html页面中的JavaScript代码

var container,
    renderer,
    scene,
    camera,
    mesh,
    start = Date.now(),
    fov = 30;

window.addEventListener( 'load', function() {

  // grab the container from the DOM
  container = document.getElementById( "container" );

  // create a scene
  scene = new THREE.Scene();

  // create a camera the size of the browser window
  // and place it 100 units away, looking towards the center of the scene
  camera = new THREE.PerspectiveCamera(
    fov,
    window.innerWidth / window.innerHeight,
    1,
    10000
  );
  camera.position.z = 100;

  // create a wireframe material
  material = new THREE.MeshBasicMaterial( {
    color: 0xb7ff00,
    wireframe: true
  } );

  // create a sphere and assign the material
  mesh = new THREE.Mesh(
    new THREE.IcosahedronGeometry( 20, 4 ),
    material
  );
  scene.add( mesh );

  // create the renderer and attach it to the DOM
  renderer = new THREE.WebGLRenderer();
  renderer.setSize( window.innerWidth, window.innerHeight );
  renderer.setPixelRatio( window.devicePixelRatio );

  container.appendChild( renderer.domElement );

  render();

} );

function render() {

  // let there be light
  renderer.render( scene, camera );
  requestAnimationFrame( render );

}
```

这样就建立了一个场景，一个位于场景中央、半径为20、由200x200个片段组成的线框球体。一个相机从100个单位以外观察它。尝试更改球体中的半径或线段，或将相机或网格移动到其他位置。

[**点击查看第一步示例**](https://www.clicktorelease.com/code/vertex-displacement-noise-3d-webgl-glsl-three-js/creating-scene-mesh-camera.html)

![](/images/vertex-displacement-with-a-noise-function/the-first-step.jpg)

<br/>

## Creating our custom shader | 创建自定义着色器