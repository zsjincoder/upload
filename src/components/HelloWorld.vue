<template>
  <div style="width: 800px; margin: 0px auto;">
    <el-tabs v-model="activeName2" type="card" @tab-click="handleClick">
      <el-tab-pane label="全景照片" name="first" >
        <picture-panorama></picture-panorama>
      </el-tab-pane>
      <el-tab-pane label="结构照片" name="second">
        <picture-structure></picture-structure>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
  import {uploadfile} from '@/api/api.js'
  import picturePanorama from './Picture-panorama.vue'
  import pictureStructure from './Picture-structure.vue'
export default {

  name: 'HelloWorld',
  data(){
    return {
      activeName2: 'first'
    }
  },
  components:{picturePanorama,pictureStructure},
  methods: {
    handleClick(tab, event) {

    },
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
