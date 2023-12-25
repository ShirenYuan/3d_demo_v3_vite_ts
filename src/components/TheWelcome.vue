<template>
  <div>
    <div ref="container"></div>
    <!-- <button @click="changeCameraPosition">Change Camera Position</button> -->
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from 'vue';
import * as THREE from 'three';
import TWEEN from 'tween.js';
import { FBXLoader } from 'three/addons/loaders/FBXLoader';
// 在导入的地方添加以下导入语句
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';

const container = ref<HTMLDivElement | null>(null);
let scene: THREE.Scene;
let camera: THREE.PerspectiveCamera;
let renderer: THREE.WebGLRenderer;
let ambientLight: THREE.AmbientLight;
let controls: OrbitControls;
let model;

watch(container, () => {
  // 处理容器大小变化
  if (container.value) {
    camera.aspect = container.value.clientWidth / container.value.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(container.value.clientWidth, container.value.clientHeight);
  }
});

onMounted(() => {
  // 创建场景
  initScene();
  // 加载文件
  // loadFBXModel('3Dfile/11.FBX');
  // loadFBXModel('3Dfile/22.FBX');
  loadFBXModel('3Dfile/33.FBX');
  // 创建相机
  initCamera();
  // 创建灯光
  initLight();
  // 创建辅助线
  addHelpers();
  // 创建渲染
  initRenderer();
  // 创建动画
  animate();
  // 创建手势
  initControls();
});

const changeCameraPosition = () => {
  console.log("切换镜头")
  console.log(camera)
  // 点击按钮时改变相机的位置，加入 Tween.js 动画
  if (camera) {
    const currentPosition = { x: camera.position.x, y: camera.position.y, z: camera.position.z };
    const targetPosition = { x: 50, y: 50, z: 50 };

    new TWEEN.Tween(currentPosition)
      .to(targetPosition, 1000) // 1000毫秒（1秒）的动画时间
      .easing(TWEEN.Easing.Quadratic.Out) // 缓动函数，可以根据需要选择
      .onUpdate(() => {
        camera!.position.set(currentPosition.x, currentPosition.y, currentPosition.z);
      })
      .start();
  }
}


// 创建场景
const initScene = () => {
  scene = new THREE.Scene();
  // 设置场景背景色为白色
  // scene.background = new THREE.Color(0xffffff);
  // const textureLoader = new THREE.TextureLoader();
  // const texture = textureLoader.load('img/015.png'); // 替换为你的图片路径
  // scene.background = texture;

 // 使用 TextureLoader 加载图片
  const textureLoader = new THREE.TextureLoader();
  const texture = textureLoader.load('img/015.png'); // 替换为你的图片路径

  // 调整纹理的minFilter，确保在小尺寸下保持清晰
  texture.minFilter = THREE.LinearFilter;

  // 调整纹理的wrapS和wrapT，确保在整个场景中正确重复
  texture.wrapS = THREE.RepeatWrapping;
  texture.wrapT = THREE.RepeatWrapping;

  // 设置纹理的重复方式，以确保图片完全展示在整个场景中
  texture.repeat.set(1, 1);

  // 设置背景为加载的纹理
  scene.background = texture;
};

// 加载FBX模型
const loadFBXModel = (modelPath: string) => {
  const loader = new FBXLoader();
  loader.load(modelPath, (fbx) => {
    model = fbx
    // 旋转模型
    // fbx.rotation.x = Math.PI / 2; // 90 度
    fbx.rotation.x = Math.PI / 2; // 90 度
    fbx.rotation.y = Math.PI ; // 90 度
    fbx.rotation.z = Math.PI / 2; // 90 度
    // 设置模型的缩放属性
    fbx.scale.set(0.001, 0.001, 0.001);
    // 设置模型的位置
    fbx.position.set(0, 0, 0);

    // 将模型添加到场景中
    scene.add(fbx);
  });
};

// 创建相机
const initCamera = () => {
  // THREE.PerspectiveCamera(fov: number, aspect: number, near: number, far: number)

  // fov (Field of View):
  // 类型: number
  // 描述: 视场角，指的是相机可见区域的垂直范围，单位是度（degrees）。
  // 典型值: 通常设置在 45 到 75 度之间，视场角越大，可见区域越广。

  // aspect:
  // 类型: number
  // 描述: 屏幕宽度和高度的比值，即视口的宽高比。
  // 计算方式: aspect = width / height，其中 width 是屏幕宽度，height 是屏幕高度。
  // 典型值: 设置为视口宽高比，以保持画面不变形。

  // near:
  // 类型: number
  // 描述: 相机到视景体近端的距离。
  // 典型值: 通常设置一个正数，代表相机到近端的距离，不能为负数。

  // far:
  // 类型: number
  // 描述: 相机到视景体远端的距离。
  // 典型值: 通常设置为正数，表示相机到远端的距离，必须大于 near。

  const target = new THREE.Vector3(0, 10, 0);
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  camera.position.set(30,30,30);
  camera.lookAt(target);
}

// 创建灯光
const initLight = () => {
  ambientLight = new THREE.AmbientLight(0xffffff, 1); // 颜色、强度
  scene.add(ambientLight);

  // const hesLight = new THREE.HemisphereLight(0xffffff,0x444444)
  // hesLight.intensity = 0.6
  // scene.add(hesLight)

  // const dirLight = new THREE.DirectionalLight()
  // dirLight.position.set(5,5,5)
  // scene.add(dirLight)
}

// 添加坐标轴辅助/网格辅助
const addHelpers = () => {
  // 添加坐标轴辅助
  const axesHelper = new THREE.AxesHelper(5);
  scene.add(axesHelper);

  // 添加网格辅助
  const gridHelper = new THREE.GridHelper(10, 10);
  scene.add(gridHelper);
};

const initRenderer = () =>{
  // 创建渲染器
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(window.innerWidth, window.innerHeight);

  // 将渲染器的DOM元素添加到容器中
  container.value?.appendChild(renderer.domElement);
}

const animate = () => {
  // 更新动画逻辑
  requestAnimationFrame(animate);
  // 更新 Tween.js
  TWEEN.update();
  // 记录相机的位置和朝向
  const cameraPosition = camera.position.clone();
  const cameraRotation = camera.rotation.clone();

  // console.log(cameraPosition)
  // console.log(cameraRotation)

  // 沿 Y 轴旋转
  // if (model) {
  //   model.rotation.z += 0.01; // 调整旋转速度
  // }
  
  // 渲染场景
  renderer.render(scene, camera);
};

const initControls = () => {
 // 创建OrbitControls
 controls = new OrbitControls(camera, renderer.domElement);

  // 启用旋转和缩放
  controls.enableRotate = true;
  controls.enableZoom = true;

  // 禁用平移
  controls.enablePan = false;

  // 如果需要阻止用户在旋转和缩放过程中触发点击事件，可以设置以下属性
  controls.enableDamping = true;
  controls.dampingFactor = 0.25;
};


</script>
