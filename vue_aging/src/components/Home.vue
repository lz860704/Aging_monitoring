<template>
    <el-container class="home-container">
        <!-- 头部区域 -->
        <el-header>
            <div>
                <img src="../assets/logo.png" alt="">
                <span>老化数据查询平台</span>
            </div>
            <div>
                <!-- 将按钮封装到一起 -->
                <el-button type="success" @click="refresh">刷新</el-button>
                <el-button type="primary" @click="logout">返回</el-button>
            </div>
        </el-header>
        <!-- 整体页面主体 -->
        <el-container>
            <!-- 侧边栏 -->
            <el-aside width="200px">
                <!-- 侧边栏区域 -->
                <el-menu background-color="#545c64" text-color="#fff" active-text-color="#409EFF" unique-opened router>
                    <!-- 一级菜单 -->
                    <el-menu-item index="/select">
                        <i class="el-icon-document"></i>
                        <span slot="title">老化查询结果</span>
                    </el-menu-item>
                </el-menu>
            </el-aside>
            <el-container>
                <!-- 右侧内容主体 -->
                <el-main>
                    <!-- 路由占位符 -->
                    <router-view></router-view>
                </el-main>
            </el-container>
        </el-container>
    </el-container>
</template>

<script>
export default {
  methods: {
    logout () {
      this.$router.push('/aging')
    },
    refresh () {
      this.$router.push({ path: '/welcome' })
      const api = JSON.parse(sessionStorage.getItem('apiaddress'))
      this.$http.get(api).then(
        (result) => {
          this.$message.success('请求成功') // 此处箭头函数的作用是为了更清晰的指向Message
          sessionStorage.setItem('agingdata', JSON.stringify(result.data)) // 将接口返回值存入sessionStorage中
          // console.log(result.data)
        }
      ).catch(
        () => {
          this.$message.error('请求失败')
        }
      )
    }
  }
}
</script>

<style lang="less" scoped>
.home-container {
    height: 100%;
}

.el-header {
    background-color: #32363A;
    display: flex;
    justify-content: space-between;
    padding-left: 0;
    align-items: center;
    color: #FFFFFF;
    font-size: 25px;
    > div {
        display: flex;
        align-items: center;
        span {
            margin-left: 15px;
        }
    }
}

.el-aside {
    background-color: #545C64;
    .el-menu {
        border-right: none;
    }
}

.el-main {
    background-color: #EAEDF1;
}
</style>
