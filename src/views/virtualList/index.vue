<template>
  <div class="list-container" ref="listContainer" @scroll="handleScroll">
    <!-- 模拟滚动条的div -->
    <div class="scroll-bar" ref="scrollBar"></div>
    <ul class="list" ref="list">
      <li v-for="item in showList" :key="item.content" >{{item.content}}</li>
    </ul>
  </div>
</template>

<script>


export default {
  data() {
    return {
      start: 0,
      end:10,
      itemHeight:30,
      showNum:100,
    };
  },
  computed:{
    list(){
      return new Array(1000).fill('').map((item,index)=>{
        return {
          id:index+1,
          content:`我是内容${index}`
        }
      })
    },
    showList(){
      return this.list.slice(this.start,this.end)
    }
  },
  mounted(){
    this.$refs.listContainer.style.height=this.itemHeight*this.showNum +'px';
    this.$refs.scrollBar.style.height=this.itemHeight*this.list.length+'px';
  },
  methods: {
    handleScroll(){
      const scrollTop = this.$refs.listContainer.scrollTop;
      this.start = ~~(scrollTop / this.itemHeight);
      this.end = this.start + this.showNum;
      this.$refs.list.style.top= this.start * this.itemHeight + "px";
    }
  },
};
</script>

<style scoped>
.list-container{
    width:600px;
    border:1px solid red;
    margin:0 auto;
    position:relative;
    overflow-y:auto;
    overflow-x:hidden;
}
.list{
    position:absolute;
    top:0;
    list-style:none;
    margin:0;
}
.list li{
    height: 30px;
    line-height: 30px;
    text-align: center;
}
</style>

