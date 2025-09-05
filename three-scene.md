# three-scene
基于 three 封装的场景功能


## 更新说明
- 0.1.41
- 


# 示例

```html
<template>
  <div :class="$style.container" ref="containerRef"></div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import { Scene } from 'three-scene'

const containerRef = ref()

const options: ConstructorParameters<typeof Scene>[0] = {
  camera: {
    position: [0, 3, 5]
  },
  grid: {
    visible: true
  },
  axes: {
    visible: true
  }
}

let scene: InstanceType<typeof Scene>

onMounted(() => {
  options.container = containerRef.value
  scene = new Scene(options)
  scene.run()
})
</script>
<style lang="scss" module>
.container {
  height: 100%;
  position: relative;
}
</style>
```



# Attributes
| 属性名         | 类型                                                | 说明                              |
| -------------- | --------------------------------------------------- | --------------------------------- |
| options        | Object                                              | [配置](/three-scene#options)      |
| container      | HTMLElement                                         | 容器                              |
| scene          | InstanceType &lt;typeof THREE.Scene&gt;             | 场景对象                          |
| renderer       | InstanceType &lt;typeof THREE.WebGLRenderer&gt;     | 渲染器对象                        |
| baseCamera     | InstanceType &lt;typeof THREE.PerspectiveCamera&gt; | 基础相机对象                      |
| cruiseCamera   | InstanceType &lt;typeof THREE.PerspectiveCamera&gt; | 巡航相机对象                      |
| cruiseGroup    | InstanceType &lt;typeof THREE.group&gt;             | 巡航组                            |
| controls       | InstanceType &lt;typeof OrbitControls&gt;           | 控制器对象                        |
| grid           | InstanceType &lt;typeof THREE.GridHelper&gt;        | 网格对象                          |
| animationId    | Number                                              | requestAnimationFrame 方法执行 id |
| pointer        | Object                                              | 鼠标事件关联属性                  |
| clock          | InstanceType &lt;typeof THREE.Clock&gt;             | 时间方法                          |
| cacheOptions   | Object                                              | 缓存配置项                        |
| pmremGenerator | InstanceType &lt;typeof THREE.PMREMGenerator&gt;    | 纹理触发器                        |

### Options
| 属性名           | 类型               | 可选值 | 默认值 | 说明                                        |
| ---------------- | ------------------ | ------ | ------ | ------------------------------------------- |
| container        | HTMLElement/String | -      | -      | 容器                                        |
| baseUrl          | String             | -      | ''     | 加载资源基本地址                            |
| bgColor          | Number/String      | -      | -      | 背景色,0x000000,'#000000'                   |
| bgUrl            | String/String[]    | -      | -      | 背景图数组（6 张图）时可组成环境图          |
| env              | String             | -      | -      | 场景环境，影响场景所有元素，仅支持 hdr 文件 |
| scale            | Number             | -      | 1      | 缩放倍数，具体表现在计算坐标位置            |
| fog              | Object             | -      | -      | [雾化](/three-scene#fog)                    |
| render           | Object             | -      | -      | [渲染器](/three-scene#render)               |
| controls         | Object             | -      | -      | [控制器](/three-scene#controls)             |
| ambientLight     | Object             | -      | -      | [环境光](/three-scene#ambientlight)         |
| directionalLight | Object             | -      | -      | [平行光](/three-scene#directionallight)     |
| camera           | Object             | -      | -      | [相机](/three-scene#camera)                 |
| grid             | Object             | -      | -      | [网格](/three-scene#grid)                   |
| axes             | Object             | -      | -      | [坐标](/three-scene#axes)                   |
| cruise           | Object             | -      | -      | [巡航](/three-scene#cruise)                 |

### Fog
| 属性名  | 类型          | 可选值 | 默认值 | 说明         |
| ------- | ------------- | ------ | ------ | ------------ |
| visible | Boolean       | -      | false  | 可见         |
| near    | Number        | -      | 100    | 雾化最近距离 |
| far     | Number        | -      | 1000   | 雾化最远距离 |
| color   | Number/String | -      | -      | 雾化颜色     |

### Render
| 属性名                 | 类型    | 可选值 | 默认值 | 说明                                                              |
| ---------------------- | ------- | ------ | ------ | ----------------------------------------------------------------- |
| antialias              | Boolean | -      | true   | 是否开启反锯齿                                                    |
| alpha                  | Boolean | -      | false  | 画布透明度缓冲区                                                  |
| logarithmicDepthBuffer | Boolean | -      | true   | 设置对数深度缓存                                                  |
| preserveDrawingBuffer  | Boolean | -      | false  | 是否保留缓冲区直到手动清除或覆盖，需要截图设置为 true，性能会下降 |

### Controls
| 属性名             | 类型    | 可选值 | 默认值   | 说明                                 |
| ------------------ | ------- | ------ | -------- | ------------------------------------ |
| visible            | Boolean | -      | false    | 可见                                 |
| autoRotate         | Boolean | -      | false    | 自动旋转                             |
| autoRotateSpeed    | Boolean | -      | 2        | 自动旋转速度                         |
| enableDamping      | Boolean | -      | false    | 阻尼（惯性）                         |
| dampingFactor      | Number  | -      | 0.25     | 阻尼系数，鼠标灵敏度(值越小惯性越大) |
| enablePan          | Boolean | -      | true     | 相机平移（右键拖拽）                 |
| enableRotate       | Boolean | -      | true     | 相机旋转                             |
| enableZoom         | Boolean | -      | true     | 缩放                                 |
| maxAzimuthAngle    | Number  | -      | Infinity | 旋转角度上限                         |
| minAzimuthAngle    | Number  | -      | Infinity | minAzimuthAngle                      |
| minDistance        | Number  | -      | 1        | 相机最近距离                         |
| maxDistance        | Number  | -      | 2000     | 相机最远距离                         |
| minPolarAngle      | Number  | -      | 0        | 垂直角度下限                         |
| maxPolarAngle      | Number  | -      | Math.PI  | 垂直角度上限                         |
| maxTargetRadius    | Number  | -      | Infinity | 目标移动半径                         |
| rotateSpeed        | Number  | -      | 1        | 旋转速度                             |
| screenSpacePanning | Boolean | -      | true     | 空间内平移/垂直平面平移              |



### AmbientLight
| 属性名    | 类型          | 可选值 | 默认值   | 说明       |
| --------- | ------------- | ------ | -------- | ---------- |
| visible   | Boolean       | -      | false    | 可见       |
| color     | Number/String | -      | 0xffffff | 环境光颜色 |
| intensity | Number        | -      | 1.5      | 光强度     |

### DirectionalLight
| 属性名    | 类型          | 可选值 | 默认值   | 说明             |
| --------- | ------------- | ------ | -------- | ---------------- |
| visible   | Boolean       | -      | false    | 可见             |
| helper    | Boolean       | -      | false    | 辅助器           |
| light2    | boolean       | -      | true     | 第二个平行光开启 |
| color     | Number/String | -      | 0xffffff | 平行光颜色       |
| intensity | Number        | -      | 1.5      | 光强度           |

### Camera
| 属性名     | 类型    | 可选值 | 默认值           | 说明                     |
| ---------- | ------- | ------ | ---------------- | ------------------------ |
| helper     | Boolean | -      | false            | 辅助器                   |
| near       | Number  | -      | 1                | 相机最近距离             |
| far        | Number  | -      | 10000            | 相机最远距离             |
| fov        | Number  | -      | 36               | 摄像机视锥体垂直视野角度 |
| orthogonal | Boolean | -      | -                | 正交                     |
| position   | Array   | -      | [-350, 510, 700] | 相机位置坐标             |

### Grid
| 属性名          | 类型          | 可选值 | 默认值   | 说明           |
| --------------- | ------------- | ------ | -------- | -------------- |
| visible         | Boolean       | -      | false    | 可见           |
| transparent     | Boolean       | -      | true     | 透明           |
| opacity         | Number        | -      | 0.3      | 透明度         |
| width           | Number        | -      | 800      | 网格宽度       |
| divisions       | Number        | -      | 80       | 网格等分数     |
| centerLineColor | Number/String | -      | 0xa1a1a1 | 中心线颜色     |
| gridColor       | Number/String | -      | 0xa1a1a1 | 网格颜色       |
| fork            | Boolean       | -      | false    | 网格交叉点     |
| forkSize        | Number        | -      | 1.4      | 网格交叉点大小 |
| forkColor       | Number/String | -      | 0xa1a1a1 | 网格交叉点颜色 |

### Axes
| 属性名  | 类型    | 可选值 | 默认值 | 说明       |
| ------- | ------- | ------ | ------ | ---------- |
| visible | Boolean | -      | false  | 可见       |
| size    | Number  | -      | 50     | 坐标轴大小 |

### Cruise
| 属性名         | 类型          | 可选值 | 默认值   | 说明                                          |
| -------------- | ------------- | ------ | -------- | --------------------------------------------- |
| visible        | Boolean       | -      | false    | 可见                                          |
| helper         | Boolean       | -      | false    | 辅助器                                        |
| points         | Array         | -      | []       | 巡航点位                                      |
| segment        | Number        | -      | 2        | 巡航分段数                                    |
| close          | Boolean       | -      | true     | 路径闭合                                      |
| tension        | Number        | -      | 0        | 巡航曲线张力                                  |
| baseUrl        | String        | -      | ''       | 加载资源基本地址                              |
| mapUrl         | String        | -      | 1        | 贴图地址                                      |
| factor         | number        | -      | -        | 系数                                          |
| repeat         | Array         | -      | [0.1, 1] | 贴图重复                                      |
| width          | Number        | -      | 15       | 宽度                                          |
| speed          | Number        | -      | 1        | 巡航时速度                                    |
| mapSpeed       | Number        | -      | 0.006    | 贴图材质动画滚动速度                          |
| offset         | Number        | -      | 10       | 巡航点偏差（距离巡航点的上下偏差）            |
| auto           | Boolean       | -      | -        | 自动巡航(可从动画函数执行机器人巡航)          |
| animateBack    | Function      | -      | -        | 帧动画回调函数                                |
| tube           | Boolean       | -      | false    | 管路模式                                      |
| color          | Number/String | -      | 0xffffff | 材质颜色                                      |
| radius         | Number        | -      | 1        | 半径 (管路模式未管路半径、平面模式为拐角半径) |
| radialSegments | Number        | -      | 1        | 路径分段                                      |
| alway          | Boolean       | -      | false    | 一直显示路线（默认巡航中展示路线）            |
| bloom          | Boolean       | -      | false    | 发光                                          |
| bloomIntensity | Number        | -      | 1        | 发光强度                                      |
| textTip        | Boolean       | -      | true     | 文本提示（按键规则）                          |
| cameraAutoMove | Boolean       | -      | true     | 相机自动移动                                  |



### Methods
| 方法名                          | 参数                            | 返回                    | 说明                                                         |
| ------------------------------- | ------------------------------- | ----------------------- | ------------------------------------------------------------ |
| debounce                        | -                               | -                       | 节流函数                                                     |
| setDebounceDuration             | ts                              | -                       | 设置节流时间                                                 |
| init                            | -                               | -                       | 初始化（灯光、网格、坐标轴、模型）                           |
| run                             | -                               | this                    | 运行（循环渲染、控制器可视操作）                             |
| loop                            | -                               | -                       | 循环（执行 requestAnimationFrame 方法）                      |
| animate                         | -                               | -                       | 更新渲染器、TWEEN 更新、巡航更新                             |
| render                          | -                               | -                       | 渲染-执行渲染方法                                            |
| sceneAddModel                   | -                               | -                       | 场景添加模型（创建场景后执行）                               |
| initModel                       | -                               | -                       | 业务模型初始化（继承后可在此方法内编写业务代码）             |
| modelAnimate                    | -                               | -                       | 业务代码模型动画（配套使用）                                 |
| createScene                     | -                               | Scene                   | 创建场景                                                     |
| createRender                    | -                               | 渲染器对象              | 创建渲染器                                                   |
| initRenderer                    | -                               | 渲染器对象              | 初始化渲染器                                                 |
| initBg                          | -                               | -                       | 初始化背景                                                   |
| initLight                       | -                               | -                       | 初始化灯光（环境光、平行光）                                 |
| createDirectional               | castShadow, s, size, near, far  | 平行光对象              | 创建平行光                                                   |
| createDirectionalLight          | color, intensity                | 平行光对象              | 创建平行光                                                   |
| createAmbientLight              | color, intensity                | 环境光对象              | 创建环境光                                                   |
| createPerspectiveCamera         | fov, aspect, near, far          | 景深相机对象            | 创建景深相机                                                 |
| initCamera                      | -                               | 景深相机对象            | 初始化相机                                                   |
| createConstrols                 | -                               | 控制器对象              | 创建控制器                                                   |
| initControls                    | -                               | 控制器对象              | 初始化控制器                                                 |
| initCruise                      | -                               | -                       | 初始化巡航                                                   |
| initGrid                        | -                               | -                       | 初始化网格                                                   |
| initAxes                        | -                               | -                       | 初始化坐标轴辅助器                                           |
| setCruisePoint                  | points                          | -                       | 设置巡航点位并生成巡航航道                                   |
| createCruise                    | -                               | -                       | 创建巡航航道                                                 |
| toggleCruise                    | -                               | -                       | 巡航开启或者关闭                                             |
| setScale                        | scale                           | -                       | 设置缩放大小，主要用于鼠标位置计算                           |
| loadEnvTexture                  | envUrl                          | -                       | 加载环境纹理                                                 |
| convertPmremTexture             | texture                         | texture                 | 转换 pmrem 环境纹理                                          |
| setEnv                          | texture                         | -                       | 设置场景环境纹理                                             |
| setBgTexture                    | bgUrl                           | -                       | 设置背景图                                                   |
| setBgColor                      | color                           | -                       | 设置背景色                                                   |
| exportImage                     | -                               | -                       | 导出场景图片( render 中 preserveDrawingBuffer 需设置为 true) |
| addObject                       | ...objects                      | -                       | 场景添加对象                                                 |
| controlSave                     | -                               | -                       | 控制保存                                                     |
| controlReset                    | -                               | -                       | 控制器重置                                                   |
| resize                          | -                               | -                       | 重置画布大小                                                 |
| createClock                     | -                               | -                       | 创建时间控件                                                 |
| createGround                    | （sizeX, sizeY, color）         | 地面网格对象            | 创建地面                                                     |
| getPosition                     | -                               | 相机坐标、控制器 target | 获取当前视角坐标                                             |
| isCameraMove                    | (to, distance)                  | -                       | 检测相机是否移动                                             |
| getValidTargetPosition          | (config, to, target, defaultTo) | -                       | 获取有效的目标点，并设置控制器中心点                         |
| getFrustum                      | -                               | THREE.Frustum           | 获取视维体                                                   |
| frustumIntersectsBox            | (frustum, object)               | Boolean                 | 检测视维体是否与对象相交                                     |
| movementXToAngle                | movementX                       | angle                   | 检测视维体是否与对象相交                                     |
| getWorldDirectionForwardVector3 | obj                             | length                  | 获取目标世界方向前进长度坐标                                 |
| bindEvent                       | -                               | -                       | 绑定鼠标事件                                                 |
| onDblclick                      | mouseEvent                      | -                       | 双击事件                                                     |
| onPointerDown                   | pointerEvent                    | -                       | 鼠标按下事件                                                 |
| onPointerMove                   | pointerEvent                    | -                       | 鼠标移动事件                                                 |
| onPointerUp                     | pointerEvent                    | -                       | 鼠标弹起事件                                                 |
| stopAnimate                     | -                               | -                       | 停止动画（requestAnimationFrame）                            |
| disposeObj                      | obj                             | -                       | 清除场景对象                                                 |
| dispose                         | -                               | -                       | 场景销毁                                                     |




### XYZ
| 属性名 | 类型   |
| ------ | ------ |
| x      | Number |
| y      | Number |
| z      | Number |
