<template>
  <li>
      <span
        @click="selectItem"
        :class="['item-row', {'item-row_active': isActiveItem}]"
      >
        <i
          @click="toggleExpand"
          v-show="isFullContents"
          :class="['item-row__icon', 'fa', 'fa-angle-right', {'item-row__icon_rotate': isExpand}]"
        />
        <i class="item-row__icon fas fa-folder"></i>
        {{name}}
      </span>
  </li>
</template>

<script>
export default {
  name: 'DirectoryItem',
  props: {
    name: {
      type: String,
      default: '',
    },
    isExpand: {
      type: Boolean,
      default: false,
    },
    isFullContents: {
      type: Boolean,
      default: false,
    },
    id: {
      type: String,
      default: '',
    },
    path: {
      type: String,
      default: '',
    },
    currentItem: {
      type: String,
      default: '',
    }
  },
  computed: {
    isActiveItem() {
      return this.currentItem === this.id;
    }
  },
  methods: {
    toggleExpand(event) {
      event.preventDefault();
      this.$emit('toggleExpand')
    },
    selectItem() {
      this.$root.$emit('selectItem', {id: this.id, path: this.path})
    }
  }
}
</script>

<style scoped src="../index.css"></style>



