<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div>
      <el-button @click="startHacking">Start</el-button>
      <el-col v-for="(item, index) in config">
        <el-col :style="item.style" v-model="modules[0].params[item.vmodel]" v-if="item.type=='col'">

        </el-col>
        <el-date-picker :style="item.style" v-model="modules[0].params[item.vmodel]" :exp="item.index= index"
           type="date" v-if="item.type == 'datepicker'" placeholder="选择日期">
        </el-date-picker>
        <el-input :exp="item.index= index" :style="item.style" v-if="item.type == 'input'" 
        v-model="modules[0].params[item.vmodel]"></el-input>
        <el-button :exp="item.index= index" :style="item.style" v-if="item.type == 'button'" @click="OnClick(item.click)">{{item.text}}</el-button>
      </el-col>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      modules:[
        {
          params:{}
        }
      ],
      config:[
        {
          type:"col",
          style:"",
          nodes:[
            {
              type:"input",
              style:"width:10%;margin:5px;",
              vmodel:"firstname"
            },
            {
              type:"input",
              style:"width:10%;margin:5px;",
              vmodel:"lastname"
            }
          ],
        },
        {
          type:"input",
          style:"width:10%;margin:5px;",
          vmodel:"firstname"
        },
        {
          type:"input",
          style:"width:10%;margin:5px;",
          vmodel:"lastname"
        },
        {
          type:"datepicker",
          style:"margin:10px",
          vmodel:"birthday"
        },
        {
          type:"button",
          text:"我是一个按钮",
          style:"left:20px",
          click:"console.log('params=' + JSON.stringify(params))"
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
    },
    OnClick(item){
      let params = this.params;
      console.log(item);
      eval(item);

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
