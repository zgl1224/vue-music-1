// 通用音乐歌单列表组件
<template lang="pug">
  .sheet-list(:id="id", @click="play(index)")
    .music-avatar
      img.avatar(v-imgsize="{url: avatar, w: 100}")
    .music-play.icon-menu(v-if="playSheet")
    .music-detail
      .name(:class="{active: playSheet}") {{name}}
      .singer {{getSinger}}
    .music-conf
      .mv.icon-menu
      .set.icon-menu
</template>
<script>
export default {
  props: {
    // 音乐的id
    id: {
      type: Number,
      default: 0
    },

    // 音乐的封面
    avatar: {
      type: String,
      default: ''
    },

    // 音乐名称
    name: {
      type: String,
      default: ''
    },

    // 音乐的索引
    index: {
      type: Number,
      default: 0
    },

    // 判断音乐列表的播放状态
    playSheet: {
      type: Boolean,
      default: false
    },

    // 歌手
    singer: {
      type: Array,
      default: function () {
        return []
      }
    },

    // 返回对应的list的所有的数据
    list: {
      type: Object,
      default: function () {
        return {}
      }
    }
  },

  computed: {
    getSinger () {
      return this.singer.map(item => item.name).toString()
    }
  },
  methods: {
    play (index) {
      this.$emit('play', index)
    }
  },
  created () {
    // console.log(this.singer.map(item => item.name).toString())
  }
}
</script>

<style lang="scss" scoped>
.sheet-list{
  width: 100%;
  height: auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: p2r(0.1rem) 0;
  position: relative;
  @include border-1px();
  .music-avatar{
    flex:0 0 p2r(0.9rem);
    margin-right: p2r(0.1rem);
    display: flex;
    align-items: center;
    justify-content: center;
    img{
      display: block;
      width: p2r(0.74rem);
      height: p2r(0.74rem);
      border-radius: p2r(0.04rem);
    }
  }
  .music-play{
    flex:0 0 p2r(0.4rem);
    padding-left: p2r(0.06rem);
    display: flex;
    align-items: center;
    justify-content: flex-start;
    font-size: $f_small_x;
    color: $primary_color;
  }
  .music-detail{
    flex:1 1 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    overflow: hidden;
    .name{
      font-size: $f_small_l;
      color: $text_color;
      @include els();
      width: 100%;
      text-align: left;
      &.active{
        color: $primary_color;
      }
    }
    .singer{
      width: 100%;
      text-align: left;
      font-size: $f_small_s;
      color: $color_gray;
      @include els();
    }
  }
  .music-conf{
    flex:0 0 p2r(1.3rem);
    display: flex;
    align-items: center;
    color: $color_gray_slow;
    font-size: $f_small_m;
    height: p2r(0.6rem);
    .mv,.set{
      flex: 0 0 p2r(0.6rem);
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .set{
      margin-left: p2r(0.1rem);
    }
  }
}
</style>
