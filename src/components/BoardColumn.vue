<template>
    <div class="board-column">
      <h2>{{ title }}</h2>
      <div 
        class="tasks" 
        @drop.prevent="onDrop" 
        @dragover.prevent
      >
        <TaskCard
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          @dragstart="onDragStart(task)"
        />
      </div>
      <button class="add-task" @click="addTask">+ Add another card</button>
    </div>
  </template>
  
  <script>
  import TaskCard from './TaskCard.vue';
  
  export default {
    name: 'BoardColumn',
    components: {
      TaskCard
    },
    props: {
      title: String,
      tasks: Array
    },
    methods: {
      onDragStart(task) {
        // Emitimos el evento de inicio de arrastre
        this.$emit('dragstart', task);
      },
      onDrop() {
        // Emitimos el evento de drop
        this.$emit('drop', this.tasks);
      },
      addTask() {
        const newTask = { id: Date.now(), title: 'New Task' };
        // eslint-disable-next-line vue/no-mutating-props
        this.tasks.push(newTask);
      }
    }
  };
  </script>
  
  <style scoped>
  .board-column {
    background-color: #ebecf0;
    padding: 10px;
    border-radius: 5px;
    width: 272px;
    margin-right: 20px;
    display: flex;
    flex-direction: column;
  }
  
  h2 {
    font-size: 14px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .tasks {
    flex-grow: 1;
    min-height: 100px;
    margin-bottom: 10px;
  }
  
  .add-task {
    background-color: transparent;
    border: none;
    color: #5e6c84;
    text-align: left;
    padding: 8px;
    font-size: 14px;
    cursor: pointer;
  }
  
  .add-task:hover {
    background-color: rgba(9, 30, 66, 0.08);
    border-radius: 3px;
  }
  </style>
  