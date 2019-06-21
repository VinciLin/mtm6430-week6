<template>
  <div>
    <!-- placeholder -->
    <slot name="title"></slot>
    <!-- when submit , stop to subimt to the server, instead, to run a "addTodo" method -->
    <!-- if not have an action (action means what to do with information), the page will refresh, so we need to add ".prevent" -->
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo">
    </form>
    <slot name="desc"></slot>
    <br>
    <slot>Default slot, placeholder content</slot>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // step1: linke to the newTodo above in v-model
      newTodo: ""
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length) {
        this.$emit("newTodo", this.newTodo);
        this.newTodo = "";
      }
    }
  }
};
</script>

<style >
input {
  min-width: 200px;
  padding: 10px 20px;
  font-size: 1.5rem;
}
</style>