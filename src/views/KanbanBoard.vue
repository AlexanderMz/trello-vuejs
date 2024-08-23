<template>
    <div class="kanban-board">
      <BoardColumn
        v-for="(column, index) in columns"
        :key="column.id"
        :title="column.title"
        :tasks="column.tasks"
        @dragstart="onDragStart"
        @drop="onDrop(column, index)"
      />
    </div>
  </template>
  
  <script>
  import BoardColumn from '../components/BoardColumn.vue';
  
  export default {
    name: 'KanbanBoard',
    components: {
      BoardColumn
    },
    data() {
      return {
        columns: [
          { id: 1, title: 'To Do', tasks: [{ id: 1, title: 'Task 1' }, { id: 2, title: 'Task 2' }] },
          { id: 2, title: 'In Progress', tasks: [{ id: 3, title: 'Task 3' }] },
          { id: 3, title: 'Done', tasks: [{ id: 4, title: 'Task 4' }] }
        ],
        draggedTask: null,
        draggedColumnIndex: null,
        taskActive: {}
      };
    },
    methods: {
      onDragStart(task) {
        if(task)
          console.log(task)
        
          this.taskActive = task;
      },
      onDrop(targetColumn) {
        console.log(this.$emit('drop'))
        console.log(this.taskActive)
        if (this.draggedTask && this.draggedTask !== targetColumn.tasks) {
          // Remueve la tarea de la columna original
          this.columns.forEach(column => {
            const index = column.tasks.indexOf(this.draggedTask);
            if (index > -1) {
              column.tasks.splice(index, 1);
            }
          });
          // Añade la tarea a la nueva columna
          console.log(this.draggedTask)
          targetColumn.tasks.push(this.draggedTask);
          this.draggedTask = null;
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .kanban-board {
    display: flex;
    align-items: flex-start;
    overflow-x: auto;
    padding: 10px;
    background-color: #0079bf;
    border-radius: 3px;
  }
  </style>
  