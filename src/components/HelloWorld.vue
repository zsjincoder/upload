<template>
  <div style="width: 800px; margin: 0px auto;">
    <el-tabs v-model="activeName2" type="card" @tab-click="handleClick">
      <el-tab-pane label="全景照片" name="first" >
        <span style="font-size: 16px; text-decoration-style: -moz-none">照片上传:</span>
        <Upload
          :before-upload="handleUpload"
          multiple
          :name="image"
          :headers="headers"
          action="//192.168.0.102/img/public/img_upload/">
          <Button  icon="ios-cloud-upload-outline">选择文件</Button>
        </Upload>
        <div v-if="file !== null"  style="display: inline">
          <div style="display: inline" v-for="(f,index) in file" :key="index">
            文件名: {{ f.name }}
            <a href="javascript:;"  @click="delectFile(index)">X</a></div>
          <Button  @click="upload" :loading="loadingStatus">{{ loadingStatus ? 'Uploading' : '点击上传' }}</Button>
        </div>
        <div>
          <div class="imgBody" v-for="(imagelist,index) in showFile" :key="imagelist.name">
            <a href="javascript:;" class="delImg"  @click="delectlistFile(index)">X</a>
            <div class="showImg">
              <img :src="imagelist.url" alt="" width="100%" height="100%">
            </div>
          </div>
        </div>
      </el-tab-pane>
      <el-tab-pane label="结构照片" name="second">结构照片</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
  import {uploadfile} from '@/api/api.js'
export default {

  name: 'HelloWorld',
  data(){
    return {
      file:null,
      showFile:[
        {
          'name': 'a42bdcc1178e62b4694c830f028db5c0',
          'url': 'https://o5wwk8baw.qnssl.com/a42bdcc1178e62b4694c830f028db5c0/avatar'
        },
        {
          'name': 'bc7521e033abdd1e92222d733590f104',
          'url': 'https://o5wwk8baw.qnssl.com/bc7521e033abdd1e92222d733590f104/avatar'
        }
      ],
      image:'image',
      headers: {'Content-Type': 'multipart/form-data'},
      loadingStatus: false,
      activeName2: 'first'
    }
  },
  methods: {
    handleUpload (file1) {
      if(file1!=null){
        if(this.file==null){
          this.file=[];
        }
        // 选择文件后 这里判断文件类型 保存文件 自定义一个keyid 值 方便后面删除操作
        let keyID = Math.random().toString().substr(2);
        file1['keyID'] = keyID;
        // 保存文件到总展示文件数据里
        this.file.push(file1);
        // 保存文件到需要上传的文件数组里
        return false;
      }
    },
    handleClick(tab, event) {

    },
    delectFile(index){
      // 删除需要上传文件数据里的当前文件
      this.file.splice(index,1);
      if(this.file.length==0){
        this.file=null
      }
    },
    delectlistFile(index){
      this.showFile.splice(index,1);
    },
    upload () {
      this.loadingStatus = true;
      let file=this.file;
      const param = new FormData() // 创建form对象
      for(let i=0;i<file.length;i++){
        param.append('image', file[i], file.name) // 通过append向form对象添加数据
      }
       console.log(param.getAll('image')) // FormData私有类对象，访问不到，可以通过get判断值是否传进去
      this.$http.post('http://192.168.0.102/img/public/img_upload', param)
        .then(response => {
          if(response.code==200){
            this.file=null;
            this.loadingStatus = false;
            this.$Message.success('Success')
          }else{
            this.loadingStatus = false;
            this.$Message.error('upload fail');
          }
        })
    }
  }
}
</script>

<style >
  .ivu-upload-list{
    display: inline;
  }
  .ivu-upload{
    display: inline;
  }
.tab1{
  display: inline;
}
  .imgBody{
    position: relative;
    width: 350px;
    height: 300px;
    float: left;
    margin: 30px 5px;
  }
  .delImg{
    position: absolute;
    right: 5px;
    top:5px;
  }
</style>
