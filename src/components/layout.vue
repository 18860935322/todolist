<template>
<el-container style="height: 750px; border: 1px solid #eee">
  <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
    <menus></menus>
  </el-aside>

  <el-container>
    <el-header style="text-align: right; font-size: 12px; background-color: #fff">
      <el-dropdown>
        <i class="el-icon-setting" style="margin-right: 15px"></i>
        <el-button @click="toLogin" type="danger" plain>注销</el-button>
      </el-dropdown>
    </el-header>
    <el-main>

      <todo></todo>
    </el-main>
  </el-container>
</el-container>
</template>

<script>
import todo from './todo'
import menus from './menus'

export default {

  components: {
    todo,
    menus
  },
  methods: {
    toLogin() {
      this.$router.push('/');
    }
  }

}


</script>

<style>


</style>
