<template>
    <div class="todo-header">
        <input 
            type="text" 
            placeholder="请输入你的任务名称，按回车键确认" 
            v-model="inputValue" 
            @keyup.enter="AddInfo"/>
    </div>
</template>

<script>
    import {nanoid} from "nanoid"
    export default {
        name:"MyHeader",
        props:["todoArray"],
        data(){
            return {
                inputValue:''
            }
        },
        methods: {
            AddInfo(){
                const itemName = []
                if (!this.inputValue) return alert("请输入有效值～")
                this.todoArray.filter(item=>{
                    itemName.push(item.info)
                })
                if(itemName.includes(this.inputValue)){
                    this.inputValue = ""
                    return alert("您已添加过该事项，请重新添加～")
                }
                const infoObj = {
                    id:nanoid(),
                    info:this.inputValue,
                    done:false
                }
                this.$emit("add",infoObj)
                this.inputValue = ''
            }
        },
    }
</script>

<style>
    /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>