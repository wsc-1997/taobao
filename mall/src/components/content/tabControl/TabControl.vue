<template>
  <div class="tab-control">
    <div v-for="(item,index) in title"
         class="tab-control-item"
         :class="{active: index === currentIndex}"
         @click="itemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  props:{
    title:{
      type: Array,
      default(){
        return []
      }
    }
  },
  data(){
    return{
      currentIndex: 0
    }
  },
  methods:{
    itemClick(index){
      this.currentIndex = index;
      this.$emit('tabClick',index)
    }
  }
}
</script>

<style scoped>
.tab-control{
  display: flex;
  text-align: center;
  font-size: 15px;
  height: 40px;
  line-height: 40px;
  background-color: #fff;
}

.tab-control-item{
  flex: 1;
}

.tab-control-item span{
  padding: 5px;
}

.active{
  color: var(--color-text);
}

.active span{
  border-bottom: 3px solid var(--color-text);
}
</style>