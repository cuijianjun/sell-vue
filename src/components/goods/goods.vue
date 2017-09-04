<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li v-for='item in goods' class="food-list">
          <h1 class='title'>{{item.name}}</h1>
          <ul>
            <li v-for='food in item.foods' class='food-item'>
              <div class="icon">
                <img :src="food.icon">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span>月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span>￥{{food.price}}</span>
                  <span v-show = "food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>

        </li>
      </ul>
    </div>
    <div class="foods-wrapper"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        goods: []
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      this.$axios.get('/api/goods').then((res) => {
        if (res.data.errno === ERR_OK) {
          this.goods = res.data.data
        }
      })
    }
  }
</script>

<style scoped lang='less' rel="stylesheet/less">
  // @import url("../../common/style/mixin.less");
  .bg-image(@url){
    background-image: url(~"@{url}@2x.png");
    @media (-webkit-min-device-pixel-ratio:3),(min-device-pixel-ratio:3){
      background-image: url("@{url}@3x.png")
    };
  }
  .goods{
    display: flex;
    position: absolute;
    top:174px;
    bottom: 46px;
    width:100%;
    overflow: hidden;
    .menu-wrapper{
      flex: 0 0 80px;
      width: 80px;
      background-color: #f3f5f7;
      .menu-item{
        display: table;
        height: 54px;
        width: 56px;
        line-height: 14px;
        padding:0 12px;
        .icon{
          display: inline-block;
          width: 12px;
          height: 12px;
          margin-right: 4px;
          background-size:12px 12px;
          background-repeat:no-repeat;
          &.decrease{
            .bg-image('decrease_3')
          }
          &.discount{
            .bg-image('discount_3')
          }
          &.guarantee{
            .bg-image('guarantee_3')
          }
          &.invoice{
            .bg-image('invoice_3')
          }
          &.special{
            .bg-image('special_3')
          }
        }
        .text{
          display: table-cell;
          width: 56px;
          vertical-align: middle;
          font-size: 12px;
        }
      }
    }
    .foods-wrapper{
      flex:1;
      .title{
        padding-left: 14px;
        height: 26px;
        line-height: 26px;
        border-left:2px solid #d9dde1;
        font-size: 12px;
        color: rgb(147,153,159);
        background-color: #fff;
      }
      .food-item{
        display: flex;
        margin:18px;
        pa
      }
    }
  }
</style>
