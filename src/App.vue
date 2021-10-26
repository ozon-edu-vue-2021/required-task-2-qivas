<template>
  <div id="app">
    <h3>Homework 2</h3>
    <p class="filepath">filepath: {{path}}</p>
    <ul>
      <tree-list-item
        v-for="(item, i) in items"
        :key="`${item.name}_${i}`"
        :id="`${item.name}_${i}`"
        :item="item"
        :path="`/${item.name}`"
        :currentItem="currentItem"
        @selectItem="onSelect"
      />
    </ul>
  </div>
</template>

<script>
import TreeListItem from './components/TreeListItem/TreeListItem';
import structure from '../public/static/node_modules.json'

export default {
  name: 'App',
  components: {
    TreeListItem,
  },
  data() {
    return {
      items: structure.contents,
      currentItem: null,
      path: '',
    }
  },
  created() {
    this.$root.$on('selectItem', ({id, path}) => {
      this.onSelect(id)
      this.path = path;
    })
  },
  methods: {
    onSelect(itemId) {
      this.currentItem = itemId;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 40px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: baseline;
  justify-content: flex-start;
  flex-direction: column;
  margin-bottom: 8px;
  font-size: 24px;
}

.filepath {
  text-align: left;
  margin: 16px 0 24px;
}

</style>