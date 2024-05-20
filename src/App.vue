<script setup>
import { ref } from 'vue';

const newtodo=ref([
  {
    id:0,
    taskname:"code",
    taskDes:"this is earning money"
  },{
    id:1,
    taskname:"eating",
    taskDes:"this is gaining energy"
  },{
    id:2,
    taskname:"sleep",
    taskDes:"for getting some rest"
  }
]);
const dummy=ref(null);
const taskDes=ref(null);
const id=ref(3);

const showCase = ref(false);
const showEdit=ref(false);
const currentedit=ref(null);
  
  function handleButtonClick() {
    showCase.value = !showCase.value;
  }
  function handleditButton(index){
     showEdit.value=!showEdit.value;
     currentedit.value=index;
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
function taskdelete(id) {
  newtodo.value.splice(id, 1);
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
           <button @click="handleditButton(key)">edit</button>
        </div>
        </div>
        <div class="overlay" v-if="showCase">
        <div class="card">
          <input v-model="dummy" type="text" placeholder="task name" />
          <input v-model="taskDes" type="text"  placeholder="task Descripition"/>
          <button @click="newtaskadder" >add task</button>
          <button @click="handleButtonClick">Close</button>
        </div>
      </div>

      <div class="overlay" v-if="showEdit">
        <div class="card">
          <input v-model="dummy" type="text" placeholder="task name" />
          <input v-model="taskDes" type="text"  placeholder="task Descripition"/>
          <button @click="newtaskadder" >add task</button>
          <button @click="handleditButton">Close</button>
        </div>
      </div>
      
      <button @click="handleButtonClick" v-if="!showCase" class="taskBtn">Add new task</button>
         
         
    </main>
</template>

<style>
 .taskCard{
    width: 270px;
    height: 130px;
    border: 0.5px black solid;
    border-radius: 5px;
    padding: 10px;
    margin: 5px;
 }
 .taskBtn{
  margin:5px 0px 0px 10px;
 }
 .taskCard button{
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
  width: 400px;
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
}

.card input {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.card button {
  padding: 10px 20px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  margin-top: 10px;
}

.card button:last-child {
  background-color: #f44336;
}

.card button:hover {
  opacity: 0.8;
}
  .card-container{
    display: grid;
   grid-template-columns: 300px 300px 300px 300px;
   gap: 10px;
  }
  
</style>
