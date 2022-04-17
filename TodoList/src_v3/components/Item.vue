<template>
    <li>
        <label>
            <input type="checkbox" :checked="infoObj.done" @change="changeStatus(infoObj.id)"/>
            <span>{{infoObj.info}}</span>
        </label>
        <button class="btn btn-danger" @click="deleteInfo(infoObj.id)">删除</button>
    </li>
</template>

<script>
    export default {
        name:"Item",
        props:["infoObj"],
        methods: {
            // 是否勾选
            changeStatus(infoId){
                this.$bus.$emit("check",infoId)
            },
            // 删除当前项
            deleteInfo(infoId){
                if(confirm("确定删除嘛？")){
                    this.$bus.$emit("deleteItem",infoId)
                }
            }
        },
    }
</script>

<style>
/*item*/
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
  li:hover{
      background-color: #ddd;
  }
  li:hover button{
      display: block;
  }
</style>