<template>


  <div id="app">  
    <input type="text" v-model="todolist">

     <button @click="add()">+增加</button>
<br>
<br>


  <h2>进行中</h2>
     <li v-for="(item,key) in list" v-if="!item.checked">
      <input type="checkbox" v-model="item.checked"> {{item.title}}<button v-on:click="remove(key)">--删除</button>
     </li>

<br>
<br>

  <h2>已完成</h2>
     <li v-for="(item,key) in list" v-if="item.checked">
      <input type="checkbox" v-model="item.checked"> {{item.title}}<button v-on:click="remove(key)">--删除</button>
     </li>

  </div>
</template>

<script>



    export default {     
      data () { 
        return {
          msg: '你好vue',
          todolist:"",
          list:[]    
        }
      },methods:{
        add(){
          this.list.push({
            title:this.todolist,
            checked:false
          });
          this.todolist="";
        },
        remove(key){
          this.list.splice(key,1)
        },
      }

    }
</script>


<style lang="scss">



</style>
