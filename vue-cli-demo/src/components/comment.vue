<template>
    <div class="comment-container">
        <h4>发表评论</h4>
        <hr>
       <textarea placeholder="请输入你要评论的内容">

       </textarea>
       <mt-button type="primary" size="large">发表评论</mt-button>
       <div class="cmt">
           <div  class="cmt-item" v-for=" item in comments" :key="item.add_time">
               <div class="cmt-user">
            <span>第i+1楼</span>
            <span>用户:{{item.user_name}}</span>
            <span>时间:{{item.add_time|dateFormat}}</span>
             </div>
            <div class="cmt-content">{{item.content}}</div>
           </div>
       </div>
       <mt-button type="danger" size="large" @click="getmore" plain>加载更多</mt-button>
     </div>
</template>
<script>
export default {
    data(){
        return{
           pageIndex: 1, 
            comments:[]
        }
    },
    created() {
        this.getcomment()
    },
    // 获取评论数据
    methods: {
        getcomment(){
            this.$http.get("getcomments/" + this.id + '?pageindex=' + this.pageIndex).then(result=>{
                 this.comments= result.body.message
                 console.log(result.body.message)
            })
        },
        getmore(){
             this.pageIndex++
             this.getcomment()
        }
    },
    props: ['id']
}
</script>
<style lang="less" scoped>
      textarea{
        margin:0;
        height:80px;
        font-size:14px;
    }
    .cmt{
        margin:5px 0;
          font-size:13px;
        .cmt-user{
            background-color: #ccc;
          
            line-height:30px
        }
        .cmt-content{
          line-height: 35px;
          text-indent: 2em;
          
        }
    }
    
</style>