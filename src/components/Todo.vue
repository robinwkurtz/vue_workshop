<template>
  <div>
    <h1>Todo</h1>
    <div class="task" v-for="(task, i) in tasks" :key="i">
      <button
        class="task_checkbox"
        :class="{task_checkbox_completed: task.completed}"
        @click="markAsDone(i)"
      />
      <p
        class="task_text"
        :class="{task_text_completed: task.completed}"
      >
      {{ task.text }}
      </p>
      <button
        class="task_delete"
        @click="deleteTask(i)"
      >
        x
      </button>
    </div>
    <div class="add">
      <input
        type="text"
        placeholder="Add thing"
        @keyup.enter="addTask"
        v-model="task"
        class="add_input"
      />
      </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data: () => ({
    task: '',
    tasks: [
      {
        text: 'Buy beer',
        completed: false
      },
      {
        text: 'Buy wine',
        completed: false
      },
      {
        text: 'Buy cheese',
        completed: true
      }
    ]
  }),
  methods: {
    markAsDone(i) {
      this.tasks[i].completed = !this.tasks[i].completed;
    },
    deleteTask(i) {
      this.tasks.splice(i, 1);
    },
    addTask() {
      if (this.task) {
        this.tasks.push({
          text: this.task,
          completed: false
        })

        this.task = '';
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task {
  align-items: center;
  grid-template-columns: auto 1fr auto;
  justify-content: space-between;
}
.task,
.add {
  border-bottom: 1px solid #474143;
  display: grid;
}
.add {
  grid-template-columns: 1fr;
}
.add_input {
  border: 0;
  color: #474143;
  font-size: 1rem;
  padding: 0.9rem;
  outline: none;
}
.task_checkbox {
  outline: none;
  background-color: #474143;
  border: 0;
  border-radius: 50%;
  cursor: pointer;
  height: 24px;
  width: 24px;
}
.task_checkbox_completed,
.task_text_completed {
  opacity: 0.45;
}
.task_checkbox:hover {
  opacity: 0.75;
}
.task_text {
  margin-left: 1.25rem;
  justify-self: start;
}
.task_text_completed {
  text-decoration: line-through;
}
.task_delete {
  outline: none;
  background: none;
  border: 0;
  border-radius: 50%;
  cursor: pointer;
  height: 24px;
  width: 24px;
}
.task_delete:hover {
  background-color: #ff6444;
  color: #fff;
}
</style>
