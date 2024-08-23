<template>
  <div class="board-column">
    <h2>{{ title }}</h2>
    <div class="tasks">
      <draggable
        :list="tasks"
        group="tasks"
        @end="onEnd"
        @change="onChange"
      >
        <TaskCard
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          :column-name="title"
          @update-description="updateDescription"
          @update-name="updateName"
        />
      </draggable>
    </div>
    <button class="add-task" @click="addTask">+ Add another card</button>
  </div>
</template>

<script>
import TaskCard from './TaskCard.vue';
import { VueDraggableNext } from "vue-draggable-next";

export default {
  name: 'BoardColumn',
  components: {
    TaskCard,
    draggable: VueDraggableNext
  },
  props: {
    title: String,
    tasks: Array
  },
  methods: {
    addTask() {
      const newTask = { id: Date.now(), name: 'New Task', description: '' };
      // eslint-disable-next-line vue/no-mutating-props
      this.tasks.push(newTask);
    },
    onEnd(event) {
      this.$emit('update-ttasks', event);
    },
    onChange(event) {
      this.$emit('change-tasks', event);
    },
    updateDescription(taskId, description) {
      this.$emit('update-description', taskId, description);
    },
    updateName(taskId, name) {
      this.$emit('update-name', taskId, name);
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
</style>