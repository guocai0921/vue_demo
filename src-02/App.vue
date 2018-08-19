<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader :addTodo="addTodo"/>
      <TodoList :todos="todos" :deleteTodo="deleteTodo"/>
      <TodoFooter :todos="todos" :deleteCompleteTodos="deleteCompleteTodos" :selectAllTodos="selectAllTodos"/>
    </div>
  </div>
</template>

<script>
  import TodoList from './components/TodoList.vue'
  import TodoHeader from './components/TodoHeader.vue'
  import TodoFooter from './components/TodoFooter.vue'
  export default {
    data () {
      return {
        // 从localStorage读取todos
        //利用深度监视
        todos : JSON.parse(window.localStorage.getItem('todos_key') || '[]')
      }
    },
    methods:{
      addTodo (todo){
        this.todos.unshift(todo)
      },
      deleteTodo(index) {
        this.todos.splice(index,1)
      },
      //删除所有选中的todo
      deleteCompleteTodos(){
        this.todos = this.todos.filter(todo => !todo.complete)
      },
      //全选或全不选
      selectAllTodos(check){
        this.todos.forEach(todo => todo.complete = check)
      }

    },

    watch : { // 深度监视todos
      todos: {
        deep: true,//代表深度监视
        handler: function (newValue){
          // 将todos的最新的值保存到localStorage
          window.localStorage.setItem('todos_key',JSON.stringify(newValue))
        }
      }
    },

    components : {TodoList,TodoHeader,TodoFooter}
  }
</script>

<style>
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
