<template>
<div id="numpages__el" class="page--list">
    <div>{{title}} {{description}}
     <span class="current--page-sel">{{currentPage}}</span>
     <span class="current--page edge-noround">{{currentTimePerf().label}} {{currentTimePerf().time}}</span>
     <span class="current--page edge-noround">{{currentDuration.durationlabel}} {{currentDuration.durationtimer}}</span>
     <DropDownInput v-on:LimitChange="setPageConfig" class="current--page edge-noround"/>
    </div>
    <div v-for="page in pageRange" v-bind:key="page">
        <a @click.prevent="retrieveInfo(page,currentLimit)" class="page--link">{{page}}</a>
    </div>
</div>
</template>

<script>
import axios from 'axios';
import DropDownInput from './DropDownInput.vue';

export default {
    name:'PagingListLayout',
    props: {
        title: String,
        description: String,
        currentPage: String,
        currentLimit: Number,
        currentTimePerf:{
            type:Function,
            default:() => {
                return { label: 'Elapsed time (ms): ', time:(performance.now()).toFixed(4) };
            }
        },
        counterFn:{
            type:Function,
            default:() => {
            let time = setInterval(() => {
                          setTimeout(() => {
                            this.currentDuration.durationtimer = (new Date().getMilliseconds());
                               },1000)}
                                ,100);
                    return time;
            }
        },
        stopCounterFn: {
            type:Function,
            default:() => {
                for(var i=0; i < 9999; i++){clearInterval(i)}
            }
        }
    },
    components: {DropDownInput},
    data() {
        return{
            maxImages:1000,
            pageRange:[],
            currentDuration:{ durationlabel:'Paging request time (ms): ', durationtimer:0 }
        }
    },
    async created() {
     this.currentDuration.durationtimer = this.counterFn();
     const [initPage,initLimit] = ["1","10"];
     this.currentLimit = initLimit;
        await axios.get(`https://picsum.photos/v2/list?page=${initPage}&limit=${initLimit}`).then(response => {
                this.$emit('clicked',response.data);
                this.stopCounterFn();
        })
            this.$data.pageRange = this.calcPage(initLimit);
            this.currentPage = initPage;
            
    },
    mounted() {
      this.$data.pageRange = this.calcPage(this.currentLimit);
    },
    methods:{
        setPageConfig(pageCfg){
            this.currentLimit = pageCfg.target.value;
        },
        calcPage(pagelim) {
            let imgsTot = [];
            for(var i=1; i<=Math.floor(this.$data.maxImages/pagelim);i++) {
                imgsTot.push(i);
            }
            return imgsTot;
        },
      async retrieveInfo(pageNum,pageLimit) {
       this.currentDuration.durationtimer = this.counterFn();
       this.$data.pageRange = this.calcPage(pageLimit);
        await axios({
                method:'get',
                timeout:5000,
                url:`https://picsum.photos/v2/list?page=${pageNum}&limit=${pageLimit}`,
                response:'json'
            }).then(response => {
                this.$emit('clicked',response.data);
                this.stopCounterFn();
            })
                
                this.currentPage = pageNum;
        }
    }
}
</script>

<style scoped>
span.current--page-sel {
    display:inline-block;
    background-color:#c72239;
    border-radius:50%;
    border:0px solid #ddd;
    color:#fff;
}
span.current--page {
    display: inline-block;
    background-color: aquamarine;
    border-radius: 50%;
    transition: .6s ease-in-out;
    -webkit-font-smoothing: antialiased;
}
span.current--page.edge-noround {
    background-color:aquamarine;
    border-radius:.1px;
    padding-left:1rem;
}
div.page--list {
    display: inline-block;
    padding-left: 0;
    margin-top: 1rem;
    margin-bottom: 1rem;
}
a.page--link {
    position: relative;
    float: left;
    padding: .2rem .5rem;
    margin-left: -1px;
    color: #fff;
    text-decoration: none;
    background-color: #c72239;
    border: 0px solid #ddd;
    border-radius: 50%;
}
a.page--link:hover {
    background-color:#ddd;
}
a.page--link.active:focus {
    background-color:#ddd;
}
#numpages__el {
    text-align:center;
    display:block;
    background-color:#9cbb9c;
    border-bottom-left-radius: 30px;
    border-bottom-right-radius: 30px;
    border-top-left-radius: 0rem;
    border-top-right-radius: 0rem;
}
</style>