<template>
<!-- 书架列表 -->
  <div class="shelf-list" :style="{top: shelfListTop}">
    <div class="shelf-list-notice">
      <div class="shelf-list-notice-bg">{{$t('shelf.notice')}}</div>
    </div>
    <!-- 循环显示图书 -->
    <div v-for="item in data" :key="item.id" class="shelf-list-item-wrapper" :style="{width: width}">
      <shelf-item :data="item" :style="{height: height}"></shelf-item>
      <div class="shelf-list-title-wrapper">
        <span class="shelf-list-title title-small">{{item.fileName}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { storeShelfMixin } from '../../utils/mixin'
import ShelfItem from '@/components/shelf/ShelfItem'
import { realPx, px2rem } from '../../utils/utils'
export default {
  mixins: [storeShelfMixin],
  components: {
    ShelfItem
  },
  props: {
    top: {
      type: Number,
      default: 94
    },
    data: Array
  },
  data() {
    return {
      width: '',
      height: ''
    }
  },
  computed: {
    shelfListTop() {
      return px2rem(this.top) + 'rem'
    }
  },
  methods: {
    isWidthAndHeight() {
      if (window.innerWidth <= 800) {
        this.height = ((window.innerWidth - realPx(120)) / 3) / 250 * 350 + 'px'
        this.width = '33.33%'
      } else if (window.innerWidth <= 1300) {
        this.height = ((window.innerWidth - realPx(120)) / 6) / 250 * 350 + 'px'
        this.width = '16.66%'
      } else {
        this.height = ((window.innerWidth - realPx(120)) / 8) / 250 * 350 + 'px'
        this.width = '12.5%'
      }
    }
  },
  mounted() {
    this.isWidthAndHeight()
  }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
@import "../../assets/styles/global";
.shelf-list{
  position: absolute;
  left: 0;
  z-index: 100;
  display: flex;
  width: 100%;
  flex-flow: row wrap;
  padding: 0 px2rem(15);
  box-sizing: border-box;
  .shelf-list-notice{
    width: 100%;
    height: px2rem(20);
    font-size: px2rem(10);
    font-weight: 700;
    @include ellipsis2(1);
    @include center;
    .shelf-list-notice-bg {
      border: px2rem(1) solid orange;
      height: px2rem(15);
      padding: px2rem(2) px2rem(15);
      line-height: px2rem(15);
      border-radius: px2rem(10);
    }
  }
  .shelf-list-item-wrapper{
    padding: px2rem(15);
    box-sizing: border-box;
  }
  .shelf-list-title-wrapper{
    margin-top: px2rem(10);
    @include center;
  }
}
</style>
