<template>
    <div class="indexBlackes home-box">
       <div class="swiper-container banner_wrap swiper-container-horizontal">
          <div class="swiper-wrapper">
              <div class="swiper-slide sliders" v-for="(item,index) in bannerlist"  :key="index">
        <!-- <router-link :to="{path:'/legalSeller',query:{sellerId:msg.seller_id}}" tag="span" >{{msg.seller_name}}</router-link> -->

                  <router-link :to="{path:'/components/newsDetail',query:{'id':item.id}}" >
                    <img :src="item.thumbnail" />
                  </router-link>
                  <!-- <div @click="gotoNews(item.id)">
                    <img :src="item.thumbnail" />
                  </div> -->
              </div>
            
              <!-- <div class="swiper-slide sliders">
                  <a href="">
                  <img src="../../static/imgs/swp2.png" />
                  </a>
              </div>
              <div class="swiper-slide sliders">
                  <a href="">
                  <img src="../../static/imgs/swp3.png" />
                  </a>
              </div> -->
               
              
          </div>
          <div class="swiper-pagination swiper-pagination02"></div>
      </div>
       
        <div class="coins-list">
          <div class="coin-tab">
            <ul class="coins flex">
              <li v-for="(coin,index) in quotation" :key="index" @click="nowCoin = coin.name" :class="{activeCoin:nowCoin == coin.name} " class="flex1 tc">{{coin.name}}</li>
            </ul>
          </div>
          <div class="list-title">
            <span>交易对</span>
            <span>最新价</span>
            <!-- <span>今日</span> -->
            <span>涨幅</span>
          </div>
          
          <ul class="list-con" v-for="(item,index) in quotation" :key="index" v-if="nowCoin == item.name">
            <li v-for="(li,inde) in item.quotation" :key="inde" :data-name='item.name+"/"+li.name'>
              <div class="two-coin">
                <span style="width:30px;text-align:left;display:inline-block;">
                  <img :src="li.logo" alt="" class="itemlogo">
                </span>
               <div style="display:inline-block;min-width:100px;text-align:left;">
                  <span>{{li.name}}</span>
                  <span style="color:#61688a">/{{item.name}}</span>
               </div>
              </div>
              <!-- <div class="yester">
                {{li.yesterday_last_price}}
              </div> -->
              <div class="today" :data-name='item.name+"/"+li.name'>
                {{li.now_price}}
              </div>
              <div class="yes-toa" :class="li.change<0?'down-clr':'up-clr'">
                {{li.change}}%
              </div>
            </li>
          </ul>
        </div>
        <div class="coinTable" style='display:none'>
            <div class="tabhang">
                <div class="tabul">
                    <ul class="clearfix">
                        <li :class="{active:index==curCoinTab}" v-for="(tab,index) in quotation" :key="index" @click="getCurrent(index)" >{{tab.name}}</li> 
                    </ul>
                </div>
                <div class="tabtable">
                    <ul class="table-nav">
                        <div class="nav_left">
                        <li style="width:220px;text-align:left;">交易市场</li>
                        <!-- <li>最新成交价</li>
                        <li>涨跌</li> -->
                        <li style="width:220px;text-align:center;">最高价 ( 24h )</li>
                        <li style="width:220px;text-align:center;">最低价 ( 24h )</li>
                        <li style="width:220px;text-align:center;">最新价</li>
                        <!-- <li>成交量</li> -->
                        </div>
                        <li class="last tc fr">操作</li>
                    </ul>
                    <div class="scroll list-list">
                      <ul class="content" v-for="(coin,index) in coin_list">
                          <div class="con_left">
                          <li class="hovertd" style="width:220px;text-align:left;">
                              <i class="iconfont icon-BTCUSDT-copy" style="float:initial;"></i>
                              <!-- <span class="hover">{{coin.symbol}}</span><br> -->
                              <span>{{coin.name}}</span>
                          </li>
                          <!-- <li> -->
                              <!-- <span >¥ {{coin.quotes.USD.price}}</span> -->
                              <!-- <span>{{coin.name}}</span> -->
                              <!-- / ¥ {{coin.quotes.USD.price}} -->
                              <!-- <i class="iconfont icon-arrow-down"></i> -->
                          <!-- </li> -->
                          <li style="width:220px;text-align:center;">{{coin.min_price}}</li>
                          <li style="width:220px;text-align:center;">{{coin.max_price}}</li>
                          <li style="width:220px;text-align:center;">{{coin.new_price}}≈0.00CNY</li>
                          <!-- <li class="red" :class="{green:coin.quotes.USD.percent_change_24h.toString().substr(0, 1)=='-'}">
                              <i v-if="coin.quotes.USD.percent_change_24h.toString().substr(0, 1)=='-'" class="iconfont icon-arrow-down"></i>
                              <i v-else class="iconfont icon-arrow-up"></i>
                              {{coin.quotes.USD.percent_change_24h}}%
                              </li> -->
                          <!-- <li>{{coin.highest}}</li>
                          <li>{{coin.lowest}}</li> -->
                          <!-- <li>{{coin.total_supply}}</li> -->
                          </div>
                          <li class="last fr">
                              <a class="baseColor">充币</a>
                              <a class="baseColor withdraw">提币</a>
                              <a class="baseColor">兑换</a>
                              <!-- <button>交易</button> -->
                          </li>
                      </ul>
                    </div>  
                </div>
            </div>
        </div>
        <!-- <div class="feature_wrap">
            <h2>全球领先的数字资产金融服务商</h2>
            <p>为全球超过130个国家的数百万用户提供安全、可信赖的数字资产交易及资产管理服务</p>
            <ul class="feature_list slide_ani a-fadeinB clearfix">
              <li class="feature_safe">
                <h3>安全可信赖</h3>
                <p>5 年数字资产金融服务经验</p>
                <p>专业分布式架构和防 DDOS 攻击系统</p>
              </li>
              <li class="feature_eco">
                <h3>全球生态布局</h3>
                <p>多个国家设立本土化交易服务中心<br>打造多业务形态为一体的区块链生态圈</p>
              </li>
              <li class="feature_user">
                <h3>用户至上</h3>
                <p>建立先行赔付机制</p>
                <p>设立投资者保护基金</p>
              </li>
            </ul>
        </div> -->
        <div class="md">
          <div>
            <div class="">
              <span>安全有保障</span>
              <span>资金托管</span>
            </div>
            <router-link to="/components/register" tag="div" class="btn">立即加入</router-link>
            <div>
              <img src="https://ztstatic.oss-cn-hangzhou.aliyuncs.com/zg72/img/home-zg-pic-$.d1d0840.jpg" alt="">
            </div>
          </div>
          <div>
            <div>全球数字资产交易平台</div>
            <div>支持币币交易、货币交易的区块链数字资产交易平台，由全球多国多领域顶级人才构成的精英团队，在系统安全、微秒级高负载、金融领域拥有资深经验</div>
          </div>
        </div>
        <div class="notice flex">
          <div>
            <div class="notpic1"></div>
            <div>Coinbkb多功能生活服务</div>
            <div>“心”的生活服务体验，让区块链服务于生活，全球多个国家开放平台币充值缴费，水电煤等。</div>
          </div>
          <div>
            <div class="notpic2"></div>
            <div>全球生态合伙人</div>
            <div>Coinbkb 每个月拿出20%平台利润 用于给全球生态合伙人进行分红。大力建设合伙人新生态社区。</div>
          </div>
          <div>
            <div class="notpic3"></div>
            <div>极速交易安全稳定</div>
            <div>超高性能撮合交易技术架构，多级数据灾备，1:1准备金仓储，Coinbkb不仅仅是交易所也是您的高级资产安全管理钱包！</div>
          </div>
          <div>
            <div class="notpic4"></div>
            <div>贵宾级客户服务</div>
            <div>7X24X365天及时响应1V1客服服务！为您的数字资产安全交易保驾护航！</div>
          </div>
          
          
        </div>
        <div class="mb">
          <img src="../assets/images/homemb.jpg" alt="">
           <div>
              <div> 随时随地 不错过任何机会</div>
              <p> 实时交易：买入、卖出、杠杆</p>
              <p> 随身充提：充值、提现</p>
              <p>实时提醒：行情提醒、事件提醒</p>
              <div class="flex down">
                <div class="  posrel flex alcenter  jscenter mr20" @mouseover="anclick" @mouseout="anclick2">
                  <img src="../assets/images/an.png" alt="" class="mr10 imglogo">
                    <span class="" >安卓下载</span>
                    <img src="../assets/images/ewm.png" alt="" class="erweima mt20 posabs" v-show="show1">
                </div>
                <div class="  posrel flex alcenter jscenter " @mouseover="appleclick" @mouseout="appleclick2">
                   <img src="../assets/images/apple.png" alt="" class="mr10 imglogo">
                  <span class="">苹果下载</span>
                  <img src="../assets/images/ewm.png" alt="" class="erweima mt20 posabs" v-show="show2">
                </div>
            </div>
           </div>
          
        </div>
        <div class="news">
          <p class="">公告</p>
          <div class="line"></div>
          <div class="items">
            <div class="item" v-for='(item,index) in noticeList' :key="index" @click="goDetail(item.id)">
              <div class="date">{{item.title}}</div>
              <div class="content">
                <img src="../assets/images/notbg.jpg" alt="">
                <div class="title">{{item.title}}</div>
                <p v-html="item.content"></p>
              </div>
            </div>
            
            
          </div>
        </div>
        <!-- <footer>
          <div class="content flex">
            <dl>
              <dt>网站功能</dt>
              <router-link to="/legalTrade" tag="dd">法币交易</router-link>
              <router-link to="/dealCenter" tag="dd">币币交易</router-link>
            </dl>
            <dl>
              <dt>用户帮助</dt>
              <router-link to="/components/login" tag="dd">登录</router-link>
              <router-link to="/components/register" tag="dd">注册</router-link>
              <router-link to="/forgetPwd" tag="dd">找回密码</router-link>
            </dl>
            <dl>
              <dt>app下载</dt>
              <dd></dd>
            </dl>
          </div>
        </footer> -->
    </div>
    
</template>


<script>
import "@/assets/style/iconfont2.css";
import "@/assets/style/iconfont.css";
import "@/assets/style/index.css";
import Swiper from "swiper";
import "swiper/dist/css/swiper.min.css";
import indexHeader from "@/view/indexHeader";
// var echarts = require("echarts");
export default {
  name: "homeContent",
  components: { indexHeader },
  data() {
    return {
      quotation: [],
      nowCoin: "",
      //   banner_imgs:[
      //       {href:'',img:'../assets/images/bg2.png'},
      //       {href:'',img:'../assets/images/bg2.png'},
      //       {href:'',img:'../assets/images/bg2.png'}
      //   ],
      curSwiper: 0,
      curCoinTab: 0,
      coinTabList: [{ title: "USDT行情" }, { title: "BTC行情" }],
      coinKlineList: [],
      coinKline: {},
      swiperList: [],
      coinList: [],
      coin_list: [],
      bannerlist:[],
      noticeList: [],
      swiperImgs: [],
      show1:false,
      show2:false
    };
  },
  created() {
    // this.init(this.initKline);
    this.getQuotation();
  },
  mounted() {
    // this.getSwiper();
    var mySwiper = new Swiper(".swiper-container01", {
      // 如果需要分页器
      pagination: ".swiper-pagination01",
      paginationClickable: true,
      // 如果需要前进后退按钮
      slidesPerView: 5,
      nextButton: ".swiper-button-next",
      prevButton: ".swiper-button-prev",
      observer: true, //修改swiper自己或子元素时，自动初始化swiper
      observeParents: true //修改swiper的父元素时，自动初始化swiper
    });
     var mySwiper02 = new Swiper(".banner_wrap", {
        // direction: 'horizental',
        loop: true,
        autoplay: 2000,
        // 如果需要分页器
        pagination: ".swiper-pagination02",
        paginationClickable: true,
        observer: true, //修改swiper自己或子元素时，自动初始化swiper
        observeParents: true //修改swiper的父元素时，自动初始化swiper
      });
    // this.connect();
    this.getNews();
  },
  methods: {
    anclick(){
      this.show1=true;
    },
     anclick2(){
      this.show1=false;
    },
    appleclick(){
      this.show2=true;
    },
     appleclick2(){
      this.show2=false;
    },
    connect() {
      var that = this;
      //console.log("socket");
      that.$socket.emit("login", localStorage.getItem("user_id"));
      that.$socket.on("transaction", msg => {
        var cname = msg.token;
        var yesprice = msg.yesterday;
        var toprice = msg.today;

        var zf = 0;
        if (toprice == yesprice) {
          zf = 0;
        } else if (yesprice == 0) {
          zf = 100;
        } else {
          zf = (((toprice - yesprice) / yesprice) * 100).toFixed(4);
        }

        console.log(cname, yesprice, toprice, zf);

        if (zf >= 0) {
          zf = "+" + zf + "%";
          $("div[data-name='" + cname + "']")
            .next()
            .css("color", "#55a067");
        } else {
          zf = zf + "%";
          $("div[data-name='" + cname + "']")
            .next()
            .css("color", "#cc4951");
        }
        $("li div[data-name='" + cname + "']")
          .prev()
          .text(yesprice);
        $("li div[data-name='" + cname + "']")
          .html(toprice)
          .next()
          .html(zf);
      });
    },
    setPercent(a, b) {
      if (a - b == 0) {
        return "0%";
      } else if (a == 0) {
        return "-100%";
      } else if (b == 0) {
        return "+100%";
      } else {
        var p = ((a - b) / b / 100).toFixed(2);
        if (p > 0) {
          p = "+" + p + "%";
        } else {
          p = p + "%";
        }
        return p;
      }
    },
    getQuotation() {
      this.$http({
        url: "/api/currency/quotation",
        method: "get"
      }).then(res => {
        if (res.data.type == "ok" && res.data.message.length != 0) {
          this.quotation = res.data.message;
          this.nowCoin = this.quotation[0].name;
        }
      });
    },
    getCurrent(index) {
      this.curCoinTab = index;
    },
    mouseEnter(index) {
      this.curSwiper = index;
    },
    init(callback) {
      this.$http.post("/api/" + "quotation").then(res => {
        if (res.data.type == "ok") {
          this.coinList = res.data.message.coin_list;
          this.swiperList = res.data.message.coin_list;
          callback && callback();
        } else {
          // layer.msg(res.message);
        }
      });
    },

    timestampToTime(timestamp) {
      var date = new Date(timestamp);
      let Y = date.getFullYear() + "/";
      let M =
        (date.getMonth() + 1 < 10
          ? "0" + (date.getMonth() + 1)
          : date.getMonth() + 1) + "/";
      let D = date.getDate() + " ";
      return Y + M + D;
    },
    // 公告
    getNews() {
      this.$http({
        url: "/api/news/list?c_id=9",
        method:'post'
      }).then(res => {
        console.log(res);
        if (res.data.type == "ok") {
          this.bannerlist = res.data.message.list;
         
        }
      });
      this.$http({
        url:  '/api/news/list',
        method:'post',
      }).then(res => {
        if(res.data.type == 'ok'){
          var list = res.data.message.list;
          if(list.length>2){
            this.noticeList = list.slice(0,3);
          } else {
            this.noticeList = list;
          }
        }
        
      })
        
    },
    // 公告详情
    goDetail(id) {
      var id = id;
      this.$router.push({
        name: "noticeDetail",
        query: { id: id }
      });
    }
  }
};
</script>
<style lang='scss' scoped>
 .itemlogo{
    width: 24px;
    height:auto;
    vertical-align: middle;
  }
footer{
 
  background: rgb(20,20,63);
  padding: 30px 0;

  .content{
    width: 1500px;
    margin: 0 auto;
    justify-content: space-between;
    dl{
      
      dt{
        font-size: 16px;
        color: #fff;
        margin-bottom: 20px;
      }
      dd{
        font-size: 14px;
        color: #8b89c8;
        line-height: 24px;
        cursor: pointer;
        &:hover{
          color: #fff;
        }
      }
    }
    dl:last-child{
      dd{
        background: url('../assets/images/ewm.png') no-repeat;
        width: 100px;
        height: 100px;
        background-size: 100%;
      }
    }
  }
}
.md {
  width: 1500px;
  margin: 0 auto;
  > div:first-child {
    margin-top: 90px;
    text-align: center;
    font-size: 40px;
    color: #fff;
    > span:last-child {
      margin-left: 6px;
      color: #33fffb;
    }
    .btn {
      background: linear-gradient(90deg, #33fffb, #44c3d5);
      width: 268px;
      margin: 30px auto 0;
      text-align: center;
      line-height: 56px;
      border-radius: 30px;
      font-size: 18px;
      color: #fff;
    }
    img {
      display: block;
      margin: 0 auto;
      width: 1180px;
      height: 635px;
    }
  }
  > div:nth-child(2) {
    padding-top: 60px;
    background: url("https://ztstatic.oss-cn-hangzhou.aliyuncs.com/zg72/img/home-zg-bg-1.5159fa3.jpg")
      right top/ 832px 432px no-repeat;
    height: 500px;
    > div:first-child {
      font-size: 40px;
      font-weight: bold;
      color: #bec1da;
    }
    > div:nth-child(2) {
      margin-top: 20px;
      color: rgba(139, 137, 200, 0.5);
      line-height: 30px;
      width: 45%;
    }
  }
}
.news {
  margin-top: 100px;
  position: relative;
  > p {
    font-weight: 600;
    font-size: 20px;
    margin: 200px auto 100px;
    color: #fff;
    width: 1500px;
  }
  .line {
    position: absolute;
    width: 100%;
    height: 1px;
    background: rgba(255, 255, 255, 0.05);
    top: 185px;
  }
  > .items {
    width: 1500px;

    margin: 0 auto;
    display: flex;
    justify-content: space-between;

    > .item {
      transition: all 0.3s;
      height: 330px;
      cursor: pointer;
      color: hsla(0, 0%, 100%, 0.9);
      border-radius: 4px;
      width: 33%;
      > .date {
        font-size: 24px;
        padding-bottom: 60px;
        color: #bec1da;
      }
      > p {
        color: #8b89c8;
      }
      .content {
        position: relative;
        transition: all 0.3s;
        max-width: 485px;
        height: 206px;
        padding: 30px;
        border-radius: 6px;
        background-color: rgba(24, 24, 76, 1);
        background-size: 100% !important;
        &::before {
          content: "";
          position: absolute;
          left: 50px;
          top: -10px;
          width: 0;
          border-right: 10px solid transparent;
          border-left: 10px solid transparent;
          border-bottom: 10px solid #2b2b6d;
          opacity: 0;
          -webkit-transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1);
          transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }
        img {
          position: absolute;
          border-radius: 6px;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          opacity: 0;
          transition: all 0.5s;
          // z-index: -1;
        }
        .title {
          font-size: 16px;
          color: #bec1da;
          padding-bottom: 30px;
        }
        p {
          font-size: 14px;
          color: #8b89c8;
        }
      }
      > .title {
        font-size: 16px;
        color: #bec1da;
        // font-weight:
      }
      &:hover {
        transition: all 0.5s;

        .content {
           &::before{
             opacity: 1;
           }
          > p,
          > div {
            transform: translateY(16px);
            transition: all 0.5s;
          }
          img {
            transition: all 0.5s;
            opacity: 1;
          }
          // background: rgba(24, 24, 76, 0) url("../assets/images/homehov.jpg");
          // background-size: 100%;
        }
      }
    }
    > .item:nth-child(3) {
      opacity: 1;

      .content {
        &::before{
          opacity: 1;
        }
        div,
        p {
          position: relative;
          z-index: 99;
        }
        img {
          opacity: 1;
        }
      }
    }
  }
}
.notice {
  width: 1500px;
  margin: 0 auto;
  justify-content: space-between;
  > div {
    border-radius: 3px;
    font-size: 12px;
    padding: 30px;
    width: 360px;
    height: 360px;
    color: rgba(139, 137, 200, 0.5);
    background: linear-gradient(to bottom right, #2b2b6d, #18184c);
    cursor: pointer;
    box-shadow: none;
    transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);

    > div:nth-child(2) {
      transition: all 0.3s;
    }
    div:nth-child(3) {
      padding-top: 10px;
    }
    &:hover {
      background: url("../assets/images/homehov.jpg") center center/ 100% 100%
        no-repeat;
      box-shadow: 0 0.05rem 0.45rem rgba(0, 0, 0, 0.2);
      transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
      color: #fff;
      > div:nth-child(2) {
        transform: translateY(-10px);
        transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
      }
      > div:nth-child(3) {
        border-top: 1px solid rgba(139, 137, 200, 0.5);
      }
      .notpic1 {
        background-image: url("../assets/images/hhov2.png") !important;
      }
      .notpic2 {
        background-image: url("../assets/images/hhov4.png") !important;
      }
      .notpic3 {
        background-image: url("../assets/images/hhov5.png") !important;
      }
      .notpic4 {
        background-image: url("../assets/images/hhov8.png") !important;
      }
    }
    > div:first-child {
      width: 80px;
      height: 88.8px;
      margin: 30px auto 0;
      margin-bottom: 20px;
      text-align: center;
    }
    > div:nth-child(2) {
      font-size: 18px;
      margin: 30px 0 20px;
      color: #bec1da;
    }
    > div:last-child {
      line-height: 24px;
    }
  }
  > div:first-child {
    > div:first-child {
      background: url("../assets/images/hhov1.png") center center/ 100% 100%
        no-repeat;
    }
  }
  > div:nth-child(2) {
    > div:first-child {
      background: url("../assets/images/hhov3.png") center center/ 100% 100%
        no-repeat;
    }
  }
  > div:nth-child(3) {
    > div:first-child {
      background: url("../assets/images/hhov6.png") center center/ 100% 100%
        no-repeat;
    }
  }
  > div:nth-child(4) {
    > div:first-child {
      background: url("../assets/images/hhov7.png") center center/ 100% 100%
        no-repeat;
    }
  }
}
.mb {
  position: relative;
  // margin-top: 100px;
  height: 800px;
  padding-left: 800px;
  >img {
    position: absolute;
    left: -497px;
    top: 0;
    width: 1770px;
  }
  > div {
    display: flex;
    position: relative;
    z-index: 99;
    height: 800px;
    justify-content: center;
    flex-direction: column;
    > div {
      padding: 100px 0 30px;
      font-size: 36px;
      color: #33fffb;
    }
    p {
      line-height: 30px;
      color: rgba(139, 137, 200, 0.5);
    }
  }
  .down{
    font-size: 14px;
    color: #8B89C8;
    >div{
      width: 180px;
      height: 50px;
      border-radius: 25px;
      line-height: 50px;
      border:1px solid #8b89c8;
      .imglogo{
        width: 26px;
      }
      .erweima{width: 150px;height: 150px;top: 40px;}
    }
  }
}
.home-box {
  background: rgb(24, 24, 76);
}
// div.swiper-container .swiper-pagination {
//   left: initial;
//   right: 10px !important;
//   top: 0;
//   height: 100%;
//   width: 10px;
//   display: flex;
//   flex-direction: column;
//   justify-content: center;
// }
// div.swiper-container .swiper-pagination > span {
//   display: block;
//   background: #fff;
//   opacity: 0.5;
//   margin: 10px 0;
// }
// div.swiper-container .swiper-pagination-bullet-active {
//   background: transparent;
//   border: 2px solid #55a067;
// }
.up-clr {
  color: #55a067;
}
.down-clr {
  color: #cc4951;
}
/* 币种列表 */
.coins-list {
  margin: 10px auto;
  width: 1500px;
  line-height: 40px;
  text-align: center;
  // border: 1px solid #4e5b85;
  .coin-tab {
    height: 42px;
    color: #c7cce6;
    // display: flex;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    > ul {
      display: flex;
      li {
        padding: 0 40px;
        font-size: 14px;
        // box-shadow: 0 0 1px hsla(231, 9%, 54%, 0.2);
        // border-bottom: 1px solid #4e5b85;
        // border-right: 1px solid #4e5b85;
      }
      .activeCoin {
        border-bottom: none;
      }
    }
  }
  .list-title {
    display: flex;
    > span {
      flex: 1;

      text-align: center;
      color: #8b89c8;
      font-size: 14px;
    }
  }
  .list-con {
    // background: rgb(32, 36, 55);
    max-height: 680px;
    overflow: auto;
    &::-webkit-scrollbar {
      display: none;
    }
    li:nth-child(2n) {
      background: rgb(24, 24, 76);
    }
    li:nth-child(2n + 1) {
      background: rgb(34, 31, 97);
    }
    li {
      display: flex;
      // border-bottom: 1px solid #282e44;
      color: #c7cce6;
      &:hover {
        background: rgb(22, 22, 68);
      }
      > div {
        flex: 1;
      }
    }
  }
}
.carousel .swiper-slide:hover {
  background-color: #327add;
}
.nav_left,
.con_left {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.withdraw {
  margin: 0 4px;
}
.carousel .last a:hover {
  cursor: pointer;
}
.sliders {
  width: 100%;
}
.sliders img {
  width: 100%;
  height: 500px;
}
.notice_ul {
  margin: 0 40px;
  padding: 5px 0;
  // background: #14143f;
  overflow: hidden;
  word-break: keep-all;
}
.notice_ul > li {
  // flex: 1;
  font-size: 12px;
  padding: 0 15px;
  text-align: center;
  color: #9eb5ca;
  word-break: keep-all;
  position: relative;
}
.notice_ul > li::after {
  content: "/";
  position: absolute;
  left: -0.5em;
  color: #9eb5ca;
}
.notice_ul > li:last-child:after {
  content: "";
  color: #6b80ae;
}
.notice_ul > li:hover {
  color: #6b80ae;
  cursor: pointer;
}
.feature_wrap {
  // background-color: #fff;
  padding: 100px 0;
  text-align: center;
  color: #54748f;
  line-height: 2em;
}
.feature_wrap h2 {
  font-size: 28px;
  margin-bottom: 10px;
  color: #192544;
}
.feature_wrap .feature_list {
  padding-top: 80px;
  width: 70%;
  margin: 0 auto;
}
.feature_wrap .feature_list li {
  float: left;
  width: 33%;
  background: transparent none no-repeat top;
  padding-top: 218px;
}
.feature_wrap .feature_list li.feature_safe {
  background-image: url(../../static/imgs/feature_safe.8e76904.svg);
}
.feature_wrap .feature_list li.feature_eco {
  background-image: url(../../static/imgs/feature_eco.4f174e6.svg);
}
.feature_wrap .feature_list li.feature_user {
  background-image: url(../../static/imgs/feature_user.7002f27.svg);
}
.feature_wrap h3 {
  font-size: 18px;
  font-weight: 700;
  margin-bottom: 10px;
  color: #192544;
}

</style>


