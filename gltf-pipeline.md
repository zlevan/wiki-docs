# gltf-pipeline
模型文件转换工具

[https://github.com/CesiumGS/gltf-pipeline](https://github.com/CesiumGS/gltf-pipeline)


# 模型转换 gltf 转 glb
```js
gltf-pipeline -i model.gltf -o model.glb
gltf-pipeline -i model.gltf -b
```

# 模型转换 glb 转 gltf
```js
gltf-pipeline -i model.glb -o model.gltf
gltf-pipeline -i model.glb -j
```

# 模型 Draco 压缩
```js
gltf-pipeline -i model.gltf -o modelDraco.gltf -d
```

# 模型保存单独的纹理
```js
gltf-pipeline -i model.gltf -t
```



```js


// Converting a glTF to glb:
const gltfPipeline = require("gltf-pipeline");
const fsExtra = require("fs-extra");
const gltfToGlb = gltfPipeline.gltfToGlb;
const gltf = fsExtra.readJsonSync("./input/model.gltf");
const options = { resourceDirectory: "./input/" };
gltfToGlb(gltf, options).then(function (results) {
  fsExtra.writeFileSync("model.glb", results.glb);
})

// Converting a glb to embedded glTF
const gltfPipeline = require("gltf-pipeline");
const fsExtra = require("fs-extra");
const glbToGltf = gltfPipeline.glbToGltf;
const glb = fsExtra.readFileSync("model.glb");
glbToGltf(glb).then(function (results) {
  fsExtra.writeJsonSync("model.gltf", results.gltf);
})

// Converting a glTF to Draco glTF
const gltfPipeline = require("gltf-pipeline");
const fsExtra = require("fs-extra");
const processGltf = gltfPipeline.processGltf;
const gltf = fsExtra.readJsonSync("model.gltf");
const options = {
  dracoOptions: {
    compressionLevel: 10,
  },
};
processGltf(gltf, options).then(function (results) {
  fsExtra.writeJsonSync("model-draco.gltf", results.gltf);

```