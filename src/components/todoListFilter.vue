<template lang="pug">
  div
    button(
      v-for="filter in filters"
      :class="{active: currentFilter===filter}"
      @click="filterAllTodos(filter)"
      type='button'
      ) {{filter}}
</template>

<script>
import {mapMutations} from "vuex";

export default {
  data(){
    return{
      filters: ['All', 'Active', 'Completed'],
      currentFilter: 'All'
    }
  },
  methods:{
    ...mapMutations(['filterTodos']),
    filterAllTodos(filter){
      this.currentFilter = filter;
      this.filterTodos(filter);
    }
  }
}
</script>

<style lang="scss" scoped>
  button{
    margin-right: 20px;
    background: transparent;
    font-weight: 300;
    color: inherit;
    cursor: pointer;
    border: 1px solid transparent;;
    border-radius: 3px;
    outline: none;
    &.active {
      border-color: rgba(175, 47, 47, 0.2);
    }

    &:last-child {
      margin-right: 0;
    }
  }
</style>
