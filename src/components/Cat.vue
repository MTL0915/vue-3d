<template>
  <div></div>
</template>

<script>
  import * as Three from 'three'
  import OrbitControls from 'three-orbitcontrols'
  import {OBJLoader} from 'three-obj-mtl-loader'
  export default {
    name:"Cat",
    data () {
      return {
        // 相机
        camera: null,
        // 场景
        scene: null,
        // 渲染器对象
        renderer: null,
        // 材质对象
        mesh: null,
        controls:null,
      }
    },
    methods: {
      // 初始化
      init () {
        // 相机位置
        let width=window.innerWidth;
        let height=window.innerHeight;
         // 创建场景
        this.scene = new Three.Scene();
        let k = width/height;
        let s = 100;
        this.camera = new Three.OrthographicCamera(-s*k,s*k,s,-s,1,1000);
        this.camera.position.set(200, 200, 120);
        this.camera.lookAt(new Three.Vector3(1, 80, 0));
        this.scene.add(this.camera);
        // 创建点光源
        let light=new Three.DirectionalLight(0xffaaff);
        light.position.set(80,100,50);
        this.scene.add(light);
        let light2=new Three.DirectionalLight(0xffaaff);
        light2.position.set(-80,-100,-50);
        this.scene.add(light2);
        //环境光
        var ambient = new Three.AmbientLight(0x444444);
        this.scene.add(ambient);
        // 创建渲染器
        this.renderer = new Three.WebGLRenderer({antialias: true})
        this.renderer.setSize(width, height)
        document.body.appendChild(this.renderer.domElement);
        // 创建控件对象
        this.controls=new OrbitControls(this.camera,this.renderer.domElement);
        this.controls.addEventListener('change',this.animate);
      },
      // 创建obj模型
      loadObj () {
        let that=this;
        let objloader=new OBJLoader();
        objloader.load('/static/cat.obj',function(obj){
          that.mesh=obj;
          that.scene.add(that.mesh);
          that.animate();
        })
      },
      // 创建动画
      animate () {
        this.renderer.render(this.scene, this.camera)
      },
    },
    mounted () {
      this.init();
      this.loadObj();
    }
  }
</script>
<style scoped>
  #container {
    height: 700px;
  }
  #three{
    height:700px;
  }
</style>