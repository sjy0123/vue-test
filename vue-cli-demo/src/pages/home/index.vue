<template> 
<div class="home-container">
  <mt-swipe :auto="4000">
      <mt-swipe-item v-for="(item, index) in banners" :key="index">
        <a :href="item.url">
          <img :src="item.img">
        </a>
      </mt-swipe-item>
    </mt-swipe>
  <div class="mui-content">
    <div class="mui-row">
        <div class="mui-col-sm-3 mui-col-xs-4">
            <li class="mui-table-view-cell">
                <router-link to="/home/newsList">
                 <img src="../../assets/menu1.png" alt="">
                 <div class="mui-media-body">新闻资讯</div>
                </router-link>
            </li>
        </div>
        <div class="mui-col-sm-3 mui-col-xs-4">
            <li class="mui-table-view-cell">
                <a >
                <img src="../../assets/menu2.png" alt="">
                 <div class="mui-media-body">新闻资讯</div>
                </a>
            </li>
        </div>
         <div class="mui-col-sm-3 mui-col-xs-4">
            <li class="mui-table-view-cell">
                <a>
                <img src="../../assets/menu3.png" alt="">
                 <div class="mui-media-body">新闻资讯</div>
                </a>
            </li>
        </div>
         <div class="mui-col-sm-3 mui-col-xs-4">
            <li class="mui-table-view-cell">
                <a>
                <img src="../../assets/menu4.png" alt="">
                 <div class="mui-media-body">新闻资讯</div>
                </a>
            </li>
        </div>
         <div class="mui-col-sm-3 mui-col-xs-4">
            <li class="mui-table-view-cell">
                <a>
                <img src="../../assets/menu5.png" alt="">
                 <div class="mui-media-body">新闻资讯</div>
                </a>
            </li>
        </div>
         <div class="mui-col-sm-3 mui-col-xs-4">
            <li class="mui-table-view-cell">
                <a>
                <img src="../../assets/menu6.png" alt="">
                 <div class="mui-media-body">新闻资讯</div>
                </a>
            </li>
        </div>
    </div>
</div>
</div>
</template>
<script>
export default {
   data(){
     return {
       banners:[]
     }
   },
   created() {
     this.getBanner()
   },
   methods: {
     getBanner(){
       this.$http.get("http://www.lovegf.cn:8899/api/getlunbo").then(result=>{
         this.banners = result.body.message
         console.log( result.body.message)
       })
     }
   },
}
</script>
<style lang="less" scoped>
.home-container{
  .mint-swipe{
     height:200px;
  .mint-swipe-item{
    img{
      width:100%;
      height:100%;
    }
  }
  }
  .mui-content{
    background-color: aliceblue;
    li{
      list-style: none;
      img{
        width:80%;
      }
      .mui-media-body{
        text-align: center;
        font-size: 13px;
      }
    }
  }
  
}
</style>