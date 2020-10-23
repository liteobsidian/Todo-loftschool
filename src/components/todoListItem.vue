<template lang="pug">
  .todo-item(:class="{checked: todo.checked}")
    label.label
      .input-block
        input(
          type="checkbox"
          @change="checkItTodo"
          :checked="todo.checked"
        ).input
      .title {{todo.name}}
    .button
      router-link(
        tag="button"
        :to="`/view/${todo.name}`"
      ).view →
    .button
      button(
        type="button"
        @click="removeExistedTodo"
      ).remove x
</template>

<script>
import {mapMutations} from "vuex"
export default {
  props: {
    todo: Object
  },
  methods: {
    ...mapMutations(['removeTodo', 'checkTodo']),
    removeExistedTodo(){
      this.removeTodo(this.todo.id)
    },
    checkItTodo(e){
      const todoItem = {
        ...this.todo,
        checked: e.target.checked
      };
      this.checkTodo(todoItem)
    }
  },
  name: "todoListItem"
}
</script>

<style lang="scss" scoped>
  .todo-item {
    display: flex;
    align-items: center;

    &:hover {
      .remove {
        visibility: visible;
      }
      .view {
        visibility: visible;
      }
    }
  }

  .checked {
    text-decoration: line-through;
    color: #d9d9d9;
    transition: color 0.4s;
  }

  .label {
    display: flex;
    align-items: center;
    flex: 1;
  }

  .input-block {
    width: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .title {
    padding: 15px 0;
    display: block;
    line-height: 1.2;
  }

  .button {
    width: 40px;
  }

  .view {
    visibility: hidden;
    cursor: pointer;
    outline: none;
    border: 1px solid rgba(136, 112, 112, 0.2);
    background: none;
    transition: color .2s;
    color: #a2a2a2;
    font-weight: 700;
    &:hover {
      color: #737373;
    }
  }

  .remove {
    background: transparent;
    border: none;
    color: firebrick;
    cursor: pointer;
    font-size: 20px;
    visibility: hidden;
  }
</style>
