<template>
  <div id="asd">
    <h2>头部组件</h2>
    <button @click="getData()">使用axios请求数据</button>
    <ul>
      <li v-for="item in list">{{item.title}}</li>
    </ul>
  </div>
</template>
<script>
/*

请求数据的模板

    axios  的使用

    1、安装  cnpm  install  axios --save


    2、哪里用哪里引入axios

    
*/
import Axios from 'axios';

export default {
  data() {
    return {
      list: []
    }
  },
  methods: {

    getData() {

      var api = 'http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1';
      Axios.get(api).then((response) => {
      	console.log(response)
        this.list = response.data.result;
      }).catch((error) => {
        console.log(error);

      })

    }
  },
  mounted() { /*生命周期函数*/

    this.getData();

  }


}

</script>
<style lang="scss" scoped>
h2 {
  color: blue
}


/*	#asd{
		background: #000;
		color: red;
	}*/

</style>
