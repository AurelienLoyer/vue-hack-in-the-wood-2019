<template>
  <li class="notification" :class="{ done: item.done}">
    <button class="delete" @click="deleteTask"></button>
    {{ item.label }}
  </li>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    item: Object
  },
  methods: {
    deleteTask() {
      this.$emit("task-done", this.item);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
