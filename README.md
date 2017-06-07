# vue2.0-Ueditor
在vue2.0中集成百度编辑器的方法

  **例子使用jsp版本**
 1. [下载](/build/build_down.php?n=ueditor&v=1_4_3_3-utf8-jsp)UEditor源码到根目录中如vue项目static中.
 2. 修改ueditor.config.js
 
        var URL = '/static/utf8-php/' || getUEBasePath();
  
 3. 3.创建vueUeditor.vue组件放入components目录中
 4. 使用方法

  <template>
 
      <div>
    
        <!--下面通过传递进来的id完成初始化-->
     
        <script :id="randomId"  type="text/plain"></ script> 
       
      </div> 
     
  </template>

    < script >
   
      //需要修改  ueditor.config.js 的路径

     //var URL = window.UEDITOR_HOME_URL || ‘/static/ueditor_1/‘;
 
     //主体文件引入 
     import  ‘../../static/ueditor/ueditor.config.js‘  
 
     import  ‘../../static/ueditor/ueditor.all.min.js‘
 
     import ‘../../static/ueditor/lang/zh-cn/zh-cn.js‘ 
 
   
    export default {
 
    props: {
 
    //配置可以传递进来
 
    ueditorConfig:{}
  
    },
  
     data () {
   
      return { 
 
      //每个编辑器生成不同的id,以防止冲突
 
      randomId: ‘editor_‘ + (Math.random() * 100000000000000000),
 
      //编辑器实例
 
     instance: null, 
 
            };
 
         },
 
      //此时--el挂载到实例上去了,可以初始化对应的编辑器了
  
    mounted () { 
 
      this.initEditor()
 
    },
 
     beforeDestroy () { 
  
     // 组件销毁的时候，要销毁 UEditor 实例
 
      if (this.instance !== null && this.instance.destroy) {

      this.instance.destroy();
 
     }

    },

      methods: {

     initEditor () {
 
      //dom元素已经挂载上去了

     this.$nextTick(() => {
 
     this.instance = UE.getEditor(this.randomId,this.ueditorConfig); 
  
    this.instance.addListener(‘ready‘, () => {
  

         });
      });
     }
    }
    };
    </script >

 

    

    
