<template>
  <div>
    <v-header :seller = 'seller'></v-header>
    <div class="tab">
      <div class="tab-item">
        <a v-link="{path:'/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/seller'}">商家</a>
      </div>
    </div>
    <router-view :seller="seller" keep-alive></router-view>
  </div>
</template>

<script>
// 引用header
import header from './components/header/header.vue';
import {urlParse} from './common/js/util';
const ERR_OK = 0;

export default {
  data () {
    return {
      seller: {
        id: (() => {
          let queryParam = urlParse();
          return queryParam.id;
        })()
      }
    };
  },
  created () {
    this.$http.get('api/seller').then(response => {
      response = response.body;
      if (response.errno === ERR_OK) {
        this.seller = Object.assign({}, this.seller, response.data);
        console.log(this.seller.id);
      }
    });
  },
  components: {
    'v-header': header
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import './common/stylus/mixin.styl';

#app {
  .tab {
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;

    .tab-item {
      flex: 1;
      text-align: center;
      border-1px(rgba(7, 17, 27, 0.1));

      & > a {
        display: block;
        font-size: 14px;
        color: rgb(77, 85, 93);

        &.active {
          color: rgb(240, 20, 20);
        }
      }
    }
  }
}
</style>
