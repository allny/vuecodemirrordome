<template>
  <div class="codeMirror clearfix">
    <div class="codeMirror-editor">
      <div class="codeMirror-editor-button">
        <button @click="run">运行</button>
        <span>html+javascript+css</span>
      </div>
      <codemirror class="codeMirror-editor-codeData" v-model="codeData" :options="cmOptions"></codemirror>
    </div>
    <div class="codeMirror-iframe">
      <iframe id="iframe" class="codeMirror-iframe-web" ref="iframe" name="result" allow="midi *; geolocation *; microphone *; camera *; encrypted-media *;" sandbox="allow-modals allow-forms allow-scripts allow-same-origin allow-popups allow-top-navigation-by-user-activation" allowfullscreen="" allowpaymentrequest="" frameborder="0" src=""></iframe>
    </div>
  </div>
</template>

<script>
  import { codemirror } from 'vue-codemirror'
  // require styles
  import 'codemirror/lib/codemirror.css'

  // language js
  import 'codemirror/mode/javascript/javascript.js'

  // theme css
  import 'codemirror/theme/monokai.css'
  export default {
    name: 'Editor',
    props: ['code'],
    components: {
      codemirror
    },
    data () {
      return {
        codeData:"",
        cmOptions: {
          // codemirror options
          tabSize: 4,
          mode: 'text/javascript',
          theme: 'monokai',
          lineNumbers: true,
          line: true,
        }
      }
    },
    mounted() {
      this.codeData='<style>\n' +
        '  \n' +
        '  @import url("//unpkg.com/element-ui@2.0.11/lib/theme-chalk/index.css");\n' +
        '.el-row {\n' +
        '    margin-bottom: 20px;\n' +
        '    &:last-child {\n' +
        '      margin-bottom: 0;\n' +
        '    }\n' +
        '  }\n' +
        '  .el-col {\n' +
        '    border-radius: 4px;\n' +
        '  }\n' +
        '  .bg-purple-dark {\n' +
        '    background: #99a9bf;\n' +
        '  }\n' +
        '  .bg-purple {\n' +
        '    background: #d3dce6;\n' +
        '  }\n' +
        '  .bg-purple-light {\n' +
        '    background: #e5e9f2;\n' +
        '  }\n' +
        '  .grid-content {\n' +
        '    border-radius: 4px;\n' +
        '    min-height: 36px;\n' +
        '  }\n' +
        '  .row-bg {\n' +
        '    padding: 10px 0;\n' +
        '    background-color: #f9fafc;\n' +
        '  }\n' +
        '\n' +
        '  </style>\n' +
        '<script src="//unpkg.com/vue/dist/vue.js"></'+'script>\n'+
'<script src="//unpkg.com/element-ui@2.0.11/lib/index.js"></'+'script>\n'+
        '<div id="app">\n'+
  '<el-row>\n'+
    '<el-col :span="24">' +
        '<div class="grid-content bg-purple-dark"></div>' +
     '</el-col>\n'+
    '</el-row>\n'+
  '<el-row>\n'+
    '<el-col :span="12"> ' +
      '<div class="grid-content bg-purple"></div> ' +
    '</el-col>\n'+
  '<el-col :span="12">' +
      '<div class="grid-content bg-purple-light"></div>' +
  '</el-col>\n'+
    '</el-row>\n'+
  '<el-row>\n'+
    '<el-col :span="8">' +
        '<div class="grid-content bg-purple"></div>' +
    '</el-col>\n' +
  '<el-col :span="8">' +
        '<div class="grid-content bg-purple-light"></div>' +
   '</el-col>\n' +
   '<el-col :span="8"> ' +
        '<div class="grid-content bg-purple"></div>' +
        '</el-col>\n'+
   '</el-row>\n'+
      '<el-row>\n'+
    '<el-col :span="6">' +
        '<div class="grid-content bg-purple"></div>' +
        '</el-col>\n'+
    '<el-col :span="6">' +
        '<div class="grid-content bg-purple-light"></div>' +
    '</el-col>\n'+
    '<el-col :span="6"> ' +
        '<div class="grid-content bg-purple"></div>' +
        '</el-col>\n'+
    '<el-col :span="6"> ' +
        '<div class="grid-content bg-purple-light"></div> ' +
        '</el-col>\n'+
        '</el-row>\n'+ '<el-row>\n'+
    '<el-col :span="4"> ' +
        '<div class="grid-content bg-purple"></div> ' +
        '</el-col>\n'+
    '<el-col :span="4">' +
        '<div class="grid-content bg-purple-light"></div> ' +
        '</el-col>\n'+
        '<el-col :span="4"> ' +
        '<div class="grid-content bg-purple"></div>' +
        '</el-col>\n'+
        ' <el-col :span="4">' +
        '<div class="grid-content bg-purple-light"></div> ' +
        '</el-col>\n'+
    '<el-col :span="4"> ' +
        '<div class="grid-content bg-purple"></div> ' +
        '</el-col>\n'+
    '<el-col :span="4">' +
        '<div class="grid-content bg-purple-light"></div>' +
        '</el-col>\n'+
    '</el-row>\n'+
        ' </div>\n'
        + '<script>\n'+ 'new Vue().$mount(\'#app\')\n' + '</'+'script>'
    },
    methods:{
      run(){
        this.$nextTick(()=>{
          let iframe=this.$refs.iframe;
          let doc=null;
          if(iframe.contentWindow){
            doc=iframe.contentWindow.document;
          }else{
            doc=iframe.document;
          }
          var babel="<script src='"+"https://cdn.bootcss.com/babel-polyfill/7.4.4/polyfill.js'>"+"</"+"script>";
          var result = '<html><head>' + babel + '</head><body>' + this.codeData + '</body></html>';
          doc.open();
          doc.writeln(result);
          doc.close();
        })
      }
    }
  }
</script>

<style scoped>
  /*这里是清除浮动的*/
  .clearfix:after {
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
  }
  .clearfix {
    *zoom: 1;
  }
  .codeMirror{
    text-align: left;
  }
  .codeMirror-editor{
    width: 50%;
    float: left;
  }
  .codeMirror-iframe{
    width: 49%;
    float: left;
    border: 1px solid #2c3e50;
    height: 340px;
  }
  .codeMirror-editor-button{
    background: #2c3e50;
    padding: 10px;
    color: #ffffff;
  }
  .codeMirror-editor-button button{
    background: #42b983;
    border: 1px solid #42b983;
    border-radius: 2px;
  }
  .codeMirror-iframe-web{
    width: 100%;
    height: 100%;
  }
</style>
