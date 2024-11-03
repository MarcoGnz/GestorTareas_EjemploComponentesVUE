<template>
  <div style="background-color: cadetblue;" class="text-center p-3 border rounded">
    <h1>Componente Hijo</h1>
    <p class="mb-3 text-muted">
      {{ message }}
    </p>
    <button @click="sendResponse" class="btn btn-primary">
      Responder al Padre
    </button>
  </div>
</template>

<script>
export default {
  props: {
    message: String // Recibimos el mensaje del componente padre
  },
  methods: {
    sendResponse() {
      this.$emit('response', 'Respuesta enviada desde el componente Hijo') // Emitimos el evento 'response' con un mensaje
    }
  }
}
</script>
