<template>
  <div class="card block-list block-feed-list">
    <div class="head">
      <el-menu :default-active="activeIndex2" class="el-menu-demo"  mode="horizontal" @select="handleSelect">
        <el-menu-item index="0"><a href="#" >全部</a></el-menu-item>
        <el-menu-item v-for="item in popNode" :index="item.hid " :key="item.id">{{item.displayName}}</el-menu-item>
      </el-menu>
    </div>
    <div class="content">

      <div v-for="item in post_list"  class="list-one block-question-two clearfix">
        <div class="l1 up-count" >
          <a href="#" >
            <img class="avatar" style="width: 40px;height: 40px;border: 1px solid #85eaa9; border-radius: 4px"  :src="item.user.avatar"   alt="头像">
          </a>
        </div>
        <div class="l2">
          <h3 style="margin-top: 10px">
            <router-link  :to="'post/'+item.hid">{{ item.title }}</router-link>
          </h3>
          <div class="ct">
            <router-link :to="'/node/'+item.node.hid+'/post'">
              <span class="d post-node">
                {{ item.node.displayName }}
              </span>
            </router-link>
            <i>•</i>
            <span class="d post-author">
                            {{ item.user.name }}
                          </span>
            <span class="d update-time"><i>•</i>
                            最后回答
                          在 {{ item.lastReplyActivated }}
                          </span>
          </div>
        </div>
        <div class="l3">
          <span class="reply-count"><a href="">{{ item.replyCount}}</a> </span>
        </div>
      </div>



    </div>
    <div class="ft">
      <el-pagination
        :page-size="50"
        layout="prev, pager, next"
        @current-change="changePage"
        :total="pageTotal">
      </el-pagination>
    </div>
  </div>
</template>

<script>
  import axios from '../utils/fetch.js';
  export default {
    data() {
      return {
        activeIndex2:'0',
        post_list:[],//帖子数据列表
        nodeHid:'',
        pageTotal:0,//总页数
        popNode:[],//欢迎节点列表
      }
    },
    mounted() {
      this.getPopNode();
      this.getPostList(1);
    },
    methods: {
      handleCommand(command) {
        this.$message('click on item ' + command);
      },
      handleSelect(key, keyPath) {
          this.nodeHid = keyPath;
          this.getPostList(1);
        console.log(key, keyPath);
      },
      /**
       * 点击分页
       */
      changePage(val){
          this.getPostList(val);
      },
      /**
       * 帖子列表
       * @param page
       */
      getPostList(page){
        axios({
          method:'get',
          url:'/post?node='+this.nodeHid,
          params:{
              page:page,
          }
        }).then((res) => {
            this.post_list = res.data.data;
            this.pageTotal = res.data.pager.entities;
        })
      },
      getPopNode() {
          axios({
            method:'get',
            url: '/node/pop/show',
          }).then((res) => {
              this.popNode = res.data.data;
              console.log(res.data);
          })
      }
    }
  }
</script>

<style scoped>


  .post-node {
    background-color: #e5e5e5;
    color: #999;
    padding: 1px 2px;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -o-border-radius: 3px;
    font-size: 10px;
  }
  .post-author{
    color: #999;
  }
  .reply-count{
    color: #00a2ae;
    height:100%;
    vertical-align:middle;
    line-height:60px;
  }

</style>
