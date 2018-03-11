<template>
  <div>
    <ul>
      <li class="list-item" v-for="(item,index) in SlideData" :data-type="0">
        <div class="list-box" @touchstart.capture="touchStart" @touchend.capture="touchEnd" @click="ins">
          <div class="list-img">
          <img :src="item.imgUrl">
          </div>
          <div class="list-content">
            <p class="title">{{item.title}}</p>
            <p class="tips">{{item.tips}}</p>
            <p class="time">{{item.time}}</p>
          </div>
        </div>
        <div class="delete"  :data-index="index">删除</div>
      </li>
    </ul>
  </div>
</template>
<script>
  import SlideData from './info'
    export default {
      data(){
          return {
            SlideData:[],
            start:0,
            end:0,
          }
      },
      created(){
        this.getData();
      },
      methods:{
        getData(){
          this.SlideData = SlideData;
        },
        ins(){
          console.log(this.isSlide());
          if(this.isSlide()){//如果当前处于滑动状态，更新所有状态变成原始状态
            this.upDate();
            return
          }
        },
        touchStart(e){
          this.start = e.touches[0].clientX;

        },
        touchEnd(e){
          let ParentEle = e.currentTarget.parentElement;
          this.end = e.changedTouches[0].clientX;
          if(ParentEle.dataset.type === '0' && this.start - this.end > 30){
              this.upDate();
              ParentEle.dataset.type = '1';
          }else if(ParentEle.dataset.type === '1' && this.start - this.end < 30){
            this.upDate();
            ParentEle.dataset.type = '0';
          }
        },
        upDate(){
          let oli = document.querySelectorAll('.list-item');
          oli.forEach((item)=>{
             item.dataset.type = '0';
             return true;
          })
        },
        isSlide(){
          let oli = document.querySelectorAll('.list-item');
          for(var i=0;i<oli.length;i++){
            if(oli[i].dataset.type == '1'){
              return true
            }
          }
          return false;
        },
      },
  }

</script>
<style scoped>
 ul,li{list-style:none;}
 .list-item{
   position: relative;
   height: 1.6rem;
   -webkit-transition: all 0.2s;
   transition: all 0.2s;
 }
 .list-item[data-type="0"]{
   transform: translate3d(0,0,0);
 }
 .list-item[data-type="1"]{
   transform: translate3d(-2.1rem,0,0);
 }
 .list-item{
   border-bottom: 1px solid #ddd;
   transform: scaleY(0.8)
 }
 .list-box{
   padding: 0.2rem;
   background: #fff;
   display: flex;
   align-items: center;
   -webkit-box-sizing: border-box;
   box-sizing: border-box;
   justify-content: flex-end;
   position: absolute;
   top: 0;
   right: 0;
   bottom: 0;
   left: 0;
   font-size: 0;
 }
 .list-item .list-img{
     display: block;
     width: 1.2rem;
     height: 1rem;
   }
 .list-item .list-img img{
      width:100%;
 }
 .list-item .list-content{
   padding: 0.1rem 0 0.1rem 0.2rem;
   position: relative;
   flex: 1;
   flex-direction: column;
   align-items: flex-start;
   justify-content: center;
   overflow: hidden;
 }
 .list-item .title{
   display: block;
   color: #333;
   overflow: hidden;
   font-size: 15px;
   font-weight: bold;
   text-overflow: ellipsis;
   white-space: nowrap;
 }
 .list-item .tips{
   display: block;
   overflow: hidden;
   font-size: 12px;
   color: #999;
   line-height: 20px;
   text-overflow: ellipsis;
   white-space: nowrap;
 }
 .list-item .time{
   display: block;
   font-size: 12px;
   position: absolute;
   right: 0;
   top: 0.1rem;
   color: #666;
 }
 .list-item .delete{
   width: 2rem;
   height: 1.6rem;
   background: #ff4949;
   font-size: 17px;
   color: #fff;
   text-align: center;
   line-height: 1.6rem;
   position: absolute;
   top:0;
   right: -2.1rem;
 }
</style>
