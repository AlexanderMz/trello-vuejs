<template>
    <div class="task-card">
        <div class="task-name" @click="toggleEditName" v-if="!isEditingName">{{ task.name }}</div>
        <input v-else v-model="taskName" @blur="updateName" @keyup.enter="updateName" class="task-name-input" />
        <div class="task-tags">
        <span
          v-for="(tag, index) in task.tags"
          :key="index"
          :style="{ backgroundColor: tag.color }"
          class="task-tag"
          @click="changeTagColor(index)"
        >
          {{ tag.name }}
        </span>
      </div>
      <div class="task-description" @click="toggleEditDescription" v-if="!isEditingDescription">{{ task.description || 'Click to add description' }}</div>
      <textarea class="task-textarea" v-else v-model="taskDescription" @blur="updateDescription"></textarea>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TaskCard',
    props: {
      task: Object,
      columnName: String
    },
    data() {
      return {
        isEditingName: false,
        isEditingDescription: false,
        taskName: this.task.name,
        taskDescription: this.task.description
      };
    },
    methods: {
    toggleEditName() {
      this.isEditingName = true;
    },
    updateName() {
      this.isEditingName = false;
      this.$emit('update-name', this.task.id, this.taskName);
    },
    toggleEditDescription() {
      this.isEditingDescription = true;
    },
    updateDescription() {
      this.isEditingDescription = false;
      this.$emit('update-description', this.task.id, this.taskDescription);
    },
      changeTagColor(index) {
        const colorNameMap = {
          '#c377e0': 'Urgent',
          '#0079bf': 'Low',
          '#ff9f1a': 'Medium',
          '#eb5a46': 'High',
          //'#c377e0': 'Optional',
         // '#0079bf': 'Completed' f2d600
        };
        const colors = Object.keys(colorNameMap);
        const currentColor = this.task.tags[index].color;
        const currentIndex = colors.indexOf(currentColor);
        const nextIndex = (currentIndex + 1) % colors.length;
        const nextColor = colors[nextIndex];
        const nextName = colorNameMap[nextColor];
        // eslint-disable-next-line vue/no-mutating-props
        this.task.tags[index].color = nextColor;
        // eslint-disable-next-line vue/no-mutating-props
        this.task.tags[index].name = nextName;
        this.$emit('update-tags', this.task.id, this.task.tags);
      }
    }
  };
  </script>
  
  <style scoped>
  .task-card {
    background-color: #fff;
    padding: 12px 8px;
    border-radius: 3px;
    margin-bottom: 8px;
    box-shadow: 0 1px 0 rgba(9, 30, 66, 0.25);
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .task-card:hover {
    background-color: #f4f5f7;
  }
  
  .task-name {
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 4px;
  }
  
  .task-name-input {
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 4px;
    width: 100%;
    border: none;
    border-radius: 3px;
    padding: 4px;
    box-shadow: 0 1px 0 rgba(9, 30, 66, 0.25);
  }
  
  .task-tags {
    margin-bottom: 8px;
  }
  
  .task-tag {
    display: inline-block;
    padding: 2px 6px;
    border-radius: 3px;
    color: #fff;
    font-size: 12px;
    margin-right: 4px;
    cursor: pointer;
  }
  
  .task-description {
    font-size: 14px;
    color: #5e6c84;
  }
  
  .task-textarea {
    width: 100%;
    border: none;
    border-radius: 3px;
    box-shadow: 0 1px 0 rgba(9, 30, 66, 0.25);
    padding: 8px;
    font-size: 14px;
    resize: none;
  }
  
  .task-textarea:focus {
    outline: none;
    box-shadow: 0 0 0 2px #0079bf;
  }
  </style>