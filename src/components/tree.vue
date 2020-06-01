<template>
	<ul class="tree-list">
		<li class="content">
			<div
				class="text"
				@click="toggle(item)"
				@dblclick="toggle(item)">
				{{ item.name }}
				<span v-if="item.hasChildren">[{{ item.isOpen ? '-' : '+' }}]</span>
			</div>
			<div class="next-tree" v-show="item.hasChildren && item.isOpen">
				<tree
					v-for="(child, index) in item.children"
					:key="index"
					:item="child"
					@load="emitLoad"
				/>
			</div>
		</li>
	</ul>
</template>

<script>
	export default {
		name: "tree",
		props: {
			item: Object
		},
		data: function() {
			return {
			};
		},
		created() {
			if (!this.item.isOpen) {
				this.$set(this.item, 'isOpen', false)
			}
		},
		methods: {
			emitLoad(node, resolve) {
				console.log(node)
				console.log(resolve)
				this.$emit('load', node, resolve);

			},
			toggle(node) {
				console.log(node)
				// 没有子节点
				if (!node.hasChildren) return;
				// 有现成的子节点
				if (node.children && node.children.length > 0) {
					node.isOpen = !node.isOpen;
					return
				}
				const emitResolve = (arr) => {
					console.log('arr', arr)
					this.$set(node, 'children', []);
					node.children = arr;
					node.isOpen = true;
				};
				// 懒加载子节点
				this.$emit('load', this.item, emitResolve);
			}
		}
	}
</script>

<style lang="scss">
	.tree-list {
		border: 2px solid cyan;
		padding: 5px;
		margin: 5px;
		.content {
			.text {
				cursor: pointer;
			}
		}
	}
	ul, li {
		list-style: none;
	}
</style>