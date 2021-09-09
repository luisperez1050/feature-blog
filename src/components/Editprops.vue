<template>
	<div class="edit-form">
		<button v-on:click="showHideForm()">Edit Props</button>
		<form v-on:submit.prevent v-if="displayForm">
			<section>
				<label for="category_label">Category label: </label>
				<input id="category_label" type="text" v-model="allProps.category.label" />
				<label for="category_link">Category link: </label>
				<input id="category_link" type="text" v-model="allProps.category.link" />
				<label for="category_icon" title="possible icons, coffee, adjust, ad, align-center">Category icon: </label>
				<input id="category_icon" type="text" v-model="allProps.category.icon" />
			</section>
			<section>
				<label for="background_image">Background Image: </label>
				<input id="background_image" type="text" v-model="allProps.pageProperties.backgroundImage" />
				<label for="item_background">Item Background Color: </label>
				<input id="item_background" type="text" v-model="allProps.pageProperties.itemBackgroundColor" />
				<label for="display_count">Display Count: </label>
				<input id="display_count" type="text" v-model="allProps.pageProperties.displayCount" />
				<label for="available_space">Available Space: </label>
				<input id="available_space" type="text" v-model="allProps.pageProperties.availableSpace" />
			</section>
			<p>Item List</p>
			<section v-for="item in allProps.items" :key="item">
				<label for="item_title">Title: </label>
				<input id="item_title" type="text" v-model="item.title" />
				<label for="item_text">Text: </label>
				<input id="item_text" type="text" v-model="item.text" />
				<label for="item_link">Link: </label>
				<input id="item_link" type="text" v-model="item.link" />
				<label for="item_date">Date: </label>
				<input id="item_date" type="text" v-model="item.date" />
				<button v-on:click="removeItem(item.title)">Delete Item</button>
			</section>
			<p>Add New Items</p>
			<section>
				<label for="item_title">New Title: </label>
				<input id="item_title" type="text" v-model="newItem.title" />
				<label for="item_text">New Text: </label>
				<input id="item_text" type="text" v-model="newItem.text" />
				<label for="item_link">New Link: </label>
				<input id="item_link" type="text" v-model="newItem.link" />
				<label for="item_date">New Date: </label>
				<input id="item_date" type="text" v-model="newItem.date" />
				<button v-on:click="addItem(newItem)">Add New Item</button>
			</section>
		</form>
	</div>
</template>

<script>
export default {
	name: 'Editprops',
	props: {
		allProps: Object,
		backgroundProp: String
	},
	data() {
		return {
			newItem: { title:'', text:'', link:'', date:''},
			displayForm: false
		}
	},
	emits: ['deleteItem', 'addItem'],
	methods: {
		showHideForm() {
			this.displayForm = !this.displayForm
		},
		removeItem(itemTitle) {
			this.$emit('deleteItem', itemTitle)
		},
		addItem(newItem) {
			this.$emit('addItem', newItem)
			this.newItem = []
		}
	}
}
</script>

<style scoped>
form section {
	margin-top: 10px;
}

form section label {
	display: inline-block;
	width: 8%;
	text-align: end;
}

form section label,
form section input {
	margin-right: 10px;
}
</style>