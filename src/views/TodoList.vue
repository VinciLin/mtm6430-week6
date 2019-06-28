<template>
  <div>
    <h1>Todo List</h1>
    <!-- add a listener , usually just<TodoForm/> -->
    <TodoForm @newTodo="addTodo">
      <h2 slot="title">Add a Todo</h2>
      <p slot="desc">Your Todos will be saved</p>
    </TodoForm>
    <!-- send info from parents todoList to child todos, todos is an attribute -->
    <Todo :todos="todoList" @removeTodo="appDeleteTodo"/>
  </div>
</template>

<script>
import Todo from "@/components/Todo.vue";
import TodoForm from "@/components/TodoForm.vue";
import axios from "axios";

export default {
  data() {
    return {
      todoList: []
    };
  },
  components: {
    Todo,
    TodoForm
  },
  methods: {
    appDeleteTodo(index) {
      this.todoList.splice(index, 1);
      axios.put(
        "https://fangyuan-vue-and-axios.firebaseio.com/data.json",
        this.todoList
      );
    },
    addTodo(todo) {
      this.todoList.push(todo);
      axios
        // send the information
        .put(
          "https://fangyuan-vue-and-axios.firebaseio.com/data.json",
          this.todoList
        )
        // whatever com back from the server
        // put not run , then will run,(response => {}) means :function (response){}
        .then(response => {
          //
          console.log(response);
          // status response
          console.log('Your data was saved status: " + response.status');
        })
        // catch the error
        .catch(error => {
          console.log(error);
        });
    }
  },

  // week 8
  // try other hook
  // beforeCreate() {
  //   console.log("before app is created");
  // },
  created() {
    axios
      .get("https://fangyuan-vue-and-axios.firebaseio.com/data.json")
      // if successful
      // arrow function, es6
      // this "response" is a response
      .then(response => {
        console.log(response.data);
        if (response.data) {
          this.todoList = response.data;
        }
      })
      // if not successful
      // "response" is a property of subject
      .catch(error => {
        console.log("There was an error in getting data:" + error.response);
      });
  }
  // beforeMount() {
  //   console.log("before app is mounted");
  // },
  // mounted() {
  //   console.log("App is mounted");
  // }
};
</script>

<style>
ul {
  list-style: none;
  width: 50%;
  margin: 0 auto;
}

ul li {
  border-bottom: 1px solid #acacac;
  padding: 10px 0;
  margin-bottom: 10px;
}
</style>