<template>
  <router-view/>
  <div class="home">
    <!--页面的头部-->
    <div class="top">
      <div class="top_body">
        <div class="search">
          <input type="text" placeholder="搜索车型">
        </div>
        <div>
          <img class="info" src="../assets/icon/info_icon.png">
        </div>
      </div>
    </div>
    <div @mouseover="overHd" @mouseout="auto">
      <div class="slideshow" v-for="(item,ind) in gallery"
           v-show="ind===index">
        <img :src="item.imgUrl" alt="">
      </div>
      <div class="thumbs">
			<span class="thumb" :class="{'active' :item===index+1}" v-for="item in 3" :key="item"
            @click="index=item-1"></span>
      </div>
    </div>
    <!--分类标签-->
    <div class="classify">
      <div v-for="items in item_all">
        <div v-for="item in items" @click="this.$router.push({ name:item.rPath})">
          <img :src=item.imgPath>
          <p>{{ item.name }}</p>
        </div>
      </div>
    </div>
    <div class="separate"></div>
    <!--新车，热销，二手-->
    <div class="car_classify">
      <div class="left">
        <img src="../assets/pages/Home/index/week_update.png" alt="">
      </div>
      <div class="right">
        <div>
          <img src="../assets/pages/Home/index/hot_SUV.png" alt="">
        </div>
        <div>
          <img src="../assets/pages/Home/index/second_hand.png" alt="">
        </div>
      </div>
    </div>
    <div class="separate"></div>
    <!--热销车型-->
    <div class="hot_car">
      <div class="hot_text">
        <span>热销车型</span>
        <a href="#">查看全部</a>
      </div>
      <hr />
      <div class="hot_car_list">
        <div class="car_item_left">
          <img src="../assets/pages/Home/index/car.png" alt="">
        </div>
        <div class="car_item_right">
          <p>新车 A系列 588km</p>
        </div>
      </div>
      <div class="hot_car_list">
        <div class="car_item_left">
          <img src="../assets/pages/Home/index/car.png" alt="">
        </div>
        <div class="car_item_right">
          <p>新车 A系列 588km</p>
        </div>
      </div>
      <div class="hot_car_list">
        <div class="car_item_left">
          <img src="../assets/pages/Home/index/car.png" alt="">
        </div>
        <div class="car_item_right">
          <p>新车 A系列 588km</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "HomeView",
  data() {
    return {
      item_all: [
        [{ name: "二手车", imgPath: require("../assets/icon/金刚区图标-01.png"), rPath: "second_hand" },
          { name: "新车", imgPath: require("../assets/icon/金刚区图标-02.png"), rPath: "" },
          { name: "零首付", imgPath: require("../assets/icon/金刚区图标-03.png"), rPath: "" },
          { name: "分期申请", imgPath: require("../assets/icon/金刚区图标-04.png"), rPath: "" },
          { name: "估价", imgPath: require("../assets/icon/金刚区图标-05.png"), rPath: "" }],
        [{ name: "顺风车", imgPath: require("../assets/icon/金刚区图标-06.png"), rPath: "hitch_ride" },
          // 报价卖车
          { name: "热销排行", imgPath: require("../assets/icon/金刚区图标-07.png"), rPath: "" },
          { name: "降价急售", imgPath: require("../assets/icon/金刚区图标-08.png"), rPath: "" },
          { name: "汽车百科", imgPath: require("../assets/icon/金刚区图标-09.png"), rPath: "" },
          { name: "汽车养护", imgPath: require("../assets/icon/金刚区图标-10.png"), rPath: "" }]],
      gallery: [
        {
          imgUrl: require("../assets/pages/Home/index/slideshow1.jpg")
        }, {
          imgUrl: require("../assets/pages/Home/index/tu1.png")
        }, {
          imgUrl: require("../assets/pages/Home/index/tu2.png")
        }
      ],
      index: 0,
      stopID: null
    };
  },
  created() {
    this.auto();
  },

  methods: {
    //鼠标一开  auto自动执行
    auto() {
      this.stopID = setInterval(() => {
        this.index++;
        this.check();
      }, 1000);
    },
    overHd() {
      clearInterval(this.stopID);

    },
    //检查边界
    check() {
      if (this.index === this.gallery.length) {
        this.index = 0;
      }
    }
  }
};
</script>


<style scoped>
.top {
  display: flex;
  justify-content: center;
}

.top .top_body {
  display: flex;
  margin-top: 5.6vw
}

/*搜索框*/
.search {
  margin-bottom: 3.2vw;
}

.search input {
  background: #E5E5E5 url("../assets/icon/search_icon.png") no-repeat 3.6vw 2.1333vw;
  background-size: 4.8vw 4.8vw;
  text-indent: 10vw;
  border: none;

  width: 83.4667vw;
  height: 9.2vw;
  border-radius: 2.6667vw;
  font-size: 1.6rem;
}

/*通知图标*/
.info {
  width: 5.3333vw;
  height: 5.4667vw;
  margin-top: 1.8667vw;
  margin-left: 2.6667vw;
  margin-bottom: 1.8667vw;
}

/*轮播图*/
.slideshow {
  width: 100%;
  display: flex;
  justify-content: center;
}
.slideshow img {
  height: 40.2667vw;
  border-radius: 2.6667vw;
  margin:0 auto;
}

/*轮播图下方栏*/
.thumbs {
  text-align: center;
  margin-top: 0.6vw;
  margin-bottom: 3.2vw;
}

/*子栏*/
.thumb {
  width: 1.3333vw;
  height: 1.3333vw;
  display: inline-block;
  border-radius: 2vw;
  margin: 0 0.6667vw;
  background-color: #fff;
}

/*激活的子栏*/
.active {
  background-color: #f70;
}


/*分类标签块*/
.classify {
  display: flex;
  flex-direction: column;
  height: 34.2667vw;
  text-align: center;
}

/*分类标签组*/
.classify div {
  display: flex;
  float: left;
  justify-content: space-around;
  margin-bottom: 1.9667vw;
}

/*分类标签块*/
.classify div div {
  display: flex;
  flex-direction: column;
  float: left;
  width: 20vw;
  height: 15vw;
}

/*分类标签字体*/
.classify div div p {
  height: 3.0667vw;
  font-size: 3.2vw;
  line-height: 6.5333vw;
  margin-top: -4vw;
}

/*分类标签图*/
.classify div div img {
  /*width: 10.6667vw;*/
  /*height: 9.6vw;*/
  /*水平居中*/
  margin: 0 auto;
  /*垂直居中*/
  display: inline-block;
  vertical-align: middle;
  transform:scale(0.5);
}


/*车分类*/
.car_classify {
  display: flex;
  justify-content: center
}

/*车分类图样式*/
.car_classify img {
  width: 45.0667vw;
  opacity: 0.7;
}

.car_classify .left {
  height: 33.4667vw;
}

.car_classify .right {
  height: 14.9333vw;
  margin-left: 1.6vw;
  margin-top: 0.5333vw;
  margin-bottom: 0.5333vw;
}

/*热销车辆*/
.hot_car {

}

/*热销车辆导航区*/
.hot_car .hot_text {
  display: flex;
  justify-content: space-between;
}

/*热销车型文本*/
.hot_car .hot_text span {
  height: 6.1333vw;
  font-size: 4.2667vw;
  font-weight: normal;
  color: #1E1E1E;
  line-height: 6.5333vw;

  margin-left: 4vw;
  margin-top: 2.2667vw;
  margin-bottom: 2.2667vw;
}

/*查看全部文本*/
.hot_car .hot_text a {
  height: 4.5333vw;
  font-size: 2.6667vw;
  font-weight: 400;
  color: #5B5B5B;
  line-height: 6.5333vw;

  margin-right: 5.4667vw;
  margin-top: 3.2vw;
  margin-bottom: 3.0667vw;

}

/*车辆列表*/
.hot_car .hot_car_list {
  margin-top: 2.8vw;
  display: flex;
}

/*列表 车辆图片*/
.hot_car .hot_car_list .car_item_left img {
  width: 32.5333vw;
  height: 15.8667vw;
  border-radius: 2.6667vw;
  margin-left: 3.8667vw;
}

/*列表 车辆文本*/
.hot_car .hot_car_list .car_item_right p {
  width: 32.8vw;
  height: 5.6vw;
  font-size: 3.7333vw;
  font-weight: normal;
  color: #272727;
  line-height: 6.5333vw;
  margin-left: 2.8vw;
}
.separate{
  height: 0.0667vw;
  border: 0.2667vw solid #E5E5E5;
  /* opacity: 0.8; */
  margin-top: 4.6667vw;
  margin-bottom: 3.6667vw;
}
</style>
