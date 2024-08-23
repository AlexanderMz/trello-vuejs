<template>
  <div class="kanban-board">
    <BoardColumn
      v-for="(column, index) in columns"
      :key="index"
      :title="column.name"
      :tasks="column.tasks"
      @update-tasks="updateTasks"
      @change-tasks="changeTasks"
      @update-description="updateTaskDescription"
      @update-tags="updateTaskTags"
      @update-name="updateTaskName"
    />
  </div>
</template>

<script>
import BoardColumn from './../components/BoardColumn.vue';

export default {
  name: 'KanbanBoard',
  components: {
    BoardColumn
  },
  data() {
    return {
      columns: [
        {
          name: 'To Do',
          tasks: [
            { id: 1, name: 'Task 1', description: '', tags: [{ name: 'Urgent', color: '#eb5a46' }] },
            { id: 2, name: 'Task 2', description: '', tags: [{ name: 'Low', color: '#0079bf' }] }
          ]
        },
        {
          name: 'In Progress',
          tasks: [
            { id: 3, name: 'Task 3', description: '', tags: [{ name: 'Medium', color: '#ff9f1a' }] }
          ]
        },
        {
          name: 'Done',
          tasks: [
            { id: 4, name: 'Task 4', description: '', tags: [{ name: 'Completed', color: '#f2d600' }] }
          ]
        }
      ]
    };
  },
  methods: {
    updateTasks(event) {
      console.log('Tasks updated', event);
    },
    changeTasks(event) {
      console.log('Tasks changed', event);
    },
    updateTaskDescription(taskId, description) {
      for (const column of this.columns) {
        const task = column.tasks.find(task => task.id === taskId);
        if (task) {
          task.description = description;
          break;
        }
      }
    },
    updateTaskTags(taskId, tags) {
      for (const column of this.columns) {
        const task = column.tasks.find(task => task.id === taskId);
        if (task) {
          task.tags = tags;
          break;
        }
      }
    },
    updateTaskName(taskId, name) {
      for (const column of this.columns) {
        const task = column.tasks.find(task => task.id === taskId);
        if (task) {
          task.name = name;
          break;
        }
      }
    }
  }
};
</script>

<style scoped>
.kanban-board {
  display: flex;
  flex-direction: row;
}
</style>