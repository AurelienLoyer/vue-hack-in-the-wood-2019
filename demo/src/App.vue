<template>
  <section class="section">
    <div class="container">
      <h1 class="title">My TODO List</h1>
      <div class="field">
        <div class="control">
          <input
            class="input"
            type="text"
            placeholder="Search"
            v-model="newTask"
            v-on:keyup.enter="submit"
          />
        </div>
      </div>
      <ul>
        <Task v-for="task of tasks" :item="task" :key="task.id" @task-done="updateTask" />
      </ul>
      <footer class="footer" style="margin-top: 2em;">
        <div class="content has-text-centered">
          <p>
            <strong>My TODO List</strong> by
            <a href="https://twitter.com/emmanueldemey">Emmanuel DEMEY</a> and
            <a href="https://twitter.com/AurelienLoyer">Aurelien LOYER</a>
          </p>
        </div>
      </footer>
    </div>
  </section>
</template>

<script>
import Task from "./components/Task";
import firebase from "firebase";

const db = firebase.initializeApp(require("./config.json")).firestore();

export default {
  name: "app",

  firestore: {
    tasks: db.collection("todos")
  },
  data() {
    return {
      newTask: "",
      tasks: [
        { id: 0, label: "speak to Hack in woods", done: false },
        { id: 1, label: "CFP DevDays", done: false }
      ]
    };
  },
  components: {
    Task
  },
  methods: {
    submit() {
      this.tasks.push();
      db.collection("todos").add({
        label: this.newTask,
        done: false
      });
      this.newTask = "";
    },
    updateTask(task) {
      db.collection("todos")
        .doc(task.id)
        .set({
          ...task,
          done: !task.done
        });
    }
  }
};
</script>

<style>
</style>
