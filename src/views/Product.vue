<template>
  <div class="product">
    <product-param :title="product.name">
      <template v-slot:buy>
        <el-button size="mini" @click="buy">立即购买</el-button>
      </template>
    </product-param>
    <div class="content w">
      <div class="item-bg">
        <h2>小米8</h2>
        <h3>小米8 战斗天使</h3>
        <p>
          <a href="" id="">全球首款双频 GP</a>
          <span>|</span>
          <a href="" id="">骁龙845</a>
          <span>|</span>
          <a href="" id="">AI 变焦双摄</a>
          <span>|</span>
          <a href="" id="">红外人脸识别</a>
        </p>
        <div class="price">
          <span>￥<em>2599</em></span>
        </div>
      </div>
      <div class="item-swiper">
        <swiper :options="swiperOption">
          <swiper-slide><img src="/imgs/product/gallery-2.png" /></swiper-slide>
          <swiper-slide><img src="/imgs/product/gallery-3.png" /></swiper-slide>
          <swiper-slide><img src="/imgs/product/gallery-4.png" /></swiper-slide>
          <swiper-slide><img src="/imgs/product/gallery-5.jpg" /></swiper-slide>
          <swiper-slide><img src="/imgs/product/gallery-6.jpg" /></swiper-slide>
          <!-- Optional controls -->
          <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
        <p class="desc">小米8 AI变焦双摄拍摄</p>
      </div>
      <div class="item-video">
        <div class="video-bg" @click="showSlide = true"></div>
        <div class="video-box">
          <div class="overlay" v-if="showSlide"></div>
          <div class="video" :class="{ slide: showSlide }">
            <span class="icon-close" @click="closeVideo"><i class="el-icon-close"></i></span>
            <video id="video" src="https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/7f49c1ccd75f76ec86b52c9ae4c4a082.mp4" muted autoplay controls="controls"></video>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ProductParam from 'components/product/ProductParam.vue'
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
export default {
  components: {
    ProductParam,
    Swiper,
    SwiperSlide
  },
  data() {
    return {
      showSlide: false, //控制动画效果
      product: {
        name: '小米8'
      }, //商品信息
      swiperOption: {
        autoplay: {
          delay: 2000, // 自动播放
          stopOnLastSlide: false,
          disableOnInteraction: false // 触摸滑动后是否继续轮播
        },
        slidesPerView: 3,
        spaceBetween: 30,
        freeMode: true,
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        }
      }
    }
  },
  mounted() {
    this.getProduct()
  },
  methods: {
    getProduct() {
      let id = this.$route.params.id
    },
    buy() {
      let id = this.$route.params.id
      // this.$router.push(`/detail/${id}`)
      this.$router.push(`/detail/10000226`)
    },
    closeVideo() {
      this.showSlide = false
      let video = document.getElementById('video')
      if (!video) {
        return false
      } else {
        video.pause()
      }
    }
  }
}
</script>
<style lang='less' scoped>
@import '~assets/css/mixin.less';
.el-button {
  background: #ff6700;
  border-color: #ff6700;
  color: #fff;
}
.product {
  .content {
    .item-bg {
      background: url('/imgs/product/product-bg-1.png') no-repeat center;
      height: 718px;
      text-align: center;
      h2 {
        font-size: 80px;
        padding-top: 55px;
      }
      h3 {
        font-size: 24px;
        letter-spacing: 10px;
      }
      p {
        margin-top: 21px;
        margin-bottom: 40px;
        a {
          font-size: 16px;
          color: #333333;
        }
        span {
          margin: 0 15px;
        }
      }
      .price {
        font-size: 30px;
        color: #333333;
        em {
          font-style: normal;
          font-size: 38px;
        }
      }
    }
    .item-swiper {
      margin: 36px auto 52px;
      .desc {
        font-size: 18px;
        color: #333333;
        text-align: center;
      }
      img {
        width: 100%;
      }
    }
    .item-video {
      height: 540px;
      background-color: #070708;
      margin-bottom: 76px;
      color: #ffffff;
      .video-bg {
        background: url('/imgs/product/gallery-1.png') no-repeat center;
        background-size: cover;
        width: 1226px;
        height: 540px;
        margin: 0 auto 120px;
        cursor: pointer;
      }
      .video-box {
        .overlay {
          .position(fixed);
          background-color: #333;
          opacity: 0.4;
          z-index: 10;
        }
        .video {
          position: fixed;
          top: -50%;
          left: 50%;
          transform: translate(-50%, -50%);
          z-index: 10;
          width: 1000px;
          height: 536px;
          opacity: 0;
          transition: all 0.6s;
          &.slide {
            top: 50%;
            opacity: 1;
          }
          video {
            width: 100%;
            height: 100%;
            object-fit: cover; // 覆盖原生组件样式
            outline: none;
          }
          .icon-close {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 38px;
            cursor: pointer;
            z-index: 11;
            .el-icon-close {
              color: silver;
            }
          }
        }
      }
    }
  }
}
</style>