<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<button v-on:click = "onClickMe">Click!</button>
	</div>
</template>

<script>
	export default{
		data:function(){
			return {
				msg:'hello form componentA'
			}
		},
		methods:{
			onClickMe:function(){
				
			}
		}
	}
</script>

<style>
	h1{
		color:pink;
	}
</style>