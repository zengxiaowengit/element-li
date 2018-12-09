<template>
  <div name="li-circlable">
    <li-core :config="config" v-if="config" :scope="scope"></li-core>
  </div>
</template>

<script>
import LiCore from './LiCore';

export default {
  name:"li-circle",//循环引用的元素必须有name
  components:{LiCore},
  data(){
    return {
    }
  },
  props:['config','scope'],
  methods: {

  },
  beforeCreate: function () {
    //组件循环引用，需要先注册。
    this.$options.components.LiCore = require('./Licore.vue').default
  }
}
</script>

