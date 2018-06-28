<template>
	<el-menu :default-openeds="['1', '3']">
    <el-submenu index="1">

    	<el-menu-item style="text-align: left" @click="goList('all')" index="1-1">
      	<i class="el-icon-tickets"></i>
      	All
      </el-menu-item>

      <el-menu-item style="text-align: left" v-for="list in lists" @click="goList(list.title)" index="1-1">
      	<i class="el-icon-tickets"></i>
      	{{ list.title }}
      </el-menu-item>

      <el-menu-item  v-if="isAdd" style="text-align: left" @click="goList(list.title)" index="1-1">
      	<input type="text" v-model="newtitle" @keyup.enter="addList" >
      </el-menu-item>
      <el-menu-item style="text-align: left" @click="isAdd = true">
      	 +添加清单
      </el-menu-item>
    </el-submenu>
  </el-menu>

</template>

<script>
import bus from '../assets/eventBus'

export default{
	data() {
		return {
			name: 'lj',
			newtitle: '',
			isAdd: false
		}
	},
	computed: {
		lists() {
			return this.$store.getters.lists;
		}
	},
	methods: {
		addList() {
			let newList = {
				title: this.newtitle,
				count: 0
			}
			this.$store.commit('addList', newList)
			this.newtitle = "";
			this.isAdd = false
		},
		goList(title) {
      bus.$emit('LIstTitle', title)
    }
	}
}

</script>

<style>
.list-style {
	background: #283643;
	color: #fff;
}


</style>
