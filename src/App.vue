<template>
  <div id="app">
    <el-button @click="startHacking">Start</el-button>
    <li-core :config="config" :scope="scope"></li-core>
    <img src="./assets/logo.png">
  </div>
</template>

<script>
import LiCore from './components/LiCore';

export default {
  components:{LiCore},
  data(){
    return {
      scope:{
        $data:{
          tableData:[
            {username:"曾晓文", address:"上海市", phone: '15546182618'},
            // {username:"曾晓文", address:"上海市", phone: '15546182618'},
            // {username:"曾晓文", address:"上海市", phone: '15546182618'}
          ]
        }
      },
      config:[
        {
          type:"row",
          nodes:[
            {
              type:"input",
              style:"width:200px;padding:10px;float:right;",
              vmodel:"cir-firstname",
              span:12
            },
            {
              type:"input",
              style:"width:200px;padding:10px;float:left;",
              vmodel:"cir-lastname",
              span:12
            }
          ],
        },
        {
          type:"row",
          nodes:[
            {
              type:"input",
              style:"width:200px;padding:10px;float:right;",
              vmodel:"firstname",
              span:12
            },
            {
              type:"datepicker",
              style:"width:200px;padding:10px;float:left;",
              vmodel:"birthday",
              span:12
            }
          ]
        },
        {
          type:"row",
          nodes:[
            {
              type:"button",
              text:"我是一个按钮",
              style:"",
              click:"$context.tableData.push({username:'曾晓文', address:'上海市', phone: '15546182618'}); console.log('scope=' + JSON.stringify(scope));"
            }
          ]
        },
        {
          type:"table",
          vmodel:"tableData",
          style:"padding:10px;margin-left:20%;margin-right:20%;",
          selection:true,
          metadata:[
            {
              label:"姓名",
              value:"username",
              width:"200px"
            },
            {
              label:"地址",
              value:"address",
              width:"400px"
            },{
              label:"联系电话",
              value:"phone",
              width:"200px"
            }
          ]
        }
      ]
    }
  },
  methods: {
    startHacking() {
      this.$notify({
        title: 'It works!',
        type: 'success',
        message: 'We\'ve laid the ground work for you. It\'s time for you to build something epic!',
        duration: 5000
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, sans-serif;
  text-align: center;
}
</style>
