<template>
   <div class="photoList-content">
  <div class="mui-scroll-wrapper mui-slider-indicator mui-segmented-control mui-segmented-control-inverted">
    <div class="mui-scroll">
        <a :class="['mui-control-item',{'mui-active':item.id==0}]" 
        v-for="item in  photolist" 
        :key="item.id"
        @click="getimglist(item.id)"
        >
           {{item.title}}
        </a>
       
    </div>
</div>
<div class="imglist">

</div>
</div>
</template>

<script>
import mui from '../../libs/mui/js/mui.min.js'
  mui('.mui-scroll-wrapper').scroll({
	deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
});
export default {
    data(){
        return{
            photolist:{},
            imglist:{}
        }
    },
    created() {
        this.getPhotolist()
        this.getimglist(0)
    },
    methods: {
        getPhotolist(){
            this.$http.get("getimgcategory").then(result=>{
                this.photolist=result.body.message
                this.photolist.unshift({
                    id:0,
                    title:"全部"
                })
                // console.log(result.body.message)
            })
        },
          getimglist(cateId){
            this.$http.get("getimages/"+cateId).then(result=>{
                this.imglist=result.body.message
                console.log(result.body.message)
            })
        }
    },
}
</script>

