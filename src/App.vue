<template>
  <div id="app">
    <v-header :seller = "seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header'
  export default {
    data () {
      return {
        seller: { }
      }
    },
    created() {
      this.$axios.get('/api/seller').then((res) => {
        this.seller = res.data.data
      })
    },
    components: {
      'v-header': header
    }
  }
</script>

<style lang='less' rel="stylesheet/less">
.tab{
  display: flex;
  width: 100%;
  height:40px;
  line-height:40px;
  border-bottom: 1px solid rgba(7, 17, 27, 0.1);
  .tab-item{
    flex: 1;
    text-align:center;
    & > a{
      display: block;
      font-size:14px;
      color: rbg(77,85,93);
      &.active{
        color: rgb(240, 20, 20);
      }
    }
  }

}

</style>
