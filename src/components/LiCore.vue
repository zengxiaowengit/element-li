<template>
  <div id="li-core-component">
    <div v-for="(item, index) in config" ref="refLiCore" :key="index">

        <el-row :style="item.style"
          v-if="item.type=='row'"
          :class="item.class">
          <li-circlable :style="item.style" v-if="item.nodes" :config="item.nodes" :scope="scope"></li-circlable>
        </el-row>

        <el-col :style="item.style"
          v-else-if="item.type=='col'"
          :class="item.class"
          :span="item.span">
          <li-circlable :style="item.style" v-if="item.nodes" :config="item.nodes" :scope="scope"></li-circlable>
        </el-col>

        <!--为基本组件默认加一列。方便布局。简化json结构  -->
        <el-col :span="item.span == null?24:item.span" v-else>
          <el-date-picker
            v-if="item.type == 'datepicker'" 
            v-model="scope.$data[item.vmodel]"
            :style="item.style" :class="item.class"
            type="date"
            placeholder="选择日期">
          </el-date-picker>

          <el-input v-if="item.type == 'input'" 
            v-model="scope.$data[item.vmodel]"
            :class="item.class" 
            :style="item.style">
          </el-input>

          <el-button
            v-if="item.type == 'button'"
            @click="OnClick(item.click)"
            :class="item.class"
            :style="item.style">
            {{item.text}}
            </el-button>

          <el-table
            v-if="item.type == 'table'"
            :data="scope.$data[item.vmodel]" 
            :style="item.style" 
            :stripe="item.stripe==null?true:item.stripe"
            :border="item.border==null?true:item.border">
            <el-table-column
              v-if="item.selection == true"
              type="selection"
              width="55">
            </el-table-column>

            <el-table-column v-for="(item, index) in item.metadata" :key="index"
              :label="item.label"
              :prop="item.value"
              :width="item.width"
              show-overflow-tooltip>
            </el-table-column>
          </el-table>
        </el-col>
        

    </div>
  </div>
</template>

<script>
import LiCirclable from './LiCirclable';

export default {
  name:"li-core",
  props:['config','scope'],
  components:{LiCirclable},
  data(){
    return {
    }
  },
  methods: {
    OnClick(code){
      let scope = this.scope;
      let $context = this.scope.$data;
      eval(code);
    }
  },
  beforeCreate: function () {
    //组件循环引用，需要先注册。
    this.$options.components.LiCirclable = require('./LiCirclable.vue').default
  }
}
</script>

<style>
#core-component {
  font-family: Helvetica, sans-serif;
  text-align: center;
}
</style>
