<template>
    <!-- Contenedor principal de la tarea -->
    <div class="card mb-3 p-3">
        <!-- Título y estado -->
        <div class="d-flex justify-content-between align-items-center">
            <!-- Título con estilo tachado si está completada -->
            <h5 :class="{ 'text-decoration-line-through': completed }">
                {{ title }}
            </h5>
            <!-- Estado de la tarea -->
            <span :class="completed ? 'badge bg-success' : 'badge bg-warning'">
                {{ completed ? 'Completada' : 'Pendiente' }}
            </span>
        </div>

        <!-- Botones de acción -->
        <div class="mt-3">
            <button @click="$emit('toggle-completion')" 
                    class="btn btn-sm btn-primary me-2">
                {{ completed ? 'Marcar como Pendiente' : 'Marcar como Completada' }}
            </button>
            <button @click="$emit('delTodo')" 
                    class="btn btn-sm btn-danger">
                Eliminar
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: {
        title: String,      // Título de la tarea
        completed: Boolean  // Estado de la tarea
    }
}
</script>

<style scoped>
/* Añade tus estilos personalizados aquí */
</style>
