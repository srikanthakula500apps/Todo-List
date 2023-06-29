 <script>
    import {ref, onMounted} from 'vue'
    import Cookie from "./Cookie.vue"
    export default {
      setup(){
  
        const newTodo=ref('')
        const todos=ref([])
        const sessionData=ref([])       
        
    onMounted(() => {
      sessionStorage.clear()
      sessionData.value=([])
    })
  
    const storedTodos = localStorage.getItem('local');
        if (storedTodos) {
          todos.value = JSON.parse(storedTodos);
        }

        const sessionTodo = sessionStorage.getItem('session');
        if (sessionTodo) {
          sessionData.value = JSON.parse(sessionTodo);
        }

                                        
        function addTodo(){
          if(newTodo.value){
            todos.value.push({text:newTodo.value});
            newTodo.value=('')
            saveTodos();
            // saveTodosData()
          }
        }
        function deletetodo(index){
          const removeLocal=todos.value.splice(index, 1);
          removeLocal.forEach((item)=>{
            sessionData.value.push(item)
          })
            
          saveTodos();
          sessionStorage.setItem('session', JSON.stringify(sessionData.value));
        }
        function editTodo(todo){
            newTodo.value=todo.text
            saveTodos();
        }
        function updatedTodo(todo){
            todo.text=newTodo.value
            newTodo.value=('')
            saveTodos();
        }
        function saveTodos() {
      // Save todos to local storage    
      localStorage.setItem('local', JSON.stringify(todos.value));
    }

    function markAsCompleted(index) {
    // todo.completed=true;
    const removeLocal=todos.value.splice(index, 1);
          removeLocal.forEach((item)=>{
            sessionData.value.push(item)
          })
          saveTodos();
          sessionStorage.setItem('session', JSON.stringify(sessionData.value));

  }
  

        return{
          newTodo,
          todos,
          addTodo,
          deletetodo,
          editTodo,
         updatedTodo,
         saveTodos,
         markAsCompleted,
         sessionData
        //  isDarkTheme,
    
        }
      }
    }
    </script>

<template class="space-y-[5px]">
  <center>
    <div>
    <input v-model="newTodo" placeholder="Enter a Todo"/>
    <button type='submit' @click="addTodo" class="bg-green-500 text-white py-2 px-4 mt-2">Submit</button>
    <div class="space-y-[5px]">
    <ul>
      <li v-for='(todo,index) in todos' :key='index' class="mb-2">
        <input type="checkbox" @change="markAsCompleted(index)">
        {{todo.text}}
        <button @click="editTodo(todo)" class="bg-blue-500 text-white py-2 px-4 ml-2">Edit</button>
        <button @click="updatedTodo(todo)" class="bg-blue-500 text-white py-2 px-4 ml-2">Update</button>
        <button @click='deletetodo(index)' class="bg-blue-500 text-white py-2 px-4 ml-2">Delete</button>
      </li>
    </ul>
    <div>
      <div v-if="sessionData.length"><h2>Session Storage Data</h2></div>
<div v-for="item in sessionData" :key="item">
  <div><p>{{ item.text }}</p>
</div>
</div>
    </div>
    </div>
      </div>
      <Cookie/>
      </center>

    </template>
    

   
    