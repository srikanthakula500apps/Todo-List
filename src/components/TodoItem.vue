 <script>
    import {ref} from 'vue'
    export default {
      setup(){
        const newTodo=ref('')
        const todos=ref([])


    //     getData() {
    // // Retrieve the data from local storage
    // const todo = localStorage.getItem('myData')
    //     }

    
        function addTodo(){
          if(newTodo.value){
            todos.value.push({text:newTodo.value});
            newTodo.value=('')
            saveTodos();
            // saveTodosData()

          }
        }
        function deletetodo(index){
          todos.value.splice(index, 1)
          saveTodos();
          // saveTodosData()
        }
        function editTodo(todo){
            newTodo.value=todo.text
            saveTodos();
            // saveTodosData()
        }
        function updatedTodo(todo){
            todo.text=newTodo.value
            newTodo.value=('')
            saveTodos();
            // saveTodosData()
        }
        function saveTodos() {
      // Save todos to local storage
      // todo.completed=false;
      localStorage.setItem('local', JSON.stringify(todos.value));
    }

    function markAsCompleted(todo) {
    todo.completed=true;
     // Update the completed property of the todo item
    sessionStorage.setItem('session', JSON.stringify(todos.value)); // Store the updated todos in session storage
    
  }
    // function saveTodosData() {
    //   sessionStorage.setItem('todos', JSON.stringify(todos.value));
    // }

        return{
          newTodo,
          todos,
          addTodo,
          deletetodo,
          editTodo,
         updatedTodo,
         saveTodos,
         markAsCompleted
        //  saveTodosData
        }
      }
    }
    </script>

<template class="space-y-[5px]">
  <center>
    <div>
    <input v-model="newTodo" placeholder="Enter a Todo" />
    <button type='submit' @click="addTodo" class="bg-green-500 text-white py-2 px-4 mt-2">Submit</button>
    <div class="space-y-[5px]">
    <ul>
      <li v-for='(todo,index) in todos' :key='index' class="mb-2">
        <input type="checkbox" v-model="todo.completed" @change="markAsCompleted(todo)">
        {{todo.text}}
        <button @click="editTodo(todo)" class="bg-blue-500 text-white py-2 px-4 ml-2">Edit</button>
        <button @click="updatedTodo(todo)" class="bg-blue-500 text-white py-2 px-4 ml-2">Update</button>
        <button @click='deletetodo(index)' class="bg-blue-500 text-white py-2 px-4 ml-2">Delete</button>
      </li>
    </ul>
    </div>
      </div>
      </center>
    </template>
    