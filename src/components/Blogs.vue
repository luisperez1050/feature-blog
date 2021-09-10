<template>
	<div class="feature">
		<Editprops 
			:allProps="{
				category,
				pageProperties,
				items
				}"
			v-on:deleteItem="onDeleteItem"
			v-on:addItem="onAddItem"
		/>
		<header>
			<span class="feature-icon">
				<font-awesome-icon :icon=category.icon />
			</span>
			
			<a v-if="category.link" :href="category.link" target="_blank">
				<h1> {{ category.label }} </h1>
			</a>
			<h1 v-else> {{ category.label }} </h1>
			
		</header>
		<main :style="{ backgroundImage: `url(${pageProperties.backgroundImage})`, gridTemplateColumns: `repeat(${calculateGridColumn}, ${pageProperties.availableSpace}px)` }" >
			<section v-for="article in items.slice(0,pageProperties.displayCount)" :key="article" >
				<article :style="{ backgroundColor: pageProperties.itemBackgroundColor }">
					<span class="date-icon">
						{{ article.date }}
					</span>
					
					<a v-if="article.link" :href="article.link" target="_blank">
						<h2> {{ article.title }} </h2>
					</a>
					<h2 v-else> {{ article.title }} </h2>
					
					{{ article.text }}
				</article>
			</section>
		</main>
		
	</div>
</template>

<script>
import Editprops from './Editprops.vue'

export default {
	name: 'Blogs',
	data() {
		return {
			category: {
				label: 'Featured Blogs',
				link: 'https://www.bing.com',
				icon: 'rss'
			},
			items: [
				{
					title: 'Test Article 1',
					text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
					link: 'https://loremipsum.io/generator/',
					date: 'Aug 20'
				},
				{
					title: 'Test Article 2',
					text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
					link: 'https://developer.mozilla.org/',
					date: 'Jul 29'
				},
				{
					title: 'Test Article 3',
					text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
					link: 'https://codesandbox.io/',
					date: 'Jun 20'
				},
				{
					title: 'Test Article 4',
					text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
					link: 'https://placeholder.com',
					date: 'May 29'
				},
				{
					title: 'Test Article 5',
					text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
					link: 'https://www.ebay.com',
					date: 'Apr 20'
				},
				{
					title: 'Test Article 6',
					text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
					link: 'https://amazon.com',
					date: 'Mar 29'
				},
			],
			pageProperties: {
				backgroundImage: 'https://cdn-scor-prd-01.azureedge.net/us/institutional/-/media/aam-web/images/thinking-aloud/august-2018/1440x770_aberdeenstandard_us_consumer.ashx?modified=20190611133438',
				itemBackgroundColor: '#ffffff',
				displayCount: 4,
				availableSpace: '540'
			},

		}
	},
	components: {
		Editprops
	},
	computed: {
		calculateGridColumn: function () {
			return (this.pageProperties.availableSpace >= '550') ? '1' : '2';
		}
	},
	methods: {
		onDeleteItem(itemTitle) {
			this.items = this.items.filter( (item) => item.title !== itemTitle);
		},
		onAddItem(newItem) {
			this.items.push(newItem);
		},
		articleHeight() {
			let maxHeight = 0;
			let articles = document.querySelectorAll('article');
			
			articles.forEach( article => {
				article.style.minHeight = 'unset';

				if (article.clientHeight > maxHeight) {
					maxHeight = article.clientHeight
				}
			});
			
			articles.forEach( element => {
				element.style.minHeight = maxHeight + "px";
			});
		}
	},
	mounted() {
		this.articleHeight()

		window.addEventListener('resize', this.articleHeight)
	},
	unmounted() {
		window.removeEventListener('resize', this.articleHeight)
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.feature{
	height: 97vh;
	max-width: 1200px;
	margin: 0 auto;
}

header {
	background-color: #eaeaea;
	margin-top: 30px;
	position: relative;
}

header h1 {
	display: inline-block;
	
}

header h1 {
	margin: 0 0 6px 0 ;
	font-size: 22px;
	line-height: 1.8;
	padding-left: 100px;
	text-transform: uppercase;
}

a {
	text-decoration: none;
}

a:hover, a:focus, a:active,
a:hover h1, a:focus h1, a:active h1
 {
	text-decoration: underline;
}

header a {
	color: #000000
}

span.feature-icon {
	border-radius: 50%;
	background-color: #000000;
	color: #ffffff;
	padding: 14px;
	position: absolute;
	top: -20px;
	left: 20px;
}
.fa-rss {
	font-size: 35px;
}

main {
	background-size: cover;
	color: #4a4a4a;
	height: 84%;
	padding: 20px;
	margin-top: 8px;
	display: grid;
	grid-template-rows: 0.25fr;
	grid-gap: 20px 50px;
	justify-content: end;
}

main h2,
main span {
	text-transform: uppercase;
}

main h2{
	margin: 0;
}

section:nth-child(odd):last-child {
	grid-column: span 2;
	padding: 0 250px;
}
article {
	margin-top: 50px;
	padding: 20px;
	position: relative;
	box-sizing: border-box;
}

article a {
	color: #4a4a4a;
}


.date-icon {
	box-sizing: border-box;
	border-radius: 50%;
	background-color: #000000;
	color: #ffffff;
	font-size: 14px;
	line-height: 1.1;
	padding: 6px;
	position: absolute;
	top: -20px;
	left: -20px;
	height: 43px;
	width: 42px;
	text-align: center;
}

@media (max-width: 1200px) {
	main {
		height: unset;
		grid-template-columns: 1fr !important;
	}
}

</style>
