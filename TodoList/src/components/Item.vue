<template>
    <transition 
      name="animate__animated animate__bounce"
      appear
      enter-active-class="animate__backInUp"
      leave-active-class="animate__backOutUp"
    >
        <li>
          <label>
              <input type="checkbox" :checked="infoObj.done" @change="changeStatus(infoObj.id)"/>
              <span v-show="!infoObj.isEdit">{{infoObj.info}}</span>
              <input 
                type="text" 
                v-show="infoObj.isEdit" 
                @blur="handleBlur($event)" 
                :value="infoObj.info"
                ref="inputTitle"
              >
          </label>
          <button class="btn btn-danger" @click="deleteInfo(infoObj.id)">删除</button>
          <button v-show="!infoObj.isEdit" class="btn btn-edit" @click="handleEdit(infoObj)">编辑</button>
      </li>
    </transition>
</template>

<script>
    import PubSub from "pubsub-js"
    import "animate.css"
    export default {
        name:"Item",
        props:["infoObj","todoArray"],
        methods: {
            // 是否勾选
            changeStatus(infoId){
                PubSub.publish("check",infoId)
            },
            // 删除当前项
            deleteInfo(infoId){
                if(confirm("确定删除嘛？")){
                  PubSub.publish("deleteItem",infoId)
                }
            },
            handleEdit(infoObj){
              if(infoObj.hasOwnProperty("isEdit")){
                infoObj.isEdit = true
              }else{
                this.$set(infoObj,"isEdit",true)
              }
              this.$nextTick(function(){
                this.$refs.inputTitle.focus()
              })
            },
            handleBlur(event){
              if(!event.target.value.trim()) return alert("请重新输入值～")  
              const itemArray = [] 
              this.todoArray.filter(item => {
                  itemArray.push(item.info)
              })
              if(itemArray.includes(event.target.value)){
                console.log("yes")
                event.target.value = ""
                return alert("已添加过该事项，请重新添加～")
              }
              this.infoObj.isEdit = false
              this.$bus.$emit("updateItem",this.infoObj.id,event.target.value)
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