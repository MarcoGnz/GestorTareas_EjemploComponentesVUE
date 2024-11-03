<template>
    <div class="container mt-4">
        <h1 class="mb-3">Lista de Tareas</h1>
        <button @click="fetchTasks" class="btn btn-primary mb-3">Cargar Tareas</button>

        <div v-if="tasks.length > 0">
            <div 
                v-for="task in tasks" 
                :key="task.id" 
                class="card mb-2 p-3" 
            >
                <div class="d-flex justify-content-between align-items-center">
                    <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">
                        {{ task.todo }}
                    </h5>
                    <span class="badge" :class="task.completed ? 'bg-success' : 'bg-warning'">
                        {{ task.completed ? 'Completada' : 'Pendiente' }}
                    </span>
                </div>
                
                <div class="d-flex mt-2">
                    <button 
                        @click="toggleTaskCompletion(task)" 
                        class="btn btn-sm" 
                        :class="task.completed ? 'btn-secondary' : 'btn-success'"
                    >
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button 
                        @click="deleteTask(task)" 
                        class="btn btn-sm btn-danger ms-2"
                    >
                        Eliminar
                    </button>
                </div>
            </div>
        </div>
        <div v-else>
            <p>No hay tareas disponibles. Haz clic en "Cargar Tareas" para verlas.</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "TaskList",
    data() {
        return {
            tasks: [] // Almacenamiento de tareas
        };
    },
    methods: {
        // Obtiene las tareas de la API
        async fetchTasks() {
            try {
                const response = await fetch('https://dummyjson.com/todos');
                const data = await response.json();
                this.tasks = data.todos;
            } catch (error) {
                console.error('Error al cargar las tareas:', error);
            }
        },

        // Cambia el estado de completado de la tarea
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Elimina la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        }
    }
};
</script>

<style scoped>
/* Estilos de personalización */
</style>
