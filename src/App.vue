<template>
  <div id="app">
    <Blogs />
  </div>
</template>

<script>
import Blogs from './components/Blogs.vue'

export default {
  name: 'App',
  components: {
    Blogs
  }
}
</script>

<style>
body {
	font-family: 'PT Sans Narrow', sans-serif;
	margin: 10px;
}
</style>
