# vue2.0-Ueditor
在vue2.0中集成百度编辑器的方法

  **例子使用jsp版本**
 1. [下载](/build/build_down.php?n=ueditor&v=1_4_3_3-utf8-jsp)UEditor源码到根目录中如vue项目static中.
 2. 修改ueditor.config.js
 
        var URL = '/static/utf8-php/' || getUEBasePath();
  
 3. 3.创建vueUeditor.vue组件放入components目录中
 4. 使用方法(创建百度编辑器组件)

  <template>
 
      <div>
    
        <!--下面通过传递进来的id完成初始化-->
     
        <div ref="editor"></div>
       
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
 
      value: {
           type: String,
          default: null,
      },
       config: {
        type: Object,
        default: {},
      }
  
    },
  
      data () {
   
      return { 
 
       //每个编辑器生成不同的id,以防止冲突
           id: ‘editor_‘ + (Math.random() * 100000000000000000),
 
       //编辑器实例
 
      instance: null, 
 
            };
 
         },
 
      //此时--el挂载到实例上去了,可以初始化对应的编辑器了
      watch: {
      value: function value(val, oldVal) {
      
        this.editor = UE.getEditor(this.id, this.config);
        
        if (val !== null) {
        
          this.editor.setContent(val);
          
        }
      }
     },
  
      mounted () { 
 
       this.initEditor()
 
    },
 
      methods: {

     initEditor () {
 
      //dom元素已经挂载上去了

     this.$nextTick(() => {
     
          this.instance = UE.getEditor(this.id, this.config);
          
            // 绑定事件，当 UEditor 初始化完成后，将编辑器实例通过自定义的 ready 事件交出去
            
            this.instance.addListener('ready', () => {
            
              this.$emit('ready', this.instance);
              
            });
            
              this.editor.addListener("contentChange", ()=> {
              
                  const wordCount = this.editor.getContentLength(true);
                  
                  const content = this.editor.getContent();
                  
                  const plainTxt = this.editor.getPlainTxt();
                  
                  this.$emit('input', {wordCount: wordCount, content: content, plainTxt: plainTxt});
                  
              });
      });
     }
    }
    };
    </script >

 

    

    
