<template>
<div>
	<div class="form-group">
    <input v-model=searchinfo type="text" @keyup.enter="searchbytext" class="form-control"  placeholder="搜索">
  </div>

	<b-modal ref="myModalRef" hide-footer title="Using Component Methods">
    <div class="d-block text-center">
      <b-form-input v-model="newText"
                  type="text"
                  placeholder="输入事项名称" @keyup.enter="addItem"></b-form-input>
      <b-form-select v-model="selected" class="mb-3">
	      <option v-for="list in lists" :value="list.title">{{ list.title }}</option>
	    </b-form-select>
    </div>
    <b-btn class="mt-3" variant="outline-danger" block @click="addItem">确定</b-btn>
  </b-modal>

  <table style="width: 100%;background-color: #fff">
	    <thead>
	    <tr>
	    	<th>操作</th>
        <th>名称</th>
        <th>日期</th>
        <th>是否完成</th>
        <th>编辑</th>
        <th>删除</th>
	    </tr>
	    </thead>
	    <tbody>
	    <tr style="height: 65px" v-for="(item,index) in items">
	        <td>
	        	<input @change="editItem(item)" v-model="item.isfinished" class="form-check-input" type="checkbox" value="option1">
	        </td>
	        <td>
					<span v-if="!isupdate&&item.isfinished"style="text-decoration:underline;color:red">{{item.text}}</span>
						</span>
						<span v-if="!isupdate&&!item.isfinished">{{item.text}}</span>
	        	<span v-if="isupdate">
	        		<input @keyup.enter="isupdate = false" type="text" name="" value="item.text" v-model="item.text">
	        	</span>
	        </td>
	        <td>{{ item.date }}</td>
	        <td>
	        	<span v-if="item.isfinished">已完成</span>
	        	<span v-if="!item.isfinished">未完成</span>
		      </td>
	        <td>
	        	<a href="#" @click="isupdate = true">编辑</a>
	        </td>
	        <td>
	        	<a href="#" @click="deleteItem(item.text)">删除</a>
	        </td>
	    </tr>
	    </tbody>
	</table>

    <button @click="showModal" class="btn btn-primary btn-lg">
           新建待办事项
     </button>

</div>

</template>

<script>
import bus from '../assets/eventBus'

const toLower = text => {
  return text.toString().toLowerCase()
}

const searchByName = (items, term) => {
  if (term) {
    return items.filter(item => toLower(item.text).includes(toLower(term)))
  }
  return items
}

export default {

data() {
		return {
			title: 'all',
			newText: '',
			selected: '请选择清单',
			items: [],
			searchinfo: '',
			dialogVisible: false,
			isupdate: false
		}
	},
	created() {
    this.init();
  },
	computed: {
		lists() {
			return this.$store.getters.lists;
		}
	},
	methods: {
		init() {
			if (this.title === 'all') {
				this.items = this.$store.getters.items
			}else {
				this.items = this.$store.getters.getItemsbytitle(this.title);
			}
		},
		showModal () {
      this.$refs.myModalRef.show()
    },
    hideModal () {
      this.$refs.myModalRef.hide()
    },
		addItem() {
			let newItem = {
				text: this.newText,
				date: new Date(),
				belongto: this.selected,
				isfinished: false,
			}
			console.log(newItem.belongto)
			this.$store.commit('addItem', newItem);
			this.newText  ="";
			this.dialogVisible = false;
			this.hideModal();
		},
		deleteItem(text) {
      this.$store.commit('deleteItem', text);
      this.init()
    },
    searchbytext() {
    	this.items = searchByName(this.$store.getters.items, this.searchinfo);
    },
    editItem(item) {
    	this.$store.commit('editItem', item);
    }
	},
	mounted() {
    var self = this;
    bus.$on('LIstTitle', function(msg) {
        self.title = msg;
        self.init()
    });
  }

}


</script>

<style>

</style>
