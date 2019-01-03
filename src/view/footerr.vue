<template>
    <div class="footer_wrap ">
        <!-- <div class="left ">
            <h1 class="mb15 logo">BKB Global</h1>
            <p class="mb15">全球领先的数字资产交易平台</p>
            <div class="icon_img">
                <i class="iconfont icon-weibo"></i>
                <i class="iconfont icon-weibo"></i>
                <i class="iconfont icon-weibo"></i>
                <i class="iconfont icon-weibo"></i>
            </div>
            <p class="mt50">© 2013-2018 BKB Global</p>
        </div> -->
        <div class="">
          <div class="footer_box">
              <div class="flex mb10">
                <p class="fl tl foot_title ft16 flex1 " v-for="item in titleList">{{item}}</p>
              </div>
              <div class="flex">
                <div class="flex1">
                  <div v-for="item in conList" ><router-link :to="itm.src" class="con_a mb10 ft12" v-for="(itm,index) in item.list" :key="index">{{itm.text}}</router-link></div>
                  <a href="https://www.coinbkb.com/mobile/images/Coinbkb.pdf" target="__blank" class="con_a  ft12">白皮书</a>
                </div>
                 <div class="flex1">
                  <div v-for="item in conList2" ><router-link :to="itm.src" class="con_a mb10 ft12" v-for="(itm,index) in item.list" :key="index">{{itm.text}}</router-link></div>
                </div>
                  <div class="flex1">
                    <!-- <p  class="con_a mb10 ft12" v-for="item in contact" >{{item}}</p> -->
                    <p class="contact mt20">
                      <!-- <a href="facebook" target="_blank"><img src="../assets/images/fc.png" alt=""></a> -->
                      <a href="https://twitter.com/Coinbkb2019" target="_blank"><img src="../assets/images/tt.png" alt=""></a>
                      <a href="https://0.plus/coinbkb" target="_blank"><img src="../assets/images/by.png" alt=""></a>
                      <!-- <a href="" target="_blank"><img src="../assets/images/qq.png" alt=""></a> -->
                      <a href="http://qm.qq.com/cgi-bin/qm/qr?k=9tVzZQonwzlsGap_ZN3SouxOMTNg-pi2" target="_blank"><img src="../assets/images/qq.png" alt=""></a>
                    </p>
                    <p class="mt20 ft12">商务邮箱：coinbkb@sina.com</p>
                  </div>
                  <div class="flex1 ">
                    <img src="../assets/images/join_code.png" alt="" class="ewm ">
                    <img src="../assets/images/wechat_kefu.png" alt="" class="ewm ml40">
                  </div>
              </div>
              
            </div>
        </div>
    </div>
</template>
<script>
export default {
  // , "关注我们"
  data() {
    return {
      titleList: ["关于我们", "帮助中心", "联系我们","关注我们"],
      conList: [
        {
          list: [{ text: "隐私条款", src: "/help" },{ text: "注册协议", src: "/help" },{ text: "币种介绍", src: "/help" }]
        },
        
      ],
      conList2:[{
          list: [{ text: "账户管理", src: "/help" },{ text: "交易管理", src: "/help" },{ text: "充值提现", src: "/help" },{ text: "费用标准", src: "/help" }]
        }
        ],
      contact: [
          "QQ群号：317660286","客服微信：coinbkb", "客服邮箱：coinbkb@sina.com"
        ],
    };
  }
};
</script>
<style scoped>
.footer_wrap {
  background: #14143f;
  color: #6b80ae;
  overflow: hidden;
  padding: 50px 80px;
 
}
.contact img{
  width: 20px;
  height: 20px;
  margin-right: 10px;
}
.footer_box{
  width: 100%;
  margin: 0 auto;
}
.footer_wrap >div{
    width: 1200px;
    margin:  0 auto;
  }
.foot_title,.con_a{
  display: inline-block;
  width: 180px;
  text-align: left;
}
.con_a{
    color: #aabdbc;
}
.con_a:hover{
    color: #d45858;
}
.logo{
    color: #6b80ae;
}
.ewm{
  width: 100px;
  height: 100px;
}
</style>


