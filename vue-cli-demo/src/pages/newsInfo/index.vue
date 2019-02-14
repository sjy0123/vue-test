<template>
    <div class="newInfo-container" >
         <h3>{{list.title}}</h3>
         <p class="time">
             <span>发表时间：{{list.add_time|dateFormat}}</span>
             <span class="click">点击：{{list.click}}次</span>
         </p>
         <hr>
         <div  class="content" v-html="list.content"> </div>
        <comment :id="id"></comment>
        
    </div>
    
</template>
<script>
export default {
    data(){
        return {
            id:this.$route.params.id,
            list:{}
        }
    },
    created() {
        this.getDate()
    },
    methods: {
        getDate(){
            this.$http.get("http://www.lovegf.cn:8899/api/getnew/"+this.id).then(result=>{
                this.list=result.body.message[0]
                // console.log(result.body.message[0])
            })

        }
    },
}
</script>
<style lang="less" scoped>
    .newInfo-container{
        h3{
            font-size: 16px;
            color:red;
            text-align: center;
            margin:10px 5px ;
            
        }
        .time{
            font-size: 13px;
            color:blue;
        }
        .click{
            float: right;
        }
    }
</style>
