<template>
    <section class="jumbotron">
        <h3 class="jumbotron-heading">Search Github Users</h3>
        <div>
            <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
            <button @click="getInfo">Search</button>
        </div>
    </section>
</template>

<script>   
    
    export default {
        name:"Search",
        data(){
            return {
                keyWord:""
            }
        },
        methods: {
            getInfo(){
                if(!this.keyWord.trim()) return alert("请输入有效值～")
                this.$bus.$emit("sendData",{isFirst:false,isLoading:true,errMsg:'',infoList:[]})
                this.$http.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
                    response => {
                        this.$bus.$emit("sendData",{isLoading:false,errMsg:'',infoList:response.data.items})
                    },
                    error => {
                        this.$bus.$emit("sendData",{isLoading:false,errMsg:error.message,infoList:[]})
                    }
                )
                this.keyWord = ""
            }
        },
    }
</script>

<style>

</style>