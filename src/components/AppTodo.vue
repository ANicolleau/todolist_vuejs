<template>
  <table>
    <td>{{ todoTitle }}</td>
    <td>{{ todoHour }}</td>
    <td>{{ todoWorker }}</td>
    <slot/>
  </table>
</template>

<script>
export default {
  name: "AppTodo",
  props: {
    "todoTitle": String,
    "todoHour": Number,
    "todoWorker": String
  }
}
</script>

<style scoped>

</style>