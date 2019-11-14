<template>
  <div class="home">
    <div class="header">
      <text class="logo">豆瓣</text>
      <icon class="icon"
            type="search"
            color="#00b600"
            size="20" />
      <button>打开豆瓣App</button>
    </div>
    <div class="content"
         v-show="aMoveList.length>0">
      <view class="title">
        <text class="hot-title">影院热映</text>
        <text class="more">更多</text>
      </view>
      <scroll-view class="scroll-view_H"
                   scroll-x="true"
                   style="width: 100%">
        <view class="scroll-view-item_H "
              v-for="(item,index) in aMoveList"
              :key="item.id">
          <img :src="item.images.small"
               alt="">
          <p class="name">{{item.title}}</p>
        </view>

      </scroll-view>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      aMoveList: []
    }
  },
  created () {
    wx.request({
      url: `https://api.douban.com/v2/movie/in_theaters`, // 开发者服务器接口地址",
      data: {
        apikey: '0df993c66c0c636e29ecbb5344252a4a'
      },
      // 请求的参数",
      method: 'GET',
      header: {
        'Content-Type': 'application/x-www-form-urlencoded'
      },
      dataType: 'json', // 如果设为json，会尝试对返回的数据做一次 JSON.parse
      success: res => {
        console.log(res.data.subjects)
        this.aMoveList = res.data.subjects
      },
      fail: () => { },
      complete: () => { }
    })
  }
}
</script>


<style lang="less">
.home {
  .header {
    // width: 100%;
    height: 94rpx;
    border-bottom: 1px #eee solid;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 36rpx;
    // background-color: #eee;
    color: #00b600;
    .logo {
      font-size: 50rpx;
      font-weight: bold;
    }
    .icon {
      flex: 1;
      margin-left: 28rpx;
    }
    button {
      background-color: #42bd56;
      font-size: 24rpx;
      color: #fff;
      line-height: 58rpx;
      height: 58rpx;
      width: 200rpx;
    }
  }
.title{
  display: flex;
  justify-content: space-between;
  padding: 12rpx 38rpx;
}
  .scroll-view_H {
    white-space: nowrap;
    margin-top: 12rpx;
    margin-left: 38rpx;
  }

  .scroll-view-item_H {
    display: inline-block;
    margin-right: 12rpx;
    text-align: center;
    width: 210rpx;
    img {
      width: 200rpx;
      height: 286rpx;
    }
    .name {
      margin-top: 20rpx;
      word-break: keep-all;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .rate {
      display: flex;
      margin-top: 4rpx;
      align-items: center;
      justify-content: center;
      img {
        width: 20rpx;
        height: 20rpx;
      }
      span {
        color: #aaa;
        margin-left: 10rpx;
      }
    }
  }
}
</style>