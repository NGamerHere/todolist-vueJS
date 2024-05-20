<script setup>
import { ref } from 'vue';

const newtodo=ref([]);
const dummy=ref(null);
const taskDes=ref(null);
const id=ref(0);

const showCase = ref(false);
  
  function handleButtonClick() {
    showCase.value = !showCase.value;
  }
  


function newtaskadder() {
    const newTask={
        id:id.value,
        taskname:dummy.value,
        taskDes:taskDes.value
    }
    newtodo.value.push(newTask);
    
    dummy.value="";
    taskDes.value="";
    id.value++;
    showCase.value = !showCase.value;
}
function taskdelete(id){
  alert(id);
}
</script>

<template>
    <main>
        <h1>todolist</h1>
        <div class="card-container">
          <div v-for="(items,key) in  newtodo" :key="key" class="taskCard">
            
            <h3>{{ items.taskname }}</h3>
            <p>{{ items.taskDes }}</p>
           <button @click="taskdelete(key)">delete</button>
        </div>
        </div>
        <div class="overlay" v-if="showCase">
        <div class="card">
          <input v-model="dummy" type="text" />
          <input v-model="taskDes" type="text" />
          <button @click="newtaskadder" >add task</button>
          <button @click="handleButtonClick">Close</button>
        </div>
      </div>
        <button @click="handleButtonClick" v-if="!showCase" class="taskBtn">Add new task</button>
         
         
    </main>
</template>

<style>
 .taskCard{
    width: 270px;
    height: 100px;
    border: 0.5px black solid;
    border-radius: 5px;
    padding: 10px;
    margin: 5px;
 }
 .taskBtn{
  margin:5px 0px 0px 10px;
 }
 .overlay {
    position: fixed;
    inset: 0;
    backdrop-filter: blur(5px); 
    z-index: 1000; 
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .card {
    width: 450px;
    height: 180px;
    border: 1px solid black;
    border-radius: 20px;
    background-color: white;
    padding: 20px;
  }
  
</style>
