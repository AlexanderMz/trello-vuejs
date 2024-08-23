<template> 
    <div class="task-card" @dragstart="onDragStart" draggable="true">
        <h4>{{ task.title }}</h4>
        <p>{{ task.description }}</p>
    </div>
</template>

<script>
    export default {
        name: 'TaskWhite',
        props: {
            task: Object
        },
        methods: {
            onDragStart() {
                this.$emit('dragstart', this.task);
            },
            onDrop(){
                this.$emit('drop', this.task)
            }
        }
    };
</script>

<style scoped>
    .task-card{
        background-color: #fff;
        padding: 8px;
        margin-bottom: 8px;
        border-radius: 3px;
        box-shadow: 0 1px 0 rgba(9,30,66,0.25);
        cursor: pointer;
        font-size: 14px;
        min-height: 30px;
    }

    .task-card:hover{
        background-color: #f4f5f7;

    }

    .task-card:active {
        background-color: #e2e4e6;
    }
</style>