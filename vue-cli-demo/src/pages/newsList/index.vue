<template>
    <div class="newsList-container">
     
<ul class="mui-table-view">
    <li class="mui-table-view-cell mui-media" v-for="item in list" :key="item.id">
        <router-link :to="'/home/newsInfo/' + item.id">
            <img class="mui-media-object mui-pull-left" :src="item.img_url">
            <div class="mui-media-body">
                <p class='mui-ellipsis title'>{{item.title}}</p>
               <span class='mui-ellipsis time'> 发表时间：{{item.add_time|dateFormat  }}</span>
                <span class='mui-ellipsis time'> 点击：{{item.click}}次</span>
            </div>
        </router-link>
    </li>
</ul>
    </div>
</template>
<script>
export default {
    data(){
        return{
            list:[]
        }

        
    },
    created() {
        this.getList()
    },
    methods: {
        getList(){
            this.$http.get("http://www.lovegf.cn:8899/api/getnewslist").then(result=>{
                this.list = result.body.message
                console.log(result.body.message)
            })
        }
    },
}
</script>
<style scoped>
   .title{
        color: black;

   }
   .time{
       font-size: 10px;
       color:blue;
   }

</style>
