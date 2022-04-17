<template>
    <ul class="todo-main">
        <Item 
            v-for="infoObj in todoArray" 
            :key="infoObj.id" 
            :infoObj="infoObj"
        /> 
    </ul>
</template>

<script>
    import Item from "./Item.vue"
    export default {
        name:"List",
        props:["todoArray"],
        components:{
            Item
        }
    }
</script>

<style>
    /*main*/
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }
</style>