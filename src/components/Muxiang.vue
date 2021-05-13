<template>
  <div id="muxiang"></div>
</template>

<script>
import * as Three from "three";
import OrbitControls from "three-orbitcontrols";
import { OBJLoader,MTLLoader} from "three-obj-mtl-loader";

export default {
  name: "Muxiang",
  data() {
    return {
      // 相机
      camera: null,
      // 场景
      scene: null,
      // 渲染器对象
      renderer: null,
      // 材质对象
      mesh: null,
      controls: null,
    };
  },
  methods: {
    // 初始化
    init() {
      // 相机位置
      let width = window.innerWidth;
      let height = window.innerHeight;
      // 创建场景
      this.scene = new Three.Scene();
      let k = width / height;
      let s = 500;
      this.camera = new Three.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);
      this.camera.position.set(200, 200, 120);
      this.camera.lookAt(new Three.Vector3(1, 80, 0));
      this.scene.add(this.camera);
      // 创建点光源
      let light = new Three.DirectionalLight(0xffffff);
      light.position.set(80, 100, 50);
      this.scene.add(light);
      let light2 = new Three.DirectionalLight(0xffffff);
      light2.position.set(-80, -100, -50);
      this.scene.add(light2);
      //环境光
      var ambient = new Three.AmbientLight(0xffffff);
      this.scene.add(ambient);
      // 创建渲染器
      this.renderer = new Three.WebGLRenderer({ antialias: true, alpha: true });
      this.renderer.setClearAlpha(0);
      this.renderer.setSize(width, height);
      // this.renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
      document.getElementById("muxiang").appendChild(this.renderer.domElement);
      // 创建控件对象
      this.controls = new OrbitControls(this.camera, this.renderer.domElement);
      this.controls.addEventListener("change", this.animate);

    },
    // 创建obj模型
    loadObjMtl() {
        let that=this;
        let objloader=new OBJLoader();
        let mtlloader=new MTLLoader();
        // objloader.load('/static/caizhi.obj',function(obj){
        //   that.mesh=obj;
        //   that.scene.add(that.mesh);
        //   that.animate();
        // })

        mtlloader.load('/static/feichuan.mtl', function(materials) {
          // 返回一个包含材质的对象MaterialCreator
          console.log(materials);
          //obj的模型会和MaterialCreator包含的材质对应起来
          objloader.setMaterials(materials);
          objloader.load('/static/feichuan.obj', function(obj) {
            console.log(obj);
            that.mesh=obj;
            that.scene.add(that.mesh);
            that.animate();
          })
        })
    },


    // 创建动画
    animate() {
      this.renderer.render(this.scene, this.camera);
    },
  },
  mounted() {
    this.init();
    this.loadObjMtl();
  },
};
</script>

<style>

#muxiang{
    color: #000;
    font-family: Monospace;
    font-size: 13px;
    text-align: center;
    font-weight: bold;
    background: url(/static/bg-qc.jpg) no-repeat;
    background-size: 100%;
    margin: 0px;
    overflow: hidden;
    width:100%;
    height:100%;
}
</style>
