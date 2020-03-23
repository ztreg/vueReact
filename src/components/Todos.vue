Kompontenten som hanterar hela "todo".
<template>
  <div>
    <h1>Template för Todos</h1>
    <!-- Tar in från props. Behöver lägga till en key till varje item,
    varje specifik todoitems id -->
    <div v-bind:key="todoItem.id" v-for="todoItem in todoItemsen">
        <h4><TodoItem v-bind:todoItem="todoItem" v-on:del-todoItem="$emit('del-todoItem', todoItem.id)"/></h4>
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
name : "Todos",
components: {
TodoItem
},
props : ["todoItemsen"]
}
</script>



<style scoped>

</style>
