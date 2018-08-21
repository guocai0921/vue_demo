<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <!--<TodoHeader @addTodo="addTodo"/>-->
      <todo-header ref="header"/>
      <TodoList :todos="todos" />
<!--
      <TodoFooter :todos="todos" :deleteCompleteTodos="deleteCompleteTodos" :selectAllTodos="selectAllTodos"/>
-->
      <todo-footer>
        <input type="checkbox" v-model="isAllCheck" slot="checkAll"/>
        <span slot="count">已完成{{completeSize}} / 全部{{todos.length}}</span>
        <button slot="delete" class="btn btn-danger" v-show="completeSize" @click="deleteCompleteTodos">清除已完成任务</button>
      </todo-footer>
    </div>
  </div>
</template>

<script>
  import storageUtil from './utils/storageUtil'
  import Pubsub from 'pubsub-js'
  import TodoList from './components/TodoList.vue'
  import TodoHeader from './components/TodoHeader.vue'
  import TodoFooter from './components/TodoFooter.vue'
  export default {
    data () {
      return {
        // 从localStorage读取todos
        //利用深度监视
        // todos : JSON.parse(window.localStorage.getItem('todos_key') || '[]')
        todos : storageUtil.readTodos()
      }
    },

    mounted () {  // 执行异步代码
      // 给<TodoHeader/>绑定addTodo事件监听
      //this.$on('addTodo',this.addTodo)
      this.$refs.header.$on('addTodo',this.addTodo)

      Pubsub.subscribe('deleteTodo',(msg,index) => {
        this.deleteTodo(index)
      })
    },

    computed: {
      completeSize() {
        return this.todos.reduce((preTotal,todo)=> preTotal+(todo.complete?1:0),0)
      },
      isAllCheck:{
        get(){
          return this.completeSize === this.todos.length && this.completeSize>0
        },
        set(value){
          this.selectAllTodos(value)
        }
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
        // handler: function (newValue){
        //   // 将todos的最新的值保存到localStorage
        //   storageUtil.saveTodos(newValue)
        // }
        handler: storageUtil.saveTodos
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
