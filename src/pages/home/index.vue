<template>
  <div>
    <div class="header">
      <span>豆瓣</span>
      <icon type="search"
            size="24"
            color="#00b600">
      </icon>
      <button>打开豆瓣APP</button>
    </div>
    <div class="move-item">
      <p class="title">
        <span class="left">影院热映</span>
        <span class="more-link">更多</span>
      </p>
      <view class="page-section-spacing">
        <scroll-view class="scroll-view_H"
                     scroll-x
                     style="width: 100%">
          <view class="scroll-view-item_H demo-text-1"
                v-for="item in moves"
                :key='item.id'>
            <img :src="item.images.medium"
                 alt="">
            <div>
              <span>{{item.title}}</span>
            </div>
            <div class="rating">
              <div class="starts" v-if="item.rating.average">
                <img src="../../../static/images/star.svg"
                     alt=""
                     v-for="(item,i) in 5"
                     :key="item">
              </div>
              <span class="num">{{item.rating.average?item.rating.average:'尚未上映'}}</span>
            </div>
          </view>
        </scroll-view>
      </view>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      moves: []
    }
  },
  onLoad () {
    this.getmsg()
  },
  methods: {
    getmsg () {
      wx.request({
        url: 'https://api.douban.com/v2/movie/in_theaters', // 开发者服务器接口地址",
        method: 'GET',
        data: {
          apikey: '0df993c66c0c636e29ecbb5344252a4a'
        },
        header: {
          'Content-Type': 'application/x-www-form-urlencoded'
        },
        success: res => {
          this.moves = res.data.subjects
          console.log(res)
        }
      })
    }
  }
}
</script>
 
<style lang='less'>
.header {
  height: 94rpx;
  border-bottom: 1rpx solid #ddd;
  display: flex;
  align-items: center;
  padding: 0 36rpx;
  span {
    color: #00b600;
    font-size: 40rpx;
  }
  icon {
    flex: 1;
    margin-left: 28rpx;
    margin-top: 8rpx;
  }
  button {
    width: 200rpx;
    height: 58rpx;
    background-color: #42bd56;
    border-radius: 8rpx;
    color: #fff;
    line-height: 58rpx;
    font-size: 24rpx;
  }
}
.move-item {
  .title {
    padding: 0rpx 10rpx;
    height: 88rpx;
    display: flex;
    align-items: center;
    justify-content: space-between;
    .left {
      font-size: 40rpx;
    }
    .more-link {
      color: #00b600;
      font-size: 30rpx;
    }
  }
}
.scroll-view_H {
  padding-left: 20rpx;
  margin-top: 12rpx;
  white-space: nowrap;
}
.scroll-view-item_H {
  text-align: center;
  display: flex;
  display: inline-block;
  align-items: center;
  margin-right: 20rpx;
  > img {
    width: 200rpx;
    height: 286rpx;
  }
  .rating {
    justify-content: center;
    display: flex;
    img {
      width: 20rpx;
      height: 20rpx;
    }
    .num{
      color: #aaa;
      margin-left: 6rpx;
    }
  }
}
</style>