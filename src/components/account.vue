<template>
    <div class="box">
        <indexHeader></indexHeader>
        <div class="account flex">
            <left v-bind:lang="lang" :current="0"></left>
            <router-view></router-view>
        </div>
    </div>
</template>
<script>
	import indexHeader from '@/view/indexHeader'
	import left from '@/view/left'
    export default {
        name:'account',
        data(){
            return {
                lang:''
            }
        },
        components:{
            indexHeader,
            left,
        },
        // mounted(){
        //     this.bus.$on('nav_name',cur=>{
        //         this.array.findIndex()
        //     })
        // }
    }
</script>
<style scoped >
    .box{
        /* background-color: #273041; */
    }
    .box .account{
        width: 1200px;
        padding-top: 30px;
        min-height: 880px;
        margin: 0 auto;
        overflow: hidden;
    }
   
</style>


