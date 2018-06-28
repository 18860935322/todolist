<template>

<div class="app-location">

  <b-modal ref="myModalRef" hide-footer title="Using Component Methods">
    <div class="d-block text-center">
      信息输入有误！
    </div>
    <b-btn class="mt-3" variant="outline-danger" block @click="hideModal">确定</b-btn>
  </b-modal>
  <el-row style="padding-top: 250px">
      <el-col :span="24">
        <div style="width: 400px;margin: auto">
    <h1>欢迎登录</h1>
    <el-input style="margin-bottom: 10px" v-model="username" placeholder="用户名"></el-input>
    <el-input type="password" v-model="password" placeholder="密码"></el-input>
    <button @click="checkLogin">登陆</button>
      </div></el-col>
    </el-row>
</div>

</template>

<script>

export default{
  data() {
    return {
      username: '',
      password: '',
      isLogin: false
    }
  },
  computed: {
    users() {
      return this.$store.getters.users;
    }
  },
  methods: {
    showModal () {
      this.$refs.myModalRef.show()
    },
    hideModal () {
      this.$refs.myModalRef.hide()
    },
    checkLogin() {
        if ( this.username === 'fcy' && this.password === '123456') {
          this.$router.push('/todo');
        }else {
          this.showModal();
        }
      }
  }
}

</script>

<style>
.app-location {
  background: #00FF00 url(../assets/image/bg.jpeg) repeat fixed top;
  height: 750px
}

 .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }


</style>
