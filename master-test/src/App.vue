<template>
  <div class="container" id="app">
    <h1>Test App</h1>
    <hr />
    <div>
      <form @submit.prevent="onSubmit" class="pt-5">
        <div class="form-group row">
          <div class="col-sm-6">
            <input class="form-control" type="text" v-model="title" />
          </div>
          <button type="submit" class="ml-3 btn btn-outline-primary">
            Add text
          </button>
        </div>
      </form>
      <div v-bind:todos="todos">
        <h3
          class="text-left"
          v-bind:style="{ color: activeColor }"
          v-for="todo of todos"
          :key="todo.id"
        >
          {{ todo.title }}
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap-vue/dist/bootstrap-vue.css';
export default {
  name: 'App',
  data() {
    return {
      title: '',
      todos: [{}],
      activeColor: false,
    };
  },
  components: {},
  methods: {
    onSubmit() {
      var format = /[!@#$%^&*()_+\-={};':"\\|,.<>?]/;
      if (this.title.trim()) {
        if (this.title.length > 3) {
          this.activeColor = 'green';
        } else if (format.test(this.title)) {
          this.activeColor = 'red';
        }
        const newTodo = {
          id: Date.now(),
          title: this.title,
        };
        this.todos.push(newTodo);
        this.title = '';
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
