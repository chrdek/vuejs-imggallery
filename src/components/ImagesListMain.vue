<template>
<div id="img__el" class="images">
<h2>{{heading}}</h2> 
<stack :column-min-width="320" :gutter-width="10" :gutter-height="10" monitor-images-loaded>
 <stack-item class="imgclass" v-for="(item,i) in items" :key="i">
   <a :id="imglink__el" @click="openImg(`${item.download_url}`)" class="tooltip" title="Click for preview">
      <img :class="imgid__el" :src="`${item.download_url}`" :width="170" :height="170" alt="Unavailable"/>
   </a>
    <div>ID: {{item.id}}</div> <div class="imgName--part">Author: {{item.author}}</div>
 </stack-item>
</stack>
<PagingListLayout v-on:clicked="setItems" title="Paging (max items per page = 100)" description=" - @page number: "/>
</div>
</template>

<script>
import {StackItem, Stack} from 'vue-stack-grid';
import PagingListLayout from './PagingListLayout.vue';

 export default {
    name: 'ImagesListMain',
    props: {
        heading: String
    },
    components:{StackItem, Stack, PagingListLayout},
    data() {
 return {
    imglink__el:'',
    imgid__el:'',
    items:[]
  }
 },
 methods: {
      setItems(result) {
         this.$data.items = result;
      },
           openImg(url) {
            let win = window.open(url);
            win.onload = function(){alert("opened link "+url);}
            }
          }
}
</script>

<style scoped>
#img__grid{
display:grid;
grid-template-columns:49px 49px 49px 49px 49px 49px;
grid-template-rows:49px 49px 49px 49px 49px 49px;
}

#img__el > div > div:nth-child(n) > a > img {
   transition:300ms;
   -webkit-transform: scale(1);
	transform: scale(1);
	-webkit-transition: .3s ease-in-out;
	transition: .3s ease-in-out;
   opacity:1;
   border-radius:15px;
}

#img__el > div > div:nth-child(n) > a > img:hover {
   transition:300ms;
   -webkit-transform: scale(1.05);
	transform: scale(1.05);
   background-color:#000;
   opacity:0.4;
   border-radius:55px;
}

.images{ opacity:0.5; }

.imgName--part {
   display:block;
   text-overflow:ellipsis;
}

.tooltip {
  display: inline;
  position: relative;
}

.tooltip:hover:after{
  display: -webkit-flex;
  display: flex;
  -webkit-justify-content: center;
  justify-content: center;
  background: #444;
  border-radius: 8px;
  color: #fff;
  content: attr(title);
  margin: -82px auto 0;
  font-size: 16px;
  padding: 13px;
  width: 220px;
}

#imglink__el { display:block; }
#img__el { 
   background-color:#50dca0;
   border-radius:30px;
   opacity:0.87;
   }

h2, li {
font-family:'Calibri';
text-align:center;
font-size: 50px;
color:#4e5c07;
}

#filt__el {
 display:block;
 border-radius:15px;
 border-style:none;
}
</style>