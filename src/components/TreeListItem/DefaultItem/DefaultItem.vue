<template>
  <li @click="selectItem" >
      <span :class="['item-row', {'item-row_active': isActiveItem}]">
        <i :class="iconClasses" />
        {{name}}
      </span>
  </li>
</template>

<script>
export default {
  name: 'DefaultItem',
  props: {
    name: {
      type: String,
      default: '',
    },
    id: {
      type: String,
      default: '',
    },
    path: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      default: '',
    },
    currentItem: {
      type: String,
      default: '',
    }
  },
  computed: {
    iconClasses() {
       const classes = ['item-row__icon', 'fas',];
       this.type === 'file'
           ? classes.push('fa-file-alt')
           : classes.push('fa-link')

       return classes;
    },
    isActiveItem() {
      return this.currentItem === this.id;
    }
  },
  methods: {
    selectItem() {
      this.$root.$emit('selectItem', {id: this.id, path: this.path})
    }
  }
}
</script>

<style scoped src="../index.css"></style>




