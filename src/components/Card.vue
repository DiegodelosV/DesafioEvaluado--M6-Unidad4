<template>
  <div class="card" :class="gravedad">
    <h3>Paciente</h3>
    <span>{{ paciente }}</span>
    <h3>Fecha</h3>
    <span>{{ fecha }}</span>
    <h3>Hora</h3>
    <span>{{ hora }}</span>
    <h3>Gravedad</h3>
    <span>{{ gravedad }}</span>
    <h3>Motivo</h3>
    <span>{{ motivo }}</span>
    <button @click="$emit('eliminar', paciente)">Eliminar</button>
  </div>
</template>

<script>
export default {
  props: ["paciente", "fecha", "hora", "gravedad", "motivo"],
};
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 200px;
  height: 70%;
  max-height: 600px;
}
.card button {
  margin-top: 10px;
}

/* Estilos para el tipo de gravedad */
.alta {
  background-color: red;
  color: white;
}

.media {
  background-color: yellow;
  color: black;
}

.baja {
  background-color: green;
  color: black;
}
</style>
