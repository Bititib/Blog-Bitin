# Threejs

Three.js是封装了WebGL的API，类似是WebGL的升级;用来制作页面3D效果;

## 安装

可以使用[npm](https://www.npmjs.com/)以及现代构建工具来安装 three.js ，也可以只需静态主机或是 CDN 来快速上手。对于大多数用户来说，从 npm 安装是最佳选择。

### npm 

> npm install three
>
> ```js
> // 方式 1: 导入整个 three.js核心库
> import * as THREE from 'three';
> 
> const scene = new THREE.Scene();
> 
> 
> // 方式 2: 仅导入你所需要的部分
> import { Scene } from 'three';
> 
> const scene = new Scene();
> ```
>
> 

### CDN 

>```js
><script async src="https://unpkg.com/es-module-shims@1.6.3/dist/es-module-shims.js"></script>
>// 以importmap方式引入
><script type="importmap">
>	{
>	"imports": {
>		"three": "https://unpkg.com/three@<version>/build/three.module.js",
>		"three/addons/": "https://unpkg.com/three@<version>/examples/jsm/"
>	}
>	}
></script>
>
><script type="module">
>
>	import * as THREE from 'three';
>    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
>
>        const controls = new OrbitControls( camera, renderer.domElement );
>	const scene = new THREE.Scene();
>
></script>
>```
>
>`注意 : ` 当通过CDN方式引入其他组件的时候要确保与three核心库的版本保持一致；否则，使用组件的时候会报错;

## 核心知识

一个基本3D场景需要有: 场景(Scene) , 视角/相机(Camera),渲染(renderer)

### Scene

场景能够让你在什么地方、摆放什么东西来交给three.js来渲染，这是你放置物体、灯光和摄像机的地方。

> ## 构造器
>
> ### Scene()
>
> 创建一个新的场景对象。
>
> ## 属性
>
> ### .[background](https://threejs.org/docs/index.html#api/zh/scenes/Scene.background) : Object
>
> 若不为空，在渲染场景的时候将设置背景，且背景总是首先被渲染的。 可以设置一个用于的“clear”的[Color](https://threejs.org/docs/index.html#api/zh/math/Color)（颜色）、一个覆盖canvas的[Texture](https://threejs.org/docs/index.html#api/zh/textures/Texture)（纹理）， 或是 a cubemap as a [CubeTexture](https://threejs.org/docs/index.html#api/zh/textures/CubeTexture) or an equirectangular as a [Texture](https://threejs.org/docs/index.html#api/zh/textures/Texture)。默认值为null。
>
> ### .[backgroundBlurriness](https://threejs.org/docs/index.html#api/zh/scenes/Scene.backgroundBlurriness) : Float
>
> Sets the blurriness of the background. Only influences environment maps assigned to [Scene.background](https://threejs.org/docs/index.html#api/zh/scenes/Scene.background). Valid input is a float between **0** and **1**. Default is **0**.
>
> ### .[environment](https://threejs.org/docs/index.html#api/zh/scenes/Scene.environment) : [Texture](https://threejs.org/docs/index.html#api/zh/textures/Texture)
>
> 若该值不为null，则该纹理贴图将会被设为场景中所有物理材质的环境贴图。 然而，该属性不能够覆盖已存在的、已分配给 [MeshStandardMaterial.envMap](https://threejs.org/docs/index.html#api/zh/materials/MeshStandardMaterial.envMap) 的贴图。默认为null。
>
> ### .[fog](https://threejs.org/docs/index.html#api/zh/scenes/Scene.fog) : [Fog](https://threejs.org/docs/index.html#api/zh/scenes/Fog)
>
> 一个[fog](https://threejs.org/docs/index.html#api/zh/scenes/Fog)实例定义了影响场景中的每个物体的雾的类型。默认值为null。
>
> ### .[isScene](https://threejs.org/docs/index.html#api/zh/scenes/Scene.isScene) : Boolean
>
> Read-only flag to check if a given object is of type Scene.
>
> ### .[overrideMaterial](https://threejs.org/docs/index.html#api/zh/scenes/Scene.overrideMaterial) : [Material](https://threejs.org/docs/index.html#api/zh/materials/Material)
>
> 如果不为空，它将强制场景中的每个物体使用这里的材质来渲染。默认值为null。
>
> ## 方法
>
> ### .[toJSON](https://threejs.org/docs/index.html#api/zh/scenes/Scene.toJSON) : Object
>
> meta -- 包含有元数据的对象，例如场景中的的纹理或图片。 将scene对象转换为 three.js [JSON Object/Scene format](https://github.com/mrdoob/three.js/wiki/JSON-Object-Scene-format-4)（three.js JSON 物体/场景格式）。

### Camera

摄像机的抽象基类。在构建新摄像机时，应始终继承此类。

> ## 构造函数
>
> ### Camera()
>
> 创建一个新的Camera（摄像机）。注意：这个类并不是被直接调用的；你所想要的或许是一个 [PerspectiveCamera](https://threejs.org/docs/index.html#api/zh/cameras/PerspectiveCamera)（透视摄像机）或者 [OrthographicCamera](https://threejs.org/docs/index.html#api/zh/cameras/OrthographicCamera)（正交摄像机）。
>
> ## 属性
>
> 共有属性请参见其基类[Object3D](https://threejs.org/docs/index.html#api/zh/core/Object3D)
>
> ### .[isCamera](https://threejs.org/docs/index.html#api/zh/cameras/Camera.isCamera) : Boolean
>
> Read-only flag to check if a given object is of type Camera.
>
> ### .[layers](https://threejs.org/docs/index.html#api/zh/cameras/Camera.layers) : [Layers](https://threejs.org/docs/index.html#api/zh/core/Layers)
>
> 摄像机是一个[layers](https://threejs.org/docs/index.html#api/zh/core/Layers)的成员. 这是一个从[Object3D](https://threejs.org/docs/index.html#api/zh/core/Object3D)继承而来的属性。
>
> 当摄像机的视点被渲染的时候，物体必须和当前被看到的摄像机共享至少一个层。
>
> ### .[matrixWorldInverse](https://threejs.org/docs/index.html#api/zh/cameras/Camera.matrixWorldInverse) : [Matrix4](https://threejs.org/docs/index.html#api/zh/math/Matrix4)
>
> 这是matrixWorld矩阵的逆矩阵。 MatrixWorld包含了相机的世界变换矩阵。
>
> ### .[projectionMatrix](https://threejs.org/docs/index.html#api/zh/cameras/Camera.projectionMatrix) : [Matrix4](https://threejs.org/docs/index.html#api/zh/math/Matrix4)
>
> 这是投影变换矩阵。
>
> ### .[projectionMatrixInverse](https://threejs.org/docs/index.html#api/zh/cameras/Camera.projectionMatrixInverse) : [Matrix4](https://threejs.org/docs/index.html#api/zh/math/Matrix4)
>
> 这是投影变换矩阵的逆矩阵。
>
> ## 方法
>
> 共有方法请参见其基类[Object3D](https://threejs.org/docs/index.html#api/zh/core/Object3D)。
>
> ### .[clone](https://threejs.org/docs/index.html#api/zh/cameras/Camera.clone) ( ) : [Camera](https://threejs.org/docs/index.html#api/zh/cameras/Camera)
>
> 返回一个具有和当前相机的属性一样的新的相机。
>
> ### .[copy](https://threejs.org/docs/index.html#api/zh/cameras/Camera.copy) ( source : [Camera](https://threejs.org/docs/index.html#api/zh/cameras/Camera), recursive : Boolean ) : this
>
> 将源摄像机的属性复制到新摄像机中。
>
> ### .[getWorldDirection](https://threejs.org/docs/index.html#api/zh/cameras/Camera.getWorldDirection) ( target : [Vector3](https://threejs.org/docs/index.html#api/zh/math/Vector3) ) : [Vector3](https://threejs.org/docs/index.html#api/zh/math/Vector3)
>
> [target](https://threejs.org/docs/index.html#api/zh/math/Vector3) — 调用该函数的结果将复制给该Vector3对象。
>
> 返回一个能够表示当前摄像机所正视的世界空间方向的[Vector3](https://threejs.org/docs/index.html#api/zh/math/Vector3)对象。 （注意：摄像机俯视时，其Z轴坐标为负。）

### Renderer

WebGL Render 用[WebGL](https://en.wikipedia.org/wiki/WebGL)渲染出你精心制作的场景; 同时要将渲染器挂载到body中 <code> document.body.appendChild(renderer.domElement)</code>

> ## 构造器
>
> ### WebGLRenderer( parameters : Object )
>
> parameters - (可选) 该对象的属性定义了渲染器的行为。也可以完全不传参数。在所有情况下，当缺少参数时，它将采用合理的默认值。 以下是合法参数：
>
> canvas - 一个供渲染器绘制其输出的[canvas](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas) 它和下面的[domElement](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.domElement)属性对应。 如果没有传这个参数，会创建一个新canvas
> context - 可用于将渲染器附加到已有的渲染环境([RenderingContext](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext))中。默认值是null
> precision - 着色器精度. 可以是 **"highp"**, **"mediump"** 或者 **"lowp"**. 如果设备支持，默认为**"highp"** .
> alpha - controls the default clear alpha value. When set to **true**, the value is **0**. Otherwise it's **1**. Default is **false**.
> premultipliedAlpha - renderer是否假设颜色有 [premultiplied alpha](https://en.wikipedia.org/wiki/Glossary_of_computer_graphics#Premultiplied_alpha). 默认为**true**
> antialias - 是否执行抗锯齿。默认为**false**.
> stencil - 绘图缓存是否有一个至少8位的模板缓存([stencil buffer](https://en.wikipedia.org/wiki/Stencil_buffer))。默认为**true**
> preserveDrawingBuffer -是否保留缓直到手动清除或被覆盖。 默认**false**.
> powerPreference - 提示用户代理怎样的配置更适用于当前WebGL环境。 可能是**"high-performance"**, **"low-power"** 或 **"default"**。默认是**"default"**. 详见[WebGL spec](https://www.khronos.org/registry/webgl/specs/latest/1.0/#5.14.12)
> failIfMajorPerformanceCaveat - 检测渲染器是否会因性能过差而创建失败。默认为false。详见 [WebGL spec](https://www.khronos.org/registry/webgl/specs/latest/1.0/#5.14.12) for details.
> depth - 绘图缓存是否有一个至少6位的深度缓存([depth buffer](https://en.wikipedia.org/wiki/Z-buffering) )。 默认是**true**.
> logarithmicDepthBuffer - 是否使用对数深度缓存。如果要在单个场景中处理巨大的比例差异，就有必要使用。 Note that this setting uses gl_FragDepth if available which disables the [Early Fragment Test](https://www.khronos.org/opengl/wiki/Early_Fragment_Test) optimization and can cause a decrease in performance. 默认是**false**。 示例：[camera / logarithmicdepthbuffer](https://threejs.org/examples/#webgl_camera_logarithmicdepthbuffer)
>
> ## 属性
>
> ### .[autoClear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClear) : Boolean
>
> 定义渲染器是否在渲染每一帧之前自动清除其输出。
>
> ### .[autoClearColor](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClearColor) : Boolean
>
> 如果[autoClear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClear)为true, 定义renderer是否清除颜色缓存。 默认是**true**
>
> ### .[autoClearDepth](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClearDepth) : Boolean
>
> 如果[autoClear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClear)是true, 定义renderer是否清除深度缓存。 默认是**true**
>
> ### .[autoClearStencil](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClearStencil) : Boolean
>
> 如果[autoClear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClear)是true, 定义renderer是否清除模板缓存. 默认是**true**
>
> ### .[debug](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.debug) : Object
>
> \- checkShaderErrors: 如果为true，定义是否检查材质着色器程序 编译和链接过程中的错误。 禁用此检查生产以获得性能增益可能很有用。 强烈建议在开发期间保持启用这些检查。 如果着色器没有编译和链接 - 它将无法工作，并且相关材料将不会呈现。 默认是**true**
> \- onShaderError( gl, program, glVertexShader, glFragmentShader ): A callback function that can be used for custom error reporting. The callback receives the WebGL context, an instance of WebGLProgram as well two instances of WebGLShader representing the vertex and fragment shader. Assigning a custom function disables the default error reporting. Default is `null`.
>
> ### .[capabilities](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.capabilities) : Object
>
> 一个包含当前渲染环境([RenderingContext](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext))的功能细节的对象。
> \- floatFragmentTextures: 环境是否支持[OES_texture_float](https://developer.mozilla.org/en-US/docs/Web/API/OES_texture_float)扩展
> \- floatVertexTextures: 如果floatFragmentTextures和vertexTextures都是true， 则此值为**true**
> \- getMaxAnisotropy(): 返回最大可用各向异性。
> \- getMaxPrecision(): 返回顶点着色器和片元着色器的最大可用精度。
> \- isWebGL2: **true** if the context in use is a WebGL2RenderingContext object.
> \- logarithmicDepthBuffer: 如果logarithmicDepthBuffer在构造器中被设为true且 环境支持[EXT_frag_depth](https://developer.mozilla.org/en-US/docs/Web/API/EXT_frag_depth)扩展，则此值为**true**
> \- maxAttributes: **gl.MAX_VERTEX_ATTRIBS**的值
> \- maxCubemapSize: **gl.MAX_CUBE_MAP_TEXTURE_SIZE** 的值，着色器可使用的立方体贴图纹理的最大宽度*高度
> \- maxFragmentUniforms: **gl.MAX_FRAGMENT_UNIFORM_VECTORS**的值，片元着色器可使用的全局变量(uniforms)数量
> \- maxSamples: The value of **gl.MAX_SAMPLES**. Maximum number of samples in context of Multisample anti-aliasing (MSAA).
> \- maxTextureSize: **gl.MAX_TEXTURE_SIZE**的值，着色器可使用纹理的最大宽度*高度
> \- maxTextures: *gl.MAX_TEXTURE_IMAGE_UNITS的值，着色器可使用的纹理数量
> \- maxVaryings: **gl.MAX_VARYING_VECTORS**的值，着色器可使用矢量的数量
> \- maxVertexTextures: **gl.MAX_VERTEX_TEXTURE_IMAGE_UNITS**的值，顶点着色器可使用的纹理数量。
> \- maxVertexUniforms: **gl.MAX_VERTEX_UNIFORM_VECTORS**的值，顶点着色器可使用的全局变量(uniforms)数量
> \- precision: 渲染器当前使用的着色器的精度
> \- vertexTextures: 如果 .[maxVertexTextures](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.maxVertexTextures) : Integer大于0，此值为**true** (即可以使用顶点纹理)
>
> ### .[clippingPlanes](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clippingPlanes) : Array
>
> 用户自定义的剪裁平面，在世界空间中被指定为THREE.Plane对象。 这些平面全局使用。空间中与该平面点积为负的点将被切掉。 默认值是[]
>
> ### .[domElement](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.domElement) : DOMElement
>
> 一个[canvas](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas)，渲染器在其上绘制输出。
> 渲染器的构造函数会自动创建(如果没有传入canvas参数);你需要做的仅仅是像下面这样将它加页面里去:
> `document.body.appendChild( renderer.domElement );`
>
> ### .[extensions](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.extensions) : Object
>
> \- get( extensionName : String ): 用于检查是否支持各种扩展，并返回一个对象，其中包含扩展的详细信息。 该方法检查以下扩展：
>
> - **WEBGL_depth_texture**
> - **EXT_texture_filter_anisotropic**
> - **WEBGL_compressed_texture_s3tc**
> - **WEBGL_compressed_texture_pvrtc**
> - **WEBGL_compressed_texture_etc1**
>
> 
>
> ### .[outputColorSpace](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.outputColorSpace) : string
>
> 定义渲染器的输出编码。默认为[THREE.SRGBColorSpace](https://threejs.org/docs/index.html#api/zh/constants/Textures)
>
> 如果渲染目标已经使用 [.setRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setRenderTarget)、之后将直接使用renderTarget.texture.colorSpace
>
> 查看[texture constants](https://threejs.org/docs/index.html#api/zh/constants/Textures)页面以获取其他格式细节
>
> ### .[info](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.info) : Object
>
> 一个对象，包含有关图形板内存和渲染过程的一系列统计信息。这些信息可用于调试或仅仅满足下好奇心。该对象包含以下字段:
>
> 
>
> - memory:
>   - geometries
>   - textures
> - render:
>   - calls
>   - triangles
>   - points
>   - lines
>   - frame
> - programs
>
> 
>
> 默认情况下，这些字段在每次渲染调用时都会重置，但是当每帧有多个渲染通道时（例如，使用后处理时），最好使用自定义模式重置。先将 autoReset 设置为 false.`renderer.info.autoReset = false;`然后在单个帧时渲染完成后调用 reset().`renderer.info.reset();`
>
> ### .[localClippingEnabled](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.localClippingEnabled) : Boolean
>
> 定义渲染器是否考虑对象级剪切平面。 默认为**false**.
>
> ### .[properties](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.properties) : Object
>
> 渲染器内部使用，以跟踪各种子对象属性。
>
> ### .[renderLists](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.renderLists) : WebGLRenderLists
>
> 在内部用于处理场景渲染对象的排序。
>
> ### .[shadowMap](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.shadowMap) : WebGLShadowMap
>
> 如果使用，它包含阴影贴图的引用。
> \- enabled: 如果设置开启，允许在场景中使用阴影贴图。默认是 **false**。
> \- autoUpdate: 启用场景中的阴影自动更新。默认是**true**
> 如果不需要动态光照/阴影, 则可以在实例化渲染器时将之设为false
> \- needsUpdate: 当被设为**true**, 场景中的阴影贴图会在下次**render**调用时刷新。默认是**false**
> 如果你已经禁用了阴影贴图的自动更新(**shadowMap.autoUpdate = false**), 那么想要在下一次渲染时更新阴影的话就需要将此值设为**true**
> \- type: 定义阴影贴图类型 (未过滤, 关闭部分过滤, 关闭部分双线性过滤), 可选值有:
>
> - THREE.BasicShadowMap
> - THREE.PCFShadowMap (默认)
> - THREE.PCFSoftShadowMap
> - THREE.VSMShadowMap
>
> 详见[Renderer constants](https://threejs.org/docs/index.html#api/zh/constants/Renderer)
>
> ### .[sortObjects](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.sortObjects) : Boolean
>
> 定义渲染器是否应对对象进行排序。默认是**true**.
>
> 说明: 排序用于尝试正确渲染出具有一定透明度的对象。根据定义，排序可能不总是有用。根据应用的需求，可能需要关闭排序并使其他方法来处理透明度的渲染，例如， 手动确定每个对象的渲染顺序。
>
> ### .[state](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.state) : Object
>
> 包含设置[WebGLRenderer.context](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.context)状态的各种属性的函数。
>
> ### .[toneMapping](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.toneMapping) : Constant
>
> 默认是[NoToneMapping](https://threejs.org/docs/index.html#api/zh/constants/Renderer)。查看[Renderer constants](https://threejs.org/docs/index.html#api/zh/constants/Renderer)以获取其它备选项
>
> ### .[toneMappingExposure](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.toneMappingExposure) : Number
>
> 色调映射的曝光级别。默认是**1**
>
> ### .[xr](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.xr) : [WebXRManager](https://threejs.org/docs/index.html#api/zh/renderers/webxr/WebXRManager)
>
> Provides access to the WebXR related [interface](https://threejs.org/docs/index.html#api/zh/renderers/webxr/WebXRManager) of the renderer.
>
> ## 方法
>
> ### .[clear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clear) ( color : Boolean, depth : Boolean, stencil : Boolean ) : undefined
>
> 告诉渲染器清除颜色、深度或模板缓存. 此方法将颜色缓存初始化为当前颜色。参数们默认都是**true**
>
> ### .[clearColor](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clearColor) ( ) : undefined
>
> 清除颜色缓存。 相当于调用[.clear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clear)( true, false, false )
>
> ### .[clearDepth](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clearDepth) ( ) : undefined
>
> 清除深度缓存。相当于调用[.clear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clear)( false, true, false )
>
> ### .[clearStencil](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clearStencil) ( ) : undefined
>
> 清除模板缓存。相当于调用[.clear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.clear)( false, false, true )
>
> ### .[compile](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.compile) ( scene : [Object3D](https://threejs.org/docs/index.html#api/zh/core/Object3D), camera : [Camera](https://threejs.org/docs/index.html#api/zh/cameras/Camera) ) : undefined
>
> 使用相机编译场景中的所有材质。这对于在首次渲染之前预编译着色器很有用。
>
> ### .[copyFramebufferToTexture](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.copyFramebufferToTexture) ( position : [Vector2](https://threejs.org/docs/index.html#api/zh/math/Vector2), texture : [FramebufferTexture](https://threejs.org/docs/index.html#api/zh/textures/FramebufferTexture), level : Number ) : undefined
>
> 将当前WebGLFramebuffer中的像素复制到2D纹理中。可访问[WebGLRenderingContext.copyTexImage2D](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/copyTexImage2D).
>
> ### .[copyTextureToTexture](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.copyTextureToTexture) ( position : [Vector2](https://threejs.org/docs/index.html#api/zh/math/Vector2), srcTexture : [Texture](https://threejs.org/docs/index.html#api/zh/textures/Texture), dstTexture : [Texture](https://threejs.org/docs/index.html#api/zh/textures/Texture), level : Number ) : undefined
>
> 将纹理的所有像素复制到一个已有的从给定位置开始的纹理中。可访问[WebGLRenderingContext.texSubImage2D](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/texSubImage2D).
>
> ### .[dispose](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.dispose) ( ) : undefined
>
> 处理当前的渲染环境
>
> ### .[forceContextLoss](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.forceContextLoss) () : undefined
>
> 模拟WebGL环境的丢失。需要支持 [WEBGL_lose_context](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_lose_context) 扩展才能用。
>
> ### .[forceContextRestore](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.forceContextRestore) ( ) : undefined
>
> 模拟WebGL环境的恢复。需要支持 [WEBGL_lose_context](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_lose_context) 扩展才能用。
>
> ### .[getClearAlpha](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getClearAlpha) () : Float
>
> 返回一个表示当前alpha值的float，范围0到1
>
> ### .[getClearColor](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getClearColor) ( target : [Color](https://threejs.org/docs/index.html#api/zh/math/Color) ) : [Color](https://threejs.org/docs/index.html#api/zh/math/Color)
>
> 返回一个表示当前颜色值的[THREE.Color](https://threejs.org/docs/index.html#api/zh/math/Color)实例
>
> ### .[getContext](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getContext) () : WebGL2RenderingContext
>
> 返回当前WebGL环境
>
> ### .[getContextAttributes](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getContextAttributes) () : WebGLContextAttributes
>
> 返回一个对象，这个对象中存有在WebGL环境在创建的时候所设置的属性
>
> ### .[getActiveCubeFace](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getActiveCubeFace) () : Integer
>
> Returns the current active cube face.
>
> ### .[getActiveMipmapLevel](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getActiveMipmapLevel) () : Integer
>
> Returns the current active mipmap level.
>
> ### .[getRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getRenderTarget) () : RenderTarget
>
> 如果当前存在RenderTarget，则返回该值；否则返回**null**。
>
> ### .[getCurrentViewport](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getCurrentViewport) () : RenderTarget
>
> 返回当前视口
>
> ### .[getDrawingBufferSize](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getDrawingBufferSize) () : Object
>
> 返回一个包含渲染器绘图缓存宽度和高度(单位像素)的对象。
>
> ### .[getPixelRatio](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getPixelRatio) () : number
>
> 返回当前使用设备像素比
>
> ### .[getSize](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.getSize) ( target : [Vector2](https://threejs.org/docs/index.html#api/zh/math/Vector2) ) : [Vector2](https://threejs.org/docs/index.html#api/zh/math/Vector2)
>
> 返回包含渲染器输出canvas的宽度和高度(单位像素)的对象。
>
> ### .[initTexture](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.initTexture) ( texture : [Texture](https://threejs.org/docs/index.html#api/zh/textures/Texture) ) : undefined
>
> 初始化给定的纹理。用于预加载纹理而不是等到第一次渲染（可能会由于解码和 GPU 上传的开销而导致明显的延迟）.
>
> ### .[resetGLState](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.resetGLState) ( ) : undefined
>
> 将GL状态重置为默认值。WebGL环境丢失时会内部调用
>
> ### .[readRenderTargetPixels](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.readRenderTargetPixels) ( renderTarget : [WebGLRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderTarget), x : Float, y : Float, width : Float, height : Float, buffer : TypedArray, activeCubeFaceIndex : Integer ) : undefined
>
> buffer - Uint8Array is the only destination type supported in all cases, other types are renderTarget and platform dependent. See [WebGL spec](https://www.khronos.org/registry/webgl/specs/latest/1.0/#5.14.12) for details.
>
> 将renderTarget中的像素数据读取到传入的缓冲区中。这是[WebGLRenderingContext.readPixels](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/readPixels)()的包装器
> 示例：[interactive / cubes / gpu](https://threejs.org/examples/#webgl_interactive_cubes_gpu)
>
> For reading out a [WebGLCubeRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLCubeRenderTarget) use the optional parameter activeCubeFaceIndex to determine which face should be read.
>
> ### .[render](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.render) ( scene : [Object3D](https://threejs.org/docs/index.html#api/zh/core/Object3D), camera : [Camera](https://threejs.org/docs/index.html#api/zh/cameras/Camera) ) : undefined
>
> 用相机([camera](https://threejs.org/docs/index.html#api/zh/cameras/Camera))渲染一个场景([scene](https://threejs.org/docs/index.html#api/zh/scenes/Scene))或是其它类型的[object](https://threejs.org/docs/index.html#api/zh/core/Object3D)。
> 渲染一般是在canvas上完成的，或者是[renderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderTarget)(如果有指定)
> 如果forceClear值是**true**，那么颜色、深度及模板缓存将会在渲染之前清除，即使渲染器的[autoClear](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClear)属性值是false
> 即便forceClear设为true, 也可以通过将[autoClearColor](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClearColor)、[autoClearStencil](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClearStencil)或[autoClearDepth](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.autoClearDepth)属性的值设为false来阻止对应缓存被清除。
>
> ### .[resetState](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.resetState) () : undefined
>
> 可用于重置内部 WebGL 状态。此方法主要与跨多个 WebGL 库共享单个 WebGL 上下文的应用程序相关。
>
> ### .[setAnimationLoop](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setAnimationLoop) ( callback : Function ) : undefined
>
> callback — 每个可用帧都会调用的函数。 如果传入‘null’,所有正在进行的动画都会停止。
>
> 可用来代替[requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)的内置函数. 对于WebXR项目，必须使用此函数。
>
> ### .[setClearAlpha](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setClearAlpha) ( alpha : Float ) : undefined
>
> 设置alpha。合法参数是一个**0.0**到 **1.0**之间的浮点数
>
> ### .[setClearColor](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setClearColor) ( color : [Color](https://threejs.org/docs/index.html#api/zh/math/Color), alpha : Float ) : undefined
>
> 设置颜色及其透明度
>
> ### .[setPixelRatio](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setPixelRatio) ( value : number ) : undefined
>
> 设置设备像素比。通常用于避免HiDPI设备上绘图模糊
>
> ### .[setRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setRenderTarget) ( renderTarget : [WebGLRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderTarget), activeCubeFace : Integer, activeMipmapLevel : Integer ) : undefined
>
> renderTarget -- 需要被激活的[renderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderTarget)(可选)。若此参数为空，则将canvas设置成活跃render target。
> activeCubeFace -- Specifies the active cube side (PX 0, NX 1, PY 2, NY 3, PZ 4, NZ 5) of [WebGLCubeRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLCubeRenderTarget). When passing a [WebGLArrayRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGLArrayRenderTarget) or [WebGL3DRenderTarget](https://threejs.org/docs/index.html#api/zh/renderers/WebGL3DRenderTarget) this indicates the z layer to render in to (optional).
> activeMipmapLevel -- Specifies the active mipmap level (optional).
>
> 该方法设置活跃rendertarget。
>
> ### .[setScissor](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setScissor) ( x : Integer, y : Integer, width : Integer, height : Integer ) : undefined
>
> 将剪裁区域设为(x, y)到(x + width, y + height) Sets the scissor area from
>
> ### .[setScissorTest](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setScissorTest) ( boolean : Boolean ) : undefined
>
> 启用或禁用剪裁检测. 若启用，则只有在所定义的裁剪区域内的像素才会受之后的渲染器影响。
>
> ### .[setSize](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setSize) ( width : Integer, height : Integer, updateStyle : Boolean ) : undefined
>
> 将输出canvas的大小调整为(width, height)并考虑设备像素比，且将视口从(0, 0)开始调整到适合大小 将updateStyle设置为false以阻止对canvas的样式做任何改变。
>
> ### .[setViewport](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer.setViewport) ( x : Integer, y : Integer, width : Integer, height : Integer ) : undefined
>
> 将视口大小设置为(x, y)到 (x + width, y + height).