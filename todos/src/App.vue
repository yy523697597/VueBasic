/*
 * @Author: yuyi 
 * @Date: 2017-05-05 21:14:23 
 * @Last Modified by:   yuyi 
 * @Last Modified time: 2017-05-05 21:14:23 
 */


<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ol>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">{{item.label}}</li>
    </ol>
  </div>
</template>

<script>
import Store from './store.js';
console.log(Store)
export default {
  data: function () {
    return {
      title: '这是一个 todo 列表',
      items: Store.fetch(),
      newItem: ''

    }

  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items);
      },
      deep: true
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished;
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      });
      this.newItem = '';

    }
  }
}
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

.finished {
  text-decoration: line-through;
  color: green;
}

input {
  width: 300px;
  height: 30px;
  border-radius: 5px;
}

li {
  font-size: 20px;
  text-align: center;
  width: 150px;
  margin: 0 auto;
  color: red;
  cursor: pointer;
}
</style>
