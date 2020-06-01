<template>
  <div class="home">

	  多个一级菜单循环
		<tree
			v-for="(item, index) in treeList"
			:key="index"
			:item="item"
			@load="onLoad"
		/>

	  单个一级菜单
	  <tree
		  :item="treeData"
		  @load="onLoad"
	  />

  </div>
</template>

<script>
	import TreeItem from '../components/tree-item'
	import Tree from '../components/tree'
	export default {
		name: 'Home',
		components: {
			TreeItem,
			Tree
		},
		data () {
			return {
				treeList: [{
					name: '一级菜单1',
					hasChildren: true
				}, {
					name: '一级菜单2',
					hasChildren: true,
					children: [{
						name: '二级菜单1',
						hasChildren: false
					}]
				}],
				treeData: {
					name: '一级菜单1',
					hasChildren: true
				}


			}
		},
		methods: {
			// 懒加载
			onLoad(node, resolve) {
				setTimeout(() => {
					const data = [{
						name: 'leaf',
						hasChildren: true
					}, {
						name: 'zone',
						hasChildren: false
					}];
					resolve(data);
				}, 300);
			}
		}
	}
</script>

<style lang="scss">
	ul,li {
		margin: 0;
		padding: 0;
	}
</style>
