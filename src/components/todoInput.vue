<template lang="pug">
  .todo-input
    div.error {{validation.firstError('todo.name')}}
    input(
      type="text"
      placeholder="Todo Name"
      autofocus
      v-model="todo.name"
      @keydown.enter="addNewTodo"
      :class="{'valid-error' : validation.hasError('todo.name')}"
    ).input
    button.button(
    v-if="todos.length!==0"
    @click="checkAllItems"
    ) ❯
</template>

<script>
import { Validator } from "simple-vue-validator"
import {mapMutations} from "vuex"

let uniqId = 0;
export default {
  mixins: [require('simple-vue-validator').mixin],
  validators: {
    'todo.name'(value){
      return Validator.value(value).required('Поле не может быть пустым')
    }
  },
  props: {
    todos: Array
  },
  data(){
    return {
      todo: {
        id: 0,
        name: "",
        checked: false
      }
    }
  },
  methods: {
    ...mapMutations(['addTodo', 'checkAll']),
    addNewTodo(){
      this.$validate().then(success=>{
        if(!success) return;

        uniqId++;
        this.todo.id = uniqId;
        this.addTodo({...this.todo});
        this.todo.name="";
        this.validation.reset()
      })
    },
    checkAllItems(){
      this.checkAll();
    }
  }
}
</script>

<style lang="scss" scoped>
  .todo-input {
    position: relative;
  }

  .error {
    position: absolute;
    top: -30px;
    color: firebrick;
  }

  .button {
    width: 60px;
    height: 34px;
    position: absolute;
    top: 19px;
    left: -2px;
    transform: rotate(90deg);
    font-size: 22px;
    color: #e6e6e6;
    padding: -2px 27px 10px 27px;
    outline: none;
    background: none;
    border: none;
    cursor: pointer;
    &:hover {
      color: #737373
    }
  }

  .input {
    font-size: 24px;
    padding: 16px 16px 16px 60px;
    background: rgba(0,0,0,0.003);
    box-shadow: inset 0 -2px 1px rgba(0,0,0,0.003);
    line-height: 1.4em;
    outline: none;
    color: inherit;
    width: 100%;
    background: #fff;
    border: 1px solid transparent;
  }

  .valid-error {
    border: 1px solid firebrick;
  }
</style>
