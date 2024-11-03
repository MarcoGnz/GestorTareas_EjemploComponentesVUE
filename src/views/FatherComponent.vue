<template>
  <div class="container mt-4">
    <!-- Contenedor del Componente Padre -->
    <div class="p-4 rounded bg-info text-white mb-4">
      <h1 class="display-6">Componente Padre</h1>
      <ChildComponent :message="parentMessage" @response="handleResponse" />
      <p class="mt-2">{{ childResponse }}</p>
    </div>

    <!-- Tareas Locales -->
    <div class="bg-secondary p-3 rounded mb-4">
      <h2 class="h5 ">Tareas Locales</h2>
      <TodoItem
        v-for="(task, index) in tasks"
        :key="index"
        :title="task.title"
        :completed="task.completed"
        @toggle-completion="toggleCompletion(index, 1)"
        @delTodo="deleteTask(index, 1)"
      />
    </div>

    <!-- Tareas Cargadas Externamente -->
    <div class="bg-warning p-3 rounded">
      <h2 class="h5">Lista de Tareas</h2>
      <button @click="fetchTasks" class="btn btn-primary btn-sm mb-3">Cargar Tareas</button>
      <div v-if="tareas.length > 0">
        <TodoItem
          v-for="(task, index2) in tareas"
          :key="task.id"
          :title="task.todo"
          :completed="task.completed"
          @toggle-completion="toggleCompletion(index2, 0)"
          @delTodo="deleteTask(index2, 0)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ChildComponent from '../components/ChildComponent.vue'
import TodoItem from '../components/TodoItem.vue'

export default {
  components: {
    ChildComponent,
    TodoItem
  },
  data() {
    return {
      parentMessage: 'Aqui estoy',
      childResponse: '',
      tasks: [
        { title: 'Tarea 1', completed: false },
        { title: 'Tarea 2', completed: true },
        { title: 'Hola', completed: false }
      ],
      tareas: []
    };
  },
  methods: {
    handleResponse(responseMessage) {
      this.childResponse = responseMessage;
    },
    toggleCompletion(index, i) {
      if (i === 1) {
        this.tasks[index].completed = !this.tasks[index].completed;
      } else {
        this.tareas[index].completed = !this.tareas[index].completed;
      }
    },
    deleteTask(index, i) {
      if (i === 1) {
        this.tasks.splice(index, 1);
      } else {
        this.tareas.splice(index, 1);
      }
    },
    async fetchTasks() {
      try {
        const response = await fetch('https://dummyjson.com/todos');
        const data = await response.json();
        this.tareas = data.todos;
      } catch (error) {
        console.error('Error al cargar las tareas:', error);
      }
    }
  }
};
</script>
