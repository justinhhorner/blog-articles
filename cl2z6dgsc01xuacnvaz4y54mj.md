## Introduction to WebGL using Three.js

Over the years I've become comfortable making 2D and 3D games using popular game engines such as Unreal and Unity. When I want to make a game available to play via browser, I depend on the WebGL builds, which makes it incredibly easy to do so.

With that said, for a while now I've been interested in learning the inner workings of WebGL and how to build 3D applications with it. How do these magic exports take my game built in a large engine and make them playable via a web browser?

Okay, slow down. Let's start from the beginning with an introduction to Three.js, a light abstraction over WebGL we can use to begin exploring concepts such as scenes, cameras, geometry, meshes, and renderers.

## What is WebGL?
**WebGL** stands for Web Graphics Library, and it is a JavaScript API supported by modern browsers, that enables high-performance 2D and 3D graphics powered by the **Graphics Processing Unit** (GPU). This means we can create immersive 3D experiences in the browser without plugins at incredible speeds due in part to WebGL conforming to **OpenGL ES**; which makes possible the use of hardware graphics acceleration.

You might be wondering how the GPU can handle this workload so much more efficiently than the CPU. That's because GPUs are able to execute a great number of calculations in parallel, making short work of having to calculate the position of thousands of vertices or more, and draw the visible pixels at 30, 60, or even more times per second.

How does the GPU know how to draw the visual pixels within a set of vertices? Ah, that's where **shaders** come into play. Shaders are programs written to accept data and output a final outcome to be rendered as pixels. They take into account the position, scale, and rotation of the model and the camera, and light data to create the final output.

### Prove It
Here are some examples of WebGL in action! It's quite amazing what is possible right in the browser. Check them out.

[Medal of Honor: Above and Beyond](https://www.oculus.com/medal-of-honor)
![MOH.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651337882779/XQXtpGkyK.png align="left")

[Windland](https://windland-neotix.vercel.app)
![Windland.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651337935617/NKJ-M6k4p.png align="left")

[Bijenkorf Magical Forest](https://admireamaze.debijenkorf.nl)
![Magical Forest.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651338059493/o5pghwDox.png align="left")

[Heraclos](https://heraclosgame.com)
![Heraclos.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651337974751/yy05PaxFw.png align="left")

## What is Three.js?
Now we have a high-level understanding of what WebGL is, why wouldn't we just use it? What's the purpose of Three.js? WebGL is a low-level API, which means it is incredibly powerful, but it's also a lot of work for very little output. It could take 100+ lines of code to draw something as simple as a single triangle on the screen. 

**Three.js** is an abstraction right above WebGL that makes working with it significantly easier and faster. That's not to say that you will lose control of optimizations and handling lower-level details yourself if you want to. Since Three.js sits just above WebGL, it provides access to work at the lower levels when necessary.

Three.js was created by [Ricardo Cabello](https://mrdoob.com), who is commonly known as [Mr.doob](https://twitter.com/mrdoob). Check out the project on [GitHub](https://github.com/mrdoob/three.js) to keep up to date with the latest developments.

## Hello, Three.js
Let's get started with a "Hello, world" style application for graphics, which is displaying a centered cube. It's intentionally simple but covers several concepts we can build upon in later articles.

Before we get started, we need to get a copy of three.js itself. I'm going to use a CDN, but you can download the full or minified version to use locally from [the repository](https://github.com/mrdoob/three.js/tree/dev/build).

### HTML
First, let's create an empty JavaScript file called `script.js` and an `index.html` file with three.js included.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello, Three.js!</title>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="./script.js"></script>
</body>
</html>
```

Now, in our `script.js` file, we can access the Three.js API through the variable `THREE`. To display a cube we will need 3 essential components; a scene, a camera, and a renderer.

### Scene
A [scene](https://threejs.org/docs/index.html?q=scene#api/en/scenes/Scene) is a collection of data that describes what we want to be rendered and where to render it. Therefore, it is where we will need to store the objects, lighting data, and cameras.

To create a scene, I'll declare a constant called `scene` and assign it a new THREE. Scene.

```javascript
const scene = new THREE.Scene();
```

### Camera
I'll spare you the definition of a camera, but you should know that Three.js contains several types of cameras that all inherit from the abstract `Camera` class.

We want a camera that mimics the way we see, so I'll create a new `PerspectiveCamera`. At a minimum, we need to provide it with the field of view and the aspect ratio we want.

At the top of the file, I added another constant to represent the rendered width and height that we'll use to set the camera's aspect ratio and pass to the renderer later.

```javascript
const size = { width: 800, height: 600 };

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, size.width / size.height);
```

### Meshes
Now we can create an object to display in the scene. Objects in the scene can be of many types; primitive shapes, models exported from 3D modeling software, lights, etc.

Creating a cube in the scene means we need to create a [Mesh](https://threejs.org/docs/index.html?q=Mesh#api/en/objects/Mesh), which is a combination of the geometry and a material. The geometry defines the shape (the triangle vertices of the shape) and the material defines how the presentation or look of the geometry.

A cube is simple enough that we can use the built-in [BoxGeometry](https://threejs.org/docs/index.html#api/en/geometries/BoxGeometry) and [MeshBasicMaterial](https://threejs.org/docs/index.html?q=MeshBasicMaterial#api/en/materials/MeshBasicMaterial) to accomplish our goal.

We need to provide BoxGeometry with a size in units for X, Y, and Z.
```javascript
const size = { width: 800, height: 600 };

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, size.width / size.height);

const geometry = new THREE.BoxGeometry(1, 1, 1);
```

Next, we'll create a material with a purple color using hexadecimal.
```javascript
const size = { width: 800, height: 600 };

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, size.width / size.height);

const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0x630063 });
```

Finally, we'll create a Mesh object using the geometry and material. Then, we'll add both the mesh and camera to the scene (otherwise, we'll have no way of displaying them).
```javascript
const size = { width: 800, height: 600 };

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, size.width / size.height);

const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0x630063 });
const mesh = new THREE.Mesh(geometry, material);

scene.add(camera);
scene.add(mesh);
```

### Renderer
No surprise here; the renderer is responsible for rendering the scene. On what surface does it render the scene, though? For that, we will need a canvas.

The renderer can do this for you automatically, but since this is an introduction, let's start by doing so ourselves, and then I'll show you how to tell the renderer to create a canvas for us. 

Head back to the index.html file and add a canvas element with an id of `canvas` to the body.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello, Three.js!</title>
</head>
<body>
    <canvas id="canvas"></canvas>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="./script.js"></script>
</body>
</html>
```

Now, we'll create a new [WebGLRenderer](https://threejs.org/docs/index.html?q=WebGLRen#api/en/renderers/WebGLRenderer) and provide it with the canvas element. Right after that, we'll use the `setSize` function to set the width and height.

The render will not start rendering automatically. We need to tell it we want to begin rendering by calling the `render` function and providing it with the scene and camera to render.

```javascript
const size = { width: 800, height: 600 };

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, size.width / size.height);
camera.position.z = 4;

const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0x630063 });
const mesh = new THREE.Mesh(geometry, material);

scene.add(camera);
scene.add(mesh);

const renderer = new THREE.WebGLRenderer({
    canvas: document.querySelector('#canvas')
});
renderer.setSize(size.width, size.height);
renderer.render(scene, camera);
```

## The Result
Let's go back to the browser and refresh to see our beautiful creation.

![render-fail.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651367204196/l-C1e3LCN.png align="left")

Well, not quite. Everything we wanted to be rendered is actually there, but we can't see it. Why is that?

We created all the objects without setting a position value, which means everything rendered in the scene is at the origin, including our camera! Our camera is actually inside the cube, but because we're inside it, we don't see the cube at all.

We can either move the camera back or move the cube forward away from the camera. In Three.js, the coordinate system uses Z as the third dimension vector, so it is the value we need to pull away from or move close to the scene. Pulling back toward the screen (or to yourself) is moving in the positive direction, so I'll set the position to 6 just below line 4 where we create the camera constant.
```javascript
camera.position.z = 6;
```

To the browser and refresh! Just look at it in all its glory.
![render-success.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651367646586/a-AUfBRm1.png align="left")

"Wait", I hear you say, "That's not a 3D cube, that's a 2D square!". Well, it seems that way because we're looking directly at it. Let's change the X and Y position of the camera just below where we set the Z position so we can see the other surfaces.
```javascript
camera.position.z = 6;
camera.position.x = 1;
camera.position.y = 1;
```

![render-3d-position](https://cdn.hashnode.com/res/hashnode/image/upload/v1651370959721/WUTPLXt8h.png align="left")

## Canvas Delegation
Before we wrap up, I promised I would show you how to tell the renderer to create the canvas, so remove the canvas element from the index.html and the arguments passed to WebGLRenderer. Then add this line just below where we call `setSize`.
```javascript
document.body.appendChild(renderer.domElement);
```

Go back to the browser and refresh to see the exact same result.

## Summary
Let's quickly recap our "Hello, world" app. Here are the high-level steps we took:

* Created `index.html` and `script.js` files
* Created a Scene and Perspective Camera
* Created a Box Geometry for the cube
* Created a material with the color 0x630063
* Created a mesh to combine our geometry and material
* Added the camera and mesh objects to the Scene
* Created a WebGLRenderer and set the width and height
* Finally, we render the scene by calling render

That's an introduction to WebGL using Three.js. I'm going to cover Three.js a lot more in the coming weeks, so if you find this helpful please consider sharing it and future articles with others, and follow me on Twitter and LinkedIn for more programming talk.

Take care.  
Stay awesome.