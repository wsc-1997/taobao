<template>
  <div class="bot">
    <div class="bot-bar-item">
      <p><img src="~assets/images/detail/icon01.png" alt=""></p>
      <p>客服</p>
    </div>
    <div class="bot-bar-item">
      <p><img src="~assets/images/detail/icon02.png" alt=""></p>
      <p>店铺</p>
    </div>
    <div class="bot-bar-item">
      <p><img src="~assets/images/detail/icon03.png" alt=""></p>
      <p>收藏</p>
    </div>
    <div class="btn cart-btn" @click="addCart">加入购购物车</div>
    <div class="btn buy-btn">购买</div>
  </div>
</template>

<script>
export default {
  name: "detailbotbar",
  methods: {
    addCart() {
      this.$emit('addCart')
    }
  }
}
</script>

<style scoped>
.bot{
  height: 49px;
  background-color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 99;
  display: flex;
}
.bot-bar-item {
  flex: 1;
  width: 16%;
  font-size: 12px;
  color: #333;
  text-align: center;
}
.bot-bar-item img{
  width: 22px;
  height: 22px;
  margin: 4px 0;
  vertical-align: middle;

}
.btn {
  width: 26%;
  font-size: 13px;
  line-height: 49px;
  text-align: center;
}
.cart-btn {
  background-color: #F9CD0B;
  line-height: 49px;
}
.buy-btn {
  color: #fff;
  background-color: var(--color-high-text);
}
</style>