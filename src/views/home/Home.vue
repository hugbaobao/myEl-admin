<template>
<div id="Home">

<div class="left" :style="{'background-color':newcolor}">
<Aside :CollapseIs="isCollapse" @color2="changeC"></Aside>
</div>

<div class="container">
  <el-container>
  <el-header height="90px">
    <div class="navbar">
      <!-- 上半部 -->
      <div class="ico" @click= "isCollapse = !isCollapse">
      <span class="el-icon-s-unfold" v-if="isCollapse"></span>
      <span class="el-icon-s-fold" v-else></span>
    </div>
    <!-- 面包屑 -->
    <div class="font">
    <Breadcrumb></Breadcrumb>
    </div>
    <!-- 右侧头像 -->
    <el-dropdown class="others" @command="handleCommand">
  <span class="el-dropdown-link">
     <el-avatar shape="square" :size="40" :src="userPng" @error="errorHandler">
     <img src="https://cube.elemecdn.com/e/fd/0fc7d20532fdaf769a25683617711png.png" v-if="errorHandler"/>
     </el-avatar>
  <i class="el-icon-arrow-down el-icon--right"></i>
  </span>
  <el-dropdown-menu slot="dropdown">
    <el-dropdown-item command="/home/personal">个人中心</el-dropdown-item>
    <el-dropdown-item command="/home">首页</el-dropdown-item>
    <el-dropdown-item command="/login" divided>退出登录</el-dropdown-item>
  </el-dropdown-menu>
</el-dropdown>
    </div>
    <!-- 下半部 -->
<div class="bot">
<Tabs></Tabs>
</div>
  </el-header>
  <el-main class="main-container">
    <router-view></router-view>
  </el-main>
</el-container>
</div>

</div>
</template>

<script>
// 引入侧边栏
import Aside from '@/components/aside/Aside.vue'
// 引入面包屑
import Breadcrumb from '@/components/breadcrumb/Breadcrumb.vue'
// Header下半部分
import Tabs from '@/components/tabs/Tabs.vue'

import eventBus from '@/uticls/eventBus.js'

export default {
  name: 'myHome',
  created () {
    const pic = sessionStorage.getItem('userHead')
    this.userPng = pic

    eventBus.$on('color', val => {
      this.newcolor = val
    })
  },
  data () {
    return {
      isCollapse: false,
      userPng: '',
      newcolor: '#CDE0C9'
    }
  },
  methods: {
    // 头像加载失败
    errorHandler () {
      return true
    },
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    },
    handleCommand (item) {
      // console.log(item)
      this.$router.push(item)
    },
    changeC (val) {
      this.newcolor = val
      console.log(this.newcolor)
    }
  },
  components: {
    Aside,
    Breadcrumb,
    Tabs
  }
}
</script>

<style scoped>
#Home {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.el-container {
  height: 100%;
}
/* 侧边包围框 */
.left {
height: 100%;
float: left;
background-color: #CDE0C9;
}
.container {
  height: 100%;
}

  /* 头部 */
.el-container .el-header {
  padding: 0;
}
.navbar {
  height: 50px;
  line-height: 50px;
  padding: 0 20px;
  box-shadow: 0px 1px 3px  #ddd;
}
.navbar .ico {
  font-size: 24px;
  margin-right: 25px;
}
.navbar .ico,.font {
  height: 100%;
  float: left;
  display: flex;
  align-items: center;
}
/* 内容部分 */
.el-main {
background-color:#F0F2F5;
}
/* 右侧头像 */
.navbar .others {
  float: right;
  height: 100%;
}
.el-dropdown-link {
    cursor: pointer;
  }
  .el-icon-arrow-down {
    font-size: 12px;
  }
.el-avatar--square {
    border-radius: 5px;
    margin-top: 5px;
}
/* 主体内容区域 */
.main-container {
  padding: 40px;
}
</style>
