<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <!-- {{title}} -->
    <h2 v-html='shuoming'></h2>
    <input v-model="newItem" v-on:keyup.enter="addItem">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}"
       v-on:click="toggleFinished(item)">
        {{item.label}}
      </li>
    </ul>
    <p>child tells me {{ childWords }}</p>
    <component-a></component-a>
    <ComponentAAA message="hi child" v-on:chidTellMeSomething = 'ListenToMyBoy'></ComponentAAA>
  </div>
</template>


<script>
import Store from './store.js'
import componentA from './components/componentA.vue'
import ComponentAAA from './components/ComponentAAA'
export default {
  name: 'App',
  data:function(){
    return {
      title:'This is a todolist',
      shuoming:'<em>hi liming</em>',
      items:Store.fetch(),
      newItem : '',
      childWords:''
    }
  },
  components:{
    componentA,ComponentAAA
  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items)
      },
      deep:true
    }
  },
  events:{
    'chidTellMeSomething':function(msg){
        this.childWords = msg;
    }
  },
  methods:{
    toggleFinished:function(item){
      item.isFinished = !item.isFinished
    },
     addItem:function(){
      this.items.push(
        {
          label:this.newItem,
          isFinished:false
        }
      )
      this.newItem =''
      this.$broadcast('onAddNew',this.items);
      
    },
    ListenToMyBoy:function(msg){
      this.childWords = msg
    }
  }
}
// new Vue({
//   el:'#app',
//   data:{
//     title:'this is a 666666666666'
//   }
// })

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished{
  text-decoration: underline;
  color: pink;
}
</style>
