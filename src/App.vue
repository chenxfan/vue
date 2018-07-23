<template>


  <div id="app"> 
    <!-- 组件的挂载与使用 -->
  <v-life v-if="flag"></v-life>
  <button @click="flag=!flag">挂载和卸载life组件</button>
  <br>
  <br>
  <br>
  <br>
  <br>

    <v-home></v-home>
    <v-news></v-news>
<br>
<br>
<br>
<!-- 实现一个todolist -->
<h1 style="color:green">TOList</h1>
    <input type="text" v-model="todolist">

     <button @click="add()">+增加</button>
<br>
<br>


  <h2>进行中</h2>
     <li v-for="(item,key) in list" v-if="!item.checked">
      <input type="checkbox" v-model="item.checked" @change="saveList()"> {{item.title}}<button v-on:click="remove(key)">--删除</button>
     </li>

<br>
<br>

  <h2>已完成</h2>
     <li v-for="(item,key) in list" v-if="item.checked">
      <input type="checkbox" v-model="item.checked" @change="saveList()"> {{item.title}}<button v-on:click="remove(key)">--删除</button>
     </li>

  </div>
</template>

<script>

import storage from "./model/storage.js";
import Home from "./components/Home.vue";
import News from "./components/News.vue";
import Life from "./components/Life.vue";
    export default {     
      data () { 
        return {
          msg: '你好vue',
          todolist:"",
          list:[] ,
          flag:true  
        }
      },methods:{
        add(){
          this.list.push({
            title:this.todolist,
            checked:false
          });
          this.todolist="";
          storage.set("list",this.list);
        },
        remove(key){
          this.list.splice(key,1);
          storage.delete("list");
        },saveList(){
          storage.set("list",this.list);
        }
      },mounted(){
          /*生命周期函数       vue页面刷新就会触发的方法*/

          var list=storage.get('list');

          if(list){  /*注意判断*/
            this.list=list;
          }
      },components:{
        'v-home':Home,
        'v-news':News,
        'v-life':Life,
      }

    }
</script>


<style lang="scss">



</style>
