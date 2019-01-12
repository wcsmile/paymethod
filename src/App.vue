<template>
  <div id="app">
    <pay-method :payMethodList="payMethodList" @payWayId ="payWayId"></pay-method>
  </div>
</template>

<script>
import payMethod from './pay/payMethod.vue'; // 引入模板
import dataList from './payMethodList'; // 引入数据
export default {
  name: 'app',
  components: {
    payMethod
  },
  data () {
    return {
      payMethodList: dataList
    }
  },
  methods:{
    payWayId:function(id){   // 组件返回的id 
      console.log(id);
    },
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  position: absolute;
  right: 0;
  left: 0;
  height: 100%;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
