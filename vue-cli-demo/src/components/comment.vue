<template>
    <div class="comment-container">
        <h4>发表评论</h4>
        <hr>
       <textarea placeholder="请输入你要评论的内容" v-model="commentContent">

       </textarea>
       <mt-button type="primary" size="large" @click="postContent">发表评论</mt-button>
       <div class="cmt">
           <div  class="cmt-item" v-for="(item,i) in comments" :key="item.i">
               <div class="cmt-user">
            <span>第{{i+1}}楼</span>
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
import {Toast} from "mint-ui"
export default {
    data(){
        return{
           pageIndex: 1, 
            comments:[],
            commentContent:[]
        }
    },
    created() {
        this.getcomment()
    },
    // 获取评论数据
    methods: {
        getcomment(){
            this.$http.get("getcomments/" + this.id + '?pageindex=' + this.pageIndex).then(result=>{
                 this.comments= this.comments.concat(result.body.message)
                //  console.log(result.body.message)
            })
        },
        getmore(){
             this.pageIndex++
             this.getcomment()
        },
        postContent(){ 
            if(this.commentContent.trim().length===0){
                Toast("请输入数据")
            }
           this.$http.post("postcomment/" + this.id,{content:this.commentContent}).then(result=>{
              Toast('result.body.message')
               this.comments=[]      //清空之前的数据
               this.pageIndex=1      //将pageIndex重置为1 增加的数据会在第一页第一楼
               this.getcomment()     //重新发送请求 渲染数据
               this.commentContent=""  //清空输入的内容
           })
          
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