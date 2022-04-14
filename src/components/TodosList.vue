<template>
  <h1>
    {{ todoListTitle }}
  </h1>
  <span>
    {{ getErrors }}
  </span>
  <input id="id-todo-title" placeholder="Titre de ma Todo" v-model="todoTitle"/>
  <input id="id-todo-hour" type="number" v-model="nbHour"/>
  <select id="id-todo-worker" v-model="workerSelected">
    <option value=""></option>
    <option value="Hercule">Hercule</option>
    <option value="Peter Pan">Peter Pan</option>
    <option value="Harry Potter">Harry Potter</option>
  </select>
  <button type="submit" @click="checkForm()">Ajouter</button>
  <AppTodo :key="todo.todoTitle" :todo-title="todo.todoTitle" :todo-hour="todo.todoHour" :todo-worker="todo.todoWorker"
           v-for="todo in todos"
           v-bind:is="todo">
    <button @click="deleteTodo(todos.indexOf(todo))">Supprimer la Tache</button>
    <button @click="editTodo(todos.indexOf(todo))">Editer cette Tache</button>

  </AppTodo>
</template>

<script>
import AppTodo from "@/components/AppTodo";

export default {
  name: "TodosList",
  components: {AppTodo},
  props: {
    todoListTitle: String
  },
  data: function () {
    return {
      toId: 0,
      todoTitle: '',
      nbHour: 0,
      workerSelected: '',
      errors: [],
      todos: []
    }
  },
  computed: {
    getErrors: function () {
      return this.errors.join(", ")
    }
  },
  methods: {
    checkForm: function () {
      this.errors = [];

      if (!this.todoTitle) {
        this.errors.push("Titre de la tache requis");
      }
      if (this.errors.length) {
        return true;
      }

      this.addTodo(this.todoTitle, this.nbHour, this.workerSelected)
    },
    addTodo: function (todoTitle, todoHour, todoWorker) {
      this.todos.push({
        todoTitle: todoTitle,
        todoHour: todoHour,
        todoWorker: todoWorker
      })
    },
    deleteTodo: function (index) {
      this.todos.splice(index, 1);
    },

    editTodo: function (index) {
      const updateFormPromise = new Promise(() => {
        const myTodo = this.todos[index]
        document.getElementById("id-todo-title").value = myTodo.todoTitle;
        document.getElementById("id-todo-hour").value = myTodo.todoHour;
        document.getElementById("id-todo-worker").value = myTodo.todoWorker;
      })
      updateFormPromise.then(() => {
        this.deleteTodo(index);
      })
    }
  },
}

</script>

<style scoped>

</style>