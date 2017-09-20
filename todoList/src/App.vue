<template>
  <div id="app">
    <h1 v-text="title" class = "leftAlign"></h1>
    <p class = "leftAlign" @mouseup="clearAll(items)"><button>Clear All</button></p>
    <p class = "leftAlign"><input v-model = "newItem" @keyup.enter="addNew"  class = "leftAlign"/></p>
    <ul>

      <li class = "leftAlign" v-for="(item, index) in items" >
      <button @click = "deleteItem(index)">X</button>
      <span>&nbsp&nbsp&nbsp</span>
      <span @click = "toggleFinish(item)"
      v-bind:class="{finished:item.isFinished}" >
      {{item.label}}
      </span>
      </li>
    </ul> 
  </div>
</template>

<script>
import Store from './store'
export default {
  name: 'app',
  data: function() {
    return {
      title: 'TODOLIST',
      items:Store.fetch(),
      newItem: '',
      childWords: '',
      del:'del'
    }
  },
  methods: {
    toggleFinish: function(item) {
      console.log(item.isFinished = !item.isFinished)
    },
    addNew: function() {
      console.log(this.newItem)
      this.items.push({
        label: this.newItem,
        isFinished: false,
      })
      this.newItem = ''
    },
    clearAll: function(items) {
      this.items.splice(0,this.items.length);
    },
    deleteItem:function(index) {
      this.items.splice(index, 1);
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  }
}
</script>

<style>

.leftAlign
{
  text-align: left;
  font-size: 24px;
  font-weight: 700
}

li{
  list-style-type: none;
}

button{
  vertical-align: middle;
}

.finished{
  text-decoration : line-through;
  color:gray;
  font-weight: 100;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
