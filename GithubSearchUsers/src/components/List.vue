<template>
    <div class="row">
        <div class="card" v-for="item,index in infoList" :key="index">
            <a :href="item.html_url" target="_blank">
                <img :src="item.avatar_url" style='width: 100px'/>
            </a>
            <p class="card-text">{{item.login}}</p>
        </div>
    </div>
</template>

<script>
    import PubSub from "pubsub-js"

    export default {
        name:"List",
        data() {
            return {
                infoList:[]
            }
        },
        methods: {
            
        },
        mounted() {
            this.$bus.$on("sendData",(data)=>{
                console.log("hahaha",data)
                this.infoList = data
            })
        },
    }
</script>

<style scoped>
    .album {
        min-height: 50rem; /* Can be removed; just added for demo purposes */
        padding-top: 3rem;
        padding-bottom: 3rem;
        background-color: #f7f7f7;
    }

    .card {
        float: left;
        width: 33.333%;
        padding: .75rem;
        margin-bottom: 2rem;
        border: 1px solid #efefef;
        text-align: center;
    }

    .card > img {
        margin-bottom: .75rem;
        border-radius: 100px;
    }

    .card-text {
        font-size: 85%;
    }
</style>