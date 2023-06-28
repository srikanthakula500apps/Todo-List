
    <script>
    import {ref} from 'vue'
    export default {
      setup(){
        const newTodo=ref('')
        const todos=ref([])
    
        function addTodo(){
          if(newTodo.value){
            todos.value.push({text:newTodo.value});
            newTodo.value=('')
            saveTodos();

          }
        }
        function deletetodo(index){
          todos.value.splice(index, 1)
          saveTodos();

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
      localStorage.setItem('todos', JSON.stringify(todos));
    }

        return{
          newTodo,
          todos,
          addTodo,
          deletetodo,
          editTodo,
         updatedTodo
        }
      }
    }
    </script>

<template>
    <div>
    <input v-model="newTodo" placeholder="Enter a Todo"/>
    <button type='submit' @click="addTodo">Submit</button>
    <ul>
      <li v-for='(todo,index) in todos' :key='index'>
        {{todo.text}}
        <button @click="editTodo(todo)">Edit</button>
        <button @click="updatedTodo(todo)">Update</button>
        <button @click='deletetodo(index)'>Delete</button>
      </li>
    </ul>
      </div>
    </template>
    
    