<template>
  <ul>
    <!-- previous
        <li>Walk the Dogs</li>
    <li>Go for ride</li>-->
    <!-- :key to track; click event -->
    <li v-for="(todo, index) in todos" :key="index" @click="todoDone(index)">{{ todo }}</li>
  </ul>
</template>
<script>
export default {
  // simply way
  // props:['todos']

  // advanced way: prop validation
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  methods: {
    //   will print out in the console
    todoDone(index) {
      console.log(index);
      // week 6 , $emit emits an event from child component to the parent
      this.$emit("removeTodo", index);
    }
  }
};
</script>