<template>
  <div id="app">
    <KanbanBoard />
  </div>
</template>

<script>
import KanbanBoard from './views/KanbanBoard.vue';

export default {
  name: 'App',
  components: {
    KanbanBoard
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #0079bf;
  margin: 0;
  padding: 0;
}

#app {
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
}

.kanban-board {
  display: flex;
  align-items: flex-start;
  padding: 20px;
}
</style>