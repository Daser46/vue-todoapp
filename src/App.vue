<template>
<div class="wrapapp">
  <div class="appsize">
    <div class="header">
    <h1> TGSL TO-DO </h1>
    </div>
    <div class="inputarea">
      <input name="newTodo" v-model="newTodo" type="text" placeholder="Enter to-do here" autocomplete="off">
      <button class="btn" @click="addTodo()">Add</button>
    </div>
    <div class="listhead">
      To-Do List 
    </div>
    <div class=listarea>
      <ul style="list-style-type: none;">
      <li v-for="(item, index) in todos" 
      :key="index"
      >
      <span @click="item.status = !item.status, saveData();" 
      :class="{ status: item.status }">{{item.todo}}</span>
      <span class="span"><button class="btn" @click="removeTodo(index)">Remove</button></span></li>
      </ul>
    </div>
    <div class="footer">
    <h5>You have {{todos.length}} item(s) in the list  <button class="btn" @click="clearAll(index)">Clear All</button></h5>
    </div>
  </div>
</div>

  
   
 
</template>

<script>

import {ref} from 'vue';
export default {
  name: 'App',
  setup() {
    var newTodo=ref("");
    var defaultTodo = [{
      status: false,
      todo: 'Add new To Do'
    }]
    var Data = JSON.parse(localStorage.getItem('todos')) || defaultTodo;
    var todos = ref(Data);

    function addTodo(){
      if(newTodo.value){
      todos.value.push({
        status: false,
        todo: newTodo.value
      });
      saveData();
      }
      newTodo.value = '';
    }
    function removeTodo(index){
      todos.value.splice(index, 1);
      saveData();
    }
    function clearAll(index){
     todos.value.splice(index);
    saveData();
    }
    function saveData(){
      var storageData = JSON.stringify(todos.value);
      localStorage.setItem("todos", storageData);
    }
 
    return{
      newTodo,
      defaultTodo,
      todos,
      Data,
      addTodo,
      removeTodo,
      clearAll,
      saveData,
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
.wrapapp{
    display: flex;
    flex-wrap: space-around;
    align-content:space-around;
    justify-content: center;
    justify-items: center;
    align-items: center;

}
.appsize{
  width: 100%;
  max-width: 400px;
  
}
.header{
  background-color: cadetblue;
  border: 1px solid rgb(71, 224, 212);
  border-radius: 15px 15px 0 0;
}
.inputarea{
  background-color: whitesmoke;
  padding: 20px;
  align-items: space-between;
  margin-bottom:0px;
}
.inputarea input{
  display: inline-block;
  position: relative;
  height: 20px;
  width: auto;
  font-family: cursive;
  font-size: 13px;
  margin-bottom:0px;
}
.inputarea .btn{
  display: inline-block;
  position: relative;
  height: 26px;
  width: auto;
  background-color: rgb(77, 241, 140);
  justify-content: center;
  border: none;
  margin-left: 10px;
  color:#000000;
  border-radius: 5px;
  margin-bottom:0px;
}
.appsize .listhead{
  position: relative;
  margin-top:0px;
  border-bottom: 2px solid rgb(15, 28, 63);
  background-color: cadetblue;
  padding: 5px;
  height: 20px;
  align-items: center;
  justify-content: center;
  font-family: 'Courier New', Courier, monospace;
  color:white;
}
.appsize .listarea{
  display: flex;
  background-color: whitesmoke;
  margin-bottom:0px;
  padding: 5px;
  align-content: left; 
  max-height: 300px; 
  overflow-y: auto;
}
.appsize .listarea li{
  background-color: white;
  margin-left: 0px;
  width: 300px;
  overflow: hidden;
  padding: 10px;
  text-align: left;
  margin-bottom: 5px;
  position: relative;
  cursor: pointer;
  list-style: none;
}

.status{
  background-color: greenyellow; 
}
.appsize .listarea li .span{
  position: absolute;
  right:0px;
 }
 .appsize .listarea li span .btn{
   border: none;
   border-radius: 15px 0 0 15px;
   background-color: rgb(255, 0, 0);
   height: 20px;
   padding-top: 0px;
   margin: 0px;
   color: white;
 }
.footer{
  background-color: cadetblue;
  border: 1px solid rgb(71, 224, 212);
  border-radius: 0 0 15px 15px;
}
.footer .btn{
  background-color: violet;
  margin-left: 20px;
  border: none;
  padding: 5px;
  border-radius: 5px;
}

</style>
