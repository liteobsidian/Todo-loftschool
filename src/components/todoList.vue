<template lang="pug">
  .todo-list
    .content
      ul.list
        li.item(v-for="todo in todos" )
          todo-list-item(
            :todo="todo"
            )

    .footer
      .footer-content
        .counter {{todos.length}} items left
        .filter
          todo-list-filter
        button.clear(
          v-if="allCheck"
          @click="allItemsRemove"
        ) Clear completed
</template>

<script>
import todoListFilter from "./todoListFilter";
import todoListItem from "./todoListItem";
import {mapMutations} from "vuex"

export default {
  props: {
    todos: Array,
    allCheck: Boolean
  },
  components: {
    todoListItem,
    todoListFilter
  },
  methods: {
    ...mapMutations(['allRemove']),
    allItemsRemove(){
      this.allRemove();
    }
  }
}
</script>

<style lang="scss" scoped>
  .list {
    font-size: 24px;;
    border-bottom: 1px solid #ededed;
  }

  .item {
    border-bottom: 1px solid #ededed;
    &:last-child {
      border-bottom: none;
     }
  }

  .footer {
    color: #777;
    padding: 10px 15px;
    text-align: center;
    position: relative;
    font-size: 14px;
    &:before {
      content: '';
      position: absolute;
      right: 0;
      bottom: 0;
      left: 0;
      height: 50px;
      overflow: hidden;
      box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6, 0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6, 0 17px 2px -6px rgba(0, 0, 0, 0.2);
    }
  }

  .footer-content {
    display: flex;
    align-items: center;
    position: relative;
  }

  .filter {
    flex: 1;
  }

  .clear {
    float: right;
    position: relative;
    line-height: 20px;
    text-decoration: none;
    cursor: pointer;
    margin: 0;
    padding: 0;
    border: 0;
    background: none;
    font-size: 100%;
    vertical-align: baseline;
    font-family: inherit;
    font-weight: inherit;
    color: inherit;
    appearance: none;
  }

  .clear:hover {
    text-decoration: underline;
    cursor: pointer;
  }
</style>
