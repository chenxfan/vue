<template>
  <div>
    <!-- <v-head></v-head> -->
    <h2>{{msg}}</h2>
    <br>
    <button @click="getdata()">使用fetchJsonp请求数据</button>
    <ul>
      <li v-for="item in list">{{item.title}}</li>
    </ul>
  </div>
</template>
<script>
import Head from "./Head.vue";
import fetchJsonp from "fetch-jsonp"
export default {

  // fetch-jsonp方式请求数据
  data() {
    return {
      msg: "我是一个新闻组件",
      list: []
    }
  },
  components: {
    'v-head': Head,
  },
  methods: {
    getdata() {
      var url = 'http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1';
      fetchJsonp(url).then((response) => {
        return response.json();

      }).then((json)=> {
        console.log('parsed json', json)
        this.list = json.result;
      }).catch((ex) => {
        console.log(ex)
      })
    }
  },
  mounted() {
    this.getdata();
  }
}

</script>
