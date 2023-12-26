<template>
  <div>
    <div ref="container"></div>
    <!-- <button @click="changeCameraPosition">Change Camera Position</button> -->
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch ,defineProps } from 'vue';
import * as THREE from 'three';
import TWEEN from 'tween.js';
import { FBXLoader } from 'three/addons/loaders/FBXLoader';
import { RGBELoader } from 'three/addons/loaders/RGBELoader';
// 在导入的地方添加以下导入语句
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';

const container = ref<HTMLDivElement | null>(null);
let scene: THREE.Scene;
let camera: THREE.PerspectiveCamera;
let renderer: THREE.WebGLRenderer;
let ambientLight: THREE.AmbientLight;
let dirLight: THREE.DirectionalLight;
let controls: OrbitControls;
let model;
// 定义属性，接收父组件传递的方法
const parents = defineProps(['parentMethod','cameraList']);

const timer = ref<any>(null)

// const cameraList = [
//   {name:"X射线衍射仪",cameraPosition:{x:"11.20",y:"11.59",z:"-32.99"},cameraRotation:{x:"-1.55",y:"-0.62",z:"-1.55"}},
//   {name:"高频疲劳材料试验机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
//   {name:"高温拉伸设备",cameraPosition:{x:"13.96",y:"4.66",z:"-21.76"},cameraRotation:{x:"-2.57",y:"-0.13",z:"-3.05"}},
//   {name:"电子拉伸材料试验机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
//   {name:"注塑机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
//   // {name:"电子拉伸材料试验机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
//   // {name:"电子拉伸材料试验机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
//   // {name:"电子拉伸材料试验机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
// ]

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

  console.log(parents.cameraList)
  // 定时更新相机位置和朝向
  let currentIndex = 0;
  const updateCamera = () => {
    const targetPosition = new THREE.Vector3(
      parseFloat(parents.cameraList[currentIndex].cameraPosition.x),
      parseFloat(parents.cameraList[currentIndex].cameraPosition.y),
      parseFloat(parents.cameraList[currentIndex].cameraPosition.z)
    );
    const targetRotation = new THREE.Euler(
      parseFloat(parents.cameraList[currentIndex].cameraRotation.x),
      parseFloat(parents.cameraList[currentIndex].cameraRotation.y),
      parseFloat(parents.cameraList[currentIndex].cameraRotation.z)
    );

    new TWEEN.Tween(camera.position)
      .to(targetPosition, 1000)
      .start();

    // 使用回调函数手动更新相机的rotation属性
    new TWEEN.Tween({})
      .to({}, 1000)
      .onUpdate(() => {
        // 在Tween完成时触发change事件，传递当前的index值
        
      })
      .onComplete(() => {
        camera.rotation.copy(targetRotation);
      })
      .start();
    if (parents.parentMethod) {
      parents.parentMethod(currentIndex);
    }
    currentIndex = (currentIndex + 1) % parents.cameraList.length;
  };
  if(timer.value){
    clearInterval(timer.value)
  }
  timer.value = setInterval(updateCamera, 5000); // 每5秒钟更新一次相机位置和朝向
});


// 创建场景
const initScene = () => {
  scene = new THREE.Scene();
  // 使用 RGBELoader 加载HDR纹理
  const rgbeLoader = new RGBELoader();
  // const hdrTexture = rgbeLoader.load('img/015.hdr', (texture) => {
  const hdrTexture = rgbeLoader.load('img/017.hdr', (texture) => {
    // 处理加载完成后的回调
    texture.mapping = THREE.EquirectangularReflectionMapping;
    scene.background = texture;
    scene.environment = texture; // 设置环境纹理
  });
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
  const target = new THREE.Vector3(0, 10, 0);
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  camera.position.set(30, 30, 30);
  camera.lookAt(target);
}

// 创建灯光
const initLight = () => {
  // ambientLight = new THREE.AmbientLight(0xffffff, 1); // 颜色、强度
  // scene.add(ambientLight);

  dirLight = new THREE.DirectionalLight(0xffffff, 3);
  dirLight.position.set(5, 5, 5); // 设置光照方向
  dirLight.castShadow = true; 
  scene.add(dirLight);
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

  // console.log("位置")
  // console.log(cameraPosition)
  // console.log("朝向")
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
  controls.enablePan = true;

  // 如果需要阻止用户在旋转和缩放过程中触发点击事件，可以设置以下属性
  controls.enableDamping = true;
  controls.dampingFactor = 0.25;
};


</script>
