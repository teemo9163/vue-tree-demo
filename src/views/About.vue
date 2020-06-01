<template>
  <div class="about">
	  <tree-item
		  :item="treeData"
		  @make-folder="makeFolder"
		  @add-item="addItem"
	  />
  </div>
</template>

<script>
	import TreeItem from '../components/tree-item'
	export default {
		components: {
			TreeItem
		},
		data() {
			return {
				treeData: {
					name: "My Tree",
					children: [
						{name: "hello"},
						{name: "wat"},
						{
							name: "child folder",
							children: [
								{
									name: "child folder",
									children: [{name: "hello"}, {name: "wat"}]
								},
								{name: "hello"},
								{name: "wat"},
								{
									name: "child folder",
									children: [{name: "hello"}, {name: "wat"}]
								}
							]
						}
					]
				}
			}
		},
		methods: {
			makeFolder: function (item) {
				Vue.set(item, "children", []);
				this.addItem(item);
			},
			addItem: function (item) {
				item.children.push({
					name: "new stuff"
				});
			}
		}
	}
</script>
