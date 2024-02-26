<template>
  <q-page class="q-pa-md">
    <q-list bordered class="q-pa-md rounded-borders" separator>
      <q-item
        v-ripple
        v-for="task in tasks"
        :key="task.id"
        @click="toggleCompletion(task)"
        clickable
        :class="{'text-grey-6': task.completed, 'text-primary': !task.completed}"
      >
        <q-item-section side top>
          <q-checkbox v-model="task.completed" color="primary"/>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-h6" :class="{'text-strike': task.completed}">{{ task.name }}</q-item-label>
        </q-item-section>

        <q-item-section side top>
          <q-item-label caption class="text-weight-medium">{{ calculateDaysLeft(task.dueDate) }}</q-item-label>
          <q-item-label caption class="text-weight-medium">{{ formatDate(task.dueDate, task.dueTime) }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'todoPage',
  data() {
    return {
      tasks: [
        {
          id: 1,
          name: 'Go to Shop',
          completed: true,
          dueDate: '2024/05/12',
          dueTime: '20:00'
        },
        {
          id: 2,
          name: 'Get Apples',
          completed: false,
          dueDate: '2024/05/12',
          dueTime: '20:00'
        },
        {
          id: 3,
          name: 'Get Chips',
          completed: false,
          dueDate: '2024/05/12',
          dueTime: '20:00'
        },
        {
          id: 4,
          name: 'Go to home',
          completed: false,
          dueDate: '2024/05/12',
          dueTime: '20:00'
        }
        // Other tasks...
      ]
    }
  },
  methods: {
    toggleCompletion(task) {
      task.completed = !task.completed;
    },
    calculateDaysLeft(dueDate) {
      const today = new Date();
      const due = new Date(dueDate);
      const difference = due - today;
      const daysLeft = Math.ceil(difference / (1000 * 60 * 60 * 24));
      return daysLeft > 0 ? `${daysLeft} days left` : 'Due today';
    },
    formatDate(date, time) {
      // Assuming you want to keep it simple for this example
      return `${date} at ${time}`;
    }
  }
})
</script>

<style>
.rounded-borders {
  border-radius: 8px;
}
</style>
