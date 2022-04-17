<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader @add="add"></MyHeader>
        <List :todoArray="todoArray"></List>
        <MyFooter :todoArray="todoArray" @SelectAllInfo="SelectAllInfo" @clearDone="clearDone"></MyFooter>
      </div>
    </div>
  </div>
</template>

<script>
  import MyHeader from './components/MyHeader.vue'
  import List from './components/List.vue'
  import MyFooter from './components/MyFooter.vue'

  export default {
    name: 'App',
    data(){
      return {
        todoArray:JSON.parse(localStorage.getItem("todoArray")) || []
      }      
    },
    components: {
      MyHeader,
      List,
      MyFooter
    },
    methods: {
      // 增加数据
      add(data){
        this.todoArray.unshift(data)
        console.log(data)
      },
      // 是否勾选
      check(id){
        this.todoArray.forEach((todoObj)=>{
          if(todoObj.id===id) todoObj.done = !todoObj.done
        })
      },
      // 删除数据
      deleteItem(id){
        this.todoArray = this.todoArray.filter((todoObj)=>{
          return todoObj.id != id
        })
      },
      // 是否全选数据
      SelectAllInfo(selectBool){
        this.todoArray.forEach(todoObj => todoObj.done = (selectBool ? false:true))
      },
      // 删除已完成列表项
      clearDone(){
        this.todoArray = this.todoArray.filter(todoObj => {
          return !todoObj.done
        })
      }
    },
    watch:{
        todoArray:{
          deep:true,
          handler(value){
            localStorage.setItem("todoArray",JSON.stringify(value))
          }
        }
    },
    mounted(){
      this.$bus.$on("check",this.check)
      this.$bus.$on("deleteItem",this.deleteItem)
    },
    beforeDestroy(){
      this.$bus.$off(["check","deleteItem"])
    }
  }
</script>

<style>
  /*base*/
  body {
    background: #fff;
  }

  .btn {
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

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
