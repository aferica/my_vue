<template>
  <div class="sidebar">

    <div class="login-auth block-user-view-info  block-right">
      <div class="block " style="margin-bottom: 20px;">
        <router-link to="/post_create">
          <el-button :plain="true" type="success" icon="edit">创建新主题</el-button>
        </router-link>
      </div>
    </div>

    <div :style="infoStyle" class="block-user-view-info  block-right">
      <h2>{{ name }}</h2>
      <div class="content clearfix">
        <div class="l1">
          <div class="user-avatar">
            <img :src="avatarSrc" class="avatar">
          </div>
        </div>
        <h2 style="background-color: #fff"></h2>
        <h2 style="background-color: #fff">
          <router-link to="/my">
            个人中心


          </router-link>
        </h2>
        <h2 style="background-color: #fff">
          <router-link to="/my?activePage=2">
            未读动态({{ unreadNum }})


          </router-link>
        </h2>
        <h2 style="background-color: #fff" @click="logout">
          <a href="#">点击退出</a>
        </h2>
      </div>
    </div>

    <div :style="loginStyle" class="block-user-view-info  block-right">
      <h2>登录</h2>
      <div class="block " style="margin-top: 20px">
        <router-link to="/login">
          <el-button type="success" class="login email_login">邮箱登录</el-button>
        </router-link>
      </div>
      <div class="block ">
        <a href="https://demo.g9zz.com/auth/github">
          <el-button type="success" class="login github_login">Github登录</el-button>
        </a>
      </div>
      <div class="block ">
        <el-button :disabled="true" type="success" class="login qq_login">QQ登录</el-button>
      </div>
      <div class="block ">
        <!--<router-link to="/" >-->
        <el-button :disabled="true" type="success" class="login weibo_login">微博登录</el-button>
        <!--</router-link>-->
      </div>
      <div class="block " style="margin-bottom: 20px">
        <!--<router-link to="/" >-->
        <el-button :disabled="true" type="success" class="login weixin_login">微信登录</el-button>
        <!--</router-link>-->
      </div>

    </div>


    <div class="search">
      <el-input
        placeholder="搜索功能还未完成.."
        size="large"
        icon="search"
        v-model="postSearch"
        :on-icon-click="handleIconClick">
      </el-input>
    </div>
    <div class="ad block-user-view-info  block-right">
      <h2>ad</h2>
      <!--<div class="f-g-f"><span>ad</span></div>-->
      <div class="ad-img">
        <a href="#"><img class="ad-1" src="../../static/ad-test.jpg" alt=""></a>
        <a href="#"><img class="ad-1" src="../../static/ad-test.jpg" alt=""></a>
      </div>

    </div>
    <div class="hot block-user-view-info  block-right">
      <!--<div class="f-g-f"><span>hot topics</span></div>-->
      <h2>hot topics</h2>
      <el-table
        :data="hotData"
        class="hotTable"
        :show-header="false"
        @row-click="clickPopPost"
        :border="false"
      >
        <el-table-column
          prop="title"
          header-align="center"
          show-overflow-tooltip
        >
        </el-table-column>
      </el-table>
    </div>
    <div class="hot block-user-view-info  block-right">
      <!--<div class="f-g-f"><span>hot topics</span></div>-->
      <h2>hot node</h2>
      <div style="margin: 10px">
        <span v-for="(item,index) in mostNode">
          <router-link :to="'/node/'+item.hid +'/post'">
          <span v-if="index%4 === 0">
            <el-tag style="margin: 4px" type="danger"> {{item.displayName}} </el-tag>
          </span>
          <span v-else-if="index%4 === 1">
            <el-tag style="margin: 4px" type="primary"> {{item.displayName}} </el-tag>
          </span>
          <span v-else-if="index%4 === 2">
            <el-tag style="margin: 4px" type="success"> {{item.displayName}} </el-tag>
          </span>
          <span v-else-if="index%4 === 3">
            <el-tag style="margin: 4px" type="warning"> {{item.displayName}} </el-tag>
          </span>
        </router-link>
        </span>
      </div>
      <span style="text-align:center;display:block">
        <router-link to="/node">
          <el-tag style="margin-bottom: 10px" type="danger"> >>>全部节点<<< </el-tag>
        </router-link>
      </span>
    </div>
    <div class="note block-user-view-info  block-right">
      <h2>note</h2>
      <!--<div class="f-g-f"><span>note</span></div>-->
      <div class="n-note">
        <el-collapse v-model="activeNames">
          <el-collapse-item title="富强、民主、文明" name="1">
            <div>QQ群：440221268；</div>
            <div>Email：zgh@g9zz.com</div>
          </el-collapse-item>
          <el-collapse-item title="和谐、自由、平等" name="2">
            <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
            <div>页面反馈：操作后，通过页面元素的变化清晰地展现当前状态。</div>
          </el-collapse-item>
          <el-collapse-item title="公正、法治、爱国" name="3">
            <div>简化流程：设计简洁直观的操作流程；</div>
            <div>清晰明确：语言表达清晰且表意明确，让用户快速理解进而作出决策；</div>
            <div>帮助用户识别：界面简单直白，让用户快速识别而非回忆，减少用户记忆负担。</div>
          </el-collapse-item>
          <el-collapse-item title="敬业、诚信、友善" name="4">
            <div>用户决策：根据场景可给予用户操作建议或安全提示，但不能代替用户进行决策；</div>
            <div>结果可控：用户可以自由的进行操作，包括撤销、回退和终止当前操作等。</div>
          </el-collapse-item>
        </el-collapse>
      </div>

    </div>
  </div>
</template>

<script>
  import cookie from '../utils/cookie.js'
  import axios from '../utils/fetch.js'
  export default {
    data () {
      return {
        postSearch: '',
        hotData: [],
        mostNode: [],
        activeNames: ['1'],
        avatarSrc: 'http://image.iphpt.com/G_logo.jpg',
        name: 'G9ZZ',
        loginStyle: 'display:block',
        infoStyle: 'display:none',
        unreadNum: 0,
      }
    },
    mounted() {
      this.initStyle();
      this.getPopPost();
      this.getMostNode();
    },
    methods: {
      handleIconClick () {
        console.log('帖子搜索', this.postSearch);
      },
      initStyle() {
        if (cookie.getCookie('token')) {
          //校验下token  如果失效了,要不重新生成一个新的!
          axios({
            url: 'updateToken',
            method: 'get',
            headers: {
              'x-auth-token': cookie.getCookie('token')
            }
          }).then((res) => {
            if (res.data.code === 200) {
              cookie.setCookie('token', res.data.data.token);
              cookie.setCookie('hid', res.data.data.hid);
            }
          }),
            this.loginStyle = 'display:none';
          this.infoStyle = 'display:block';
          let hid = cookie.getCookie('hid');
          this.getUserInfo(hid);
          this.getUnreadNum(hid);
        } else {
          this.loginStyle = 'display:block';
          this.infoStyle = 'display:none';
        }
      },
      getUnreadNum(hid) {
        let that = this;
        axios({
          url: '/notify/unreadNum',
          method: 'get'
        }).then((res) => {
          that.unreadNum = res.data.data.count;
        })
      },
      getUserInfo(hid) {
        axios({
          url: '/user/' + hid,
          method: 'get',
        }).then((res) => {
          this.avatarSrc = res.data.data.avatar;
          this.name = res.data.data.name;
        })
      },
      getPopPost() {
        axios({
          url: '/post/most/pop',
          method: 'get',
        }).then((res) => {
          this.hotData = res.data.data;
        })
      },
      getMostNode() {
        axios({
          url: '/node/most/show',
          method: 'get'
        }).then((res) => {
          this.mostNode = res.data.data;
        })
      },
      clickPopPost(val){
        console.log(2222);
        this.$router.push('/post/' + val.hid);
      },
      logout() {
        cookie.clearCookie('token');
        cookie.clearCookie('hid');
        location.reload();
      }
    }
  }
</script>

<style scoped>
  .sidebar {
    /*min-height:300px;*/
    /*background-color: cornflowerblue;*/
    /*margin-left: 20px;*/
    /*border: 1px solid #d1dbe5;*/
    /*border-radius: 4px;*/
  }

  .sidebar > div {
    border: 0 solid #d1dbe5;
    border-radius: 4px;
    box-shadow: 0 6px 11px #dad3d2;
  }

  .block-siteuser-add {
    margin-bottom: 15px;
  }

  .block-user-view-info {
    background-color: #fff;
    margin-bottom: 15px;
  }

  .block-user-view-info .block {
    text-align: center;
  }

  .login-auth {
    background-color: #fff;

  }

  .search {
    margin-top: 15px;
    min-height: 20px;
    background-color: #fff;
    padding: 10px;
  }

  .ad {
    margin-top: 15px;
    min-height: 100px;
    background-color: #fff;
  }

  .ad-img {
    padding: 10px;
    background-color: #fff;
  }

  .ad-1 {
    height: 50px;
    width: 100%;
    overflow: hidden;
    background-size: cover;
    margin-top: 5px;

  }

  .hot {
    margin-top: 15px;
    min-height: 100px;
    background-color: #fff;
  }

  .hotTable {
    width: 100%;
    padding: 10px;
  }

  .note {
    margin-top: 15px;
    min-height: 100px;
    background-color: #fff;
  }

  .f-g-f {
    padding: 10px;
    letter-spacing: -1px;
    color: #b59797;
    border-bottom: 1px solid #ddd;
    background-color: #eef5f1;
  }

  .f-g-f span {
    letter-spacing: 0;
    line-height: 8px;
  /assets/ images / weibo . png text-align: center;
    display: block;
  }

  /*.block-siteuser-add .lbtn  {*/
  /*width: 100%;*/
  /*padding: 8px 0;*/
  /*}*/
  .login {
    margin: 5px;
    width: 50%;
  }

  .github_login {
    border-color: black;
    color: black;
    background: url('../../static/images/github_login.png') no-repeat 10px 9px #fff;
  }

  .email_login {
    border-color: #acacac;
    color: #acacac;
    background: url('../../static/images/email_login.jpg') no-repeat 10px 9px #fff;
  }

  .qq_login {
    border-color: #37b5f9;
    color: #37b5f9;
    background: url('../../static/images/qq_login_03.jpg') no-repeat 10px 8px #fff;
  }

  .weibo_login {
    border-color: #f26d7e;
    color: #f26d7e;
    background: url('../../static/images/weibo_login_10.jpg') no-repeat 10px 8px #fff;
  }

  .weixin_login {
    border-color: #13ce66;
    color: #13ce66;
    background: url('../../static/images/weixin_login_15.jpg') no-repeat 10px 8px #fff;
  }
</style>
