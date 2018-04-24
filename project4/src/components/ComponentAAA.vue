<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<h2>{{ message }}</h2>
		<button v-on:click = "onClickMe">Click!</button>
	</div>
</template>

<script>
	export default{
		data:function(){
			return {
				msg:'hello form componentAAAAAAA'
			}
		},
		props:['message'],
		events:{
			'onAddNew':function(items){
				console.log(this.items)
			}
		},
		methods:{
			onClickMe:function(){
				// console.log(this.message)
				// this.$emit('chidTellMeSomething',this.msg);
				this.$dispatch('chidTellMeSomething',this.msg);
			}
		}
	}
</script>

<style>
	h1{
		color:pink;
	}
</style>