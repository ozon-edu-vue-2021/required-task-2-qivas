<template>
    <li>
      <directory-item
        v-if="item.type==='directory'"
        @toggleExpand="toggleExpand"
        :isExpand="isExpand"
        :isFullContents="isFullContents"
        :name="item.name"
        :id="id"
        :path="path"
        :currentItem="currentItem"
      />
      <default-item
        v-else
        :type="item.type"
        :isFullContents="isFullContents"
        :name="item.name"
        :id="id"
        :path="path"
        :currentItem="currentItem"
      />
      <ul v-if="isFullContents && isExpand">
        <tree-list-item
          v-for="(subItem, i) in item.contents"
          :key="`${subItem.name}_ ${i}`"
          :id="`${subItem.name}_ ${i}`"
          :item="subItem"
          :path="`${path}/${subItem.name}`"
          :currentItem="currentItem"
        />
      </ul>
    </li>
</template>

<script>
import DirectoryItem from './DirectoryItem/DirectoryItem';
import DefaultItem from './DefaultItem/DefaultItem';
export default {
  name: 'TreeListItem',
  components: {DirectoryItem, DefaultItem},
  props: ['item', 'currentItem', 'id', 'path'],
  data() {
    return {
      isExpand: false,
      isActive: false,
    }
  },
  computed: {
    isFullContents() {
      return this.item.contents && this.item.contents.length > 0
    }
  },
  methods: {
    toggleExpand() {
      this.isExpand = !this.isExpand;
    },
    selectItem(id) {
      this.$root.$emit('selectItem', id)
    }
  }
}
</script>

<style scoped src="./index.css"></style>




