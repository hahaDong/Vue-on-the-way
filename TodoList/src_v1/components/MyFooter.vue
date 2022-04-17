<template>
    <div class="todo-footer" v-show="total > 0">
        <label>
            <input type="checkbox" :checked="isAllChecked" @click="SelectAll"/>
        </label>
        <span>
            <span>已完成{{CountDone}}</span> / 全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div>
</template>

<script>
    export default {
        name:"MyFooter",
        props:["todoArray","SelectAllInfo","clearDone"],
        computed:{
            total(){
                return this.todoArray.length
            },
            CountDone(){
                return this.todoArray.reduce((prev,cur) => {
                    return prev + (cur.done ? 1 : 0)
                },0)
            },
            isAllChecked(){
                return this.total === this.CountDone
            }
        },
        methods: {
            // 全选或全不选
            SelectAll(){
                /**
                 * this.isAllChecked值为true，表示列表项已经全部被勾选，此时应该全不选
                 */
                console.log(this.isAllChecked)
                this.SelectAllInfo(this.isAllChecked)
            },
            // 清除已完成数据
            clearAll(){
                if(this.CountDone == 0){
                    alert("没有已完成事项！")
                    return
                }
                if(confirm("确认删除已完成的事项嘛？")){
                    // 通知App.vue删除已经完成的数据
                    this.clearDone()
                }
            }
        },
    }
</script>

<style>
/*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>