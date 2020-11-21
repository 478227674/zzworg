<template>
  <div class="menu_container">
    <el-row class="tac">
      <el-col :span="24">
        <h5 class="menu_bg"></h5>
        <el-menu
          class="el-menu-vertical-demo menu_bottom"
          :default-active="$route.path"
        >
          <!--<template v-for="(menu, index) in menus">-->
          <!--<el-submenu :index="index+''" :key="index" v-if="menu.chirdMenu">-->
          <!--<template slot="title">-->
          <!--<i :class="menu.icon"></i>-->
          <!--<span>{{menu.title}}</span>-->
          <!--</template>-->
          <!--<el-menu-item-group :key="index" v-for="(item,index) in menu.chirdMenu">-->
          <!--<router-link :to="item.path">-->
          <!--<el-menu-item   :index="item.path" :key="item.path">{{item.btn}}</el-menu-item>-->
          <!--</router-link>-->
          <!--</el-menu-item-group>-->
          <!--</el-submenu>-->
          <!--<router-link :key="index"  :to="menu.path" v-else>-->
          <!--<el-menu-item :index="menu.path" >-->
          <!--<i :class="menu.icon"></i><span slot="title">{{menu.title}}</span>-->
          <!--</el-menu-item>-->
          <!--</router-link>-->
          <!--</template>-->
          <el-submenu index="101">
            <template slot="title">
              <i class="el-icon-c-scale-to-original"></i>
              <span>机构信息</span>
            </template>
            <template>
              <router-link to="/home/organ" >
                <el-menu-item index="/home/organ" >
                  <i class="el-icon-edit-outline"></i><span slot="title">机构简介</span>
                </el-menu-item>
              </router-link>
            </template>
<!--            <template>-->
<!--              <router-link to="/home/filelist">-->
<!--                <el-menu-item index="/home/filelist">-->
<!--                  <i class="el-icon-finished"></i><span slot="title">账号认证</span>-->
<!--                </el-menu-item>-->
<!--              </router-link>-->
<!--            </template>-->
            <template v-if="roleType!=1">
              <router-link to="/home/enterprise">
                <el-menu-item index="/home/enterprise">
                  <i class="el-icon-finished"></i><span slot="title">机构认证</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/schooltypes" >
                <el-menu-item index="/home/schooltypes" >
                  <i class="el-icon-full-screen"></i><span slot="title">营业范围</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/money_orders" >
                <el-menu-item index="/home/money_orders" >
                  <i class="el-icon-full-screen"></i><span slot="title">账号余额</span>
                </el-menu-item>
              </router-link>
            </template>
          </el-submenu>
          <el-submenu index="102">
            <template slot="title">
              <i class="el-icon-shopping-bag-1"></i>
              <span>课程发布</span>
            </template>
            <template>
              <router-link to="/home/goodslist" >
                <el-menu-item index="/home/goodslist" >
                  <i class="el-icon-sell"></i><span slot="title">免费课程</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/goodsactive" >
                <el-menu-item index="/home/goodsactive" >
                  <i class="el-icon-sell"></i><span slot="title">优惠课程</span>
                </el-menu-item>
              </router-link>
            </template>
<!--            <template>-->
<!--              <router-link to="/home/recomtoindex">-->
<!--                <el-menu-item index="/home/recomtoindex">-->
<!--                  <i class="el-icon-tickets"></i><span slot="title">推荐管理</span>-->
<!--                </el-menu-item>-->
<!--              </router-link>-->
<!--            </template>-->
          </el-submenu>
          <el-submenu index="103">
            <template slot="title">
              <i class="el-icon-circle-plus-outline"></i>
              <span>内容发布</span>
            </template>

            <template>
              <router-link to="/home/newslist" >
                <el-menu-item index="/home/newslist" >
                  <i class="el-icon-news"></i><span slot="title">资讯发布</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/swiper" >
                <el-menu-item index="/home/swiper" >
                  <i class="el-icon-picture-outline"></i><span slot="title">机构相册</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/orgswiper" >
                <el-menu-item index="/home/orgswiper" >
                  <i class="el-icon-picture-outline"></i><span slot="title">轮播图发布</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/teacher" >
                <el-menu-item index="/home/teacher" >
                  <i class="el-icon-user"></i><span slot="title">教师管理</span>
                </el-menu-item>
              </router-link>
            </template>
          </el-submenu>
          <el-submenu index="104">
            <template slot="title">
              <i class="el-icon-phone-outline"></i>
              <span>信息订单</span>
            </template>
            <template>
              <router-link to="/home/ordersys" >
                <el-menu-item index="/home/ordersys" >
                  <i class="el-icon-phone-outline"></i><span slot="title">咨询信息</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/orgorder">
                <el-menu-item index="/home/orgorder">
                  <i class="el-icon-money"></i><span slot="title">收费信息</span>
                </el-menu-item>
              </router-link>
            </template>
          </el-submenu>
          <el-submenu index="105">
            <template slot="title">
              <i class="el-icon-user"></i>
              <span>用户中心</span>
            </template>
            <template>
              <router-link to="/home/procollect" >
                <el-menu-item index="/home/procollect" >
                  <i class="el-icon-star-off"></i><span slot="title">课程收藏</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/orgcollect" >
                <el-menu-item index="/home/orgcollect" >
                  <i class="el-icon-star-off"></i><span slot="title">机构收藏</span>
                </el-menu-item>
              </router-link>
            </template>
          </el-submenu>
          <el-submenu index="106">
            <template slot="title">
              <i class="el-icon-s-platform"></i>
              <span>便捷工具</span>
            </template>

            <template>
              <router-link to="/home/service" >
                <el-menu-item index="/home/service" >
                  <i class="el-icon-bell"></i><span slot="title">400坐席</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/phone_his" >
                <el-menu-item index="/home/phone_his" >
                  <i class="el-icon-bell"></i><span slot="title">通话记录</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/push" >
                <el-menu-item index="/home/push" >
                  <i class="el-icon-bell"></i><span slot="title">推送消息</span>
                </el-menu-item>
              </router-link>
            </template>
            <template>
              <router-link to="/home/coupon" >
                <el-menu-item index="/home/coupon" >
                  <i class="el-icon-discount"></i><span slot="title">优惠券管理</span>
                </el-menu-item>
              </router-link>
            </template>
          </el-submenu>

<!--          <template>-->
<!--            <router-link to="/home/organ">-->
<!--              <el-menu-item index="/home/organ">-->
<!--                <i class="el-icon-setting"></i><span slot="title">机构简介</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->

<!--          <template>-->
<!--            <router-link to="/home/goodslist">-->
<!--              <el-menu-item index="/home/goodslist">-->
<!--                <i class="el-icon-menu"></i><span slot="title">正价课程</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/goodsactive">-->
<!--              <el-menu-item index="/home/goodsactive">-->
<!--                <i class="el-icon-tickets"></i><span slot="title">优惠课程</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/special">-->
<!--              <el-menu-item index="/home/special">-->
<!--                <i class="el-icon-tickets"></i><span slot="title">特价课程</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/newslist">-->
<!--              <el-menu-item index="/home/newslist">-->
<!--                <i class="el-icon-tickets"></i><span slot="title">资讯管理</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/swiper">-->
<!--              <el-menu-item index="/home/swiper">-->
<!--                <i class="el-icon-view"></i><span slot="title">风采展示</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
          <!--<template>-->
          <!--<router-link to="/home/price_competition" >-->
          <!--<el-menu-item index="/home/price_competition" >-->
          <!--<i class="el-icon-menu"></i><span slot="title">竞价推荐</span>-->
          <!--</el-menu-item>-->
          <!--</router-link>-->
          <!--</template>-->

<!--          <template>-->
<!--            <router-link to="/home/teacher">-->
<!--              <el-menu-item index="/home/teacher">-->
<!--                <i class="el-icon-menu"></i><span slot="title">教师管理</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/push">-->
<!--              <el-menu-item index="/home/push">-->
<!--                <i class="el-icon-news"></i><span slot="title">推送消息</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/orgorder">-->
<!--              <el-menu-item index="/home/orgorder">-->
<!--                <i class="el-icon-news"></i><span slot="title">机构订单</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
          <!--<template>-->
          <!--<router-link to="/home/chatuserlist" >-->
          <!--<el-menu-item index="/home/chatuserlist" >-->
          <!--<i class="el-icon-news"></i><span slot="title">坐席管理</span>-->
          <!--</el-menu-item>-->
          <!--</router-link>-->
          <!--</template>-->
<!--          <template>-->
<!--            <router-link to="/home/orderlist">-->
<!--              <el-menu-item index="/home/orderlist">-->
<!--                <i class="el-icon-tickets"></i><span slot="title">订单列表</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/grouporderlist">-->
<!--              <el-menu-item index="/home/grouporderlist">-->
<!--                <i class="el-icon-tickets"></i><span slot="title">拼团订单列表</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/refundgrouporder">-->
<!--              <el-menu-item index="/home/refundgrouporder">-->
<!--                <i class="el-icon-tickets"></i><span slot="title">拼团退款列表</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
          <!--<template>-->
          <!--<router-link to="/home/freelist" >-->
          <!--<el-menu-item index="/home/freelist" >-->
          <!--<i class="el-icon-tickets"></i><span slot="title">试听列表</span>-->
          <!--</el-menu-item>-->
          <!--</router-link>-->
          <!--</template>-->
<!--          <template>-->
<!--            <router-link to="/home/videos">-->
<!--              <el-menu-item index="/home/videos">-->
<!--                <i class="el-icon-remove-outline"></i><span slot="title">阶段管理</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->

          <!--<template>-->
          <!--<router-link to="/home/saler" >-->
          <!--<el-menu-item index="/home/saler" >-->
          <!--<i class="el-icon-remove-outline"></i><span slot="title">销售员管理</span>-->
          <!--</el-menu-item>-->
          <!--</router-link>-->
          <!--</template>-->
<!--          <template>-->
<!--            <router-link to="/home/orgswiper">-->
<!--              <el-menu-item index="/home/orgswiper">-->
<!--                <i class="el-icon-remove-outline"></i><span slot="title">机构轮播图</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/message">-->
<!--              <el-menu-item index="/home/message">-->
<!--                <i class="el-icon-remove-outline"></i><span slot="title">动态消息管理</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/coupon" >-->
<!--              <el-menu-item index="/home/coupon" >-->
<!--                <i class="el-icon-menu"></i><span slot="title">优惠券管理</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/schooltypes" >-->
<!--              <el-menu-item index="/home/schooltypes" >-->
<!--                <i class="el-icon-menu"></i><span slot="title">营业范围</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/procollect" >-->
<!--              <el-menu-item index="/home/procollect" >-->
<!--                <i class="el-icon-menu"></i><span slot="title">查看课程收藏</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/orgcollect" >-->
<!--              <el-menu-item index="/home/orgcollect" >-->
<!--                <i class="el-icon-menu"></i><span slot="title">查看机构收藏</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/audtionuser" >-->
<!--              <el-menu-item index="/home/audtionuser" >-->
<!--                <i class="el-icon-menu"></i><span slot="title">预约试听列表</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
<!--          <template>-->
<!--            <router-link to="/home/ordersys" >-->
<!--              <el-menu-item index="/home/ordersys" >-->
<!--                <i class="el-icon-menu"></i><span slot="title">订单系统</span>-->
<!--              </el-menu-item>-->
<!--            </router-link>-->
<!--          </template>-->
        </el-menu>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        menus: [],
        roleType:'',//1为信息员跳转来的
      };
    },
    methods: {},
    created() {
      this.roleType = this.$store.state.user.user.type
    }
  };
</script>
<style>
  .el-submenu__title{
    text-align:left !important;
  }
</style>
<style lang='less' scoped>
  .el-submenu__title{
    text-align:left !important;
  }
  .menu_bg {
    height: 60px;
    background-color: #3899cc;
  }

  .menu_container {
    height: 100vh;
    background: #fff;
    position: fixed;
    left: 0;
    overflow: scroll;
    .tac {
      height: 100%;
      .el-menu-vertical-demo {
        border: none;
        min-width: 200px;
      }
    }
  }

  .el-menu-item {
    text-align: left;
    height: 50px !important;
    line-height: 50px !important;
  }
</style>
