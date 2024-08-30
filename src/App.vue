<script>
import Card from "./components/Card.vue";

export default {
  data() {
    return {
      cards: [],
      paciente: "",
      fecha: "",
      hora: "",
      gravedad: "",
      motivo: "",
    };
  },
  components: {
    Card,
  },
  // computed se usa para crear propiedades que dependen de otras propiedades
  computed: {
    // Verificación si todos los campos están completos
    formularioCompleto() {
      return (
        this.paciente && this.fecha && this.hora && this.gravedad && this.motivo
      );
    },
  },
  methods: {
    agregarCard(event) {
      event.preventDefault();

      // Agregar la card si todos los campos están completos
      if (this.formularioCompleto) {
        this.cards.push({
          paciente: this.paciente,
          fecha: this.fecha,
          hora: this.hora,
          gravedad: this.gravedad,
          motivo: this.motivo,
        });

        // Limpiar formulario
        this.paciente = "";
        this.fecha = "";
        this.hora = "";
        this.gravedad = "";
        this.motivo = "";
      }
    },
    eliminarCard(paciente) {
      this.cards = this.cards.filter((card) => card.paciente !== paciente);
    },
  },
};
</script>

<template>
  <h1>Administrador de citas médicas</h1>
  <form @submit.prevent="agregarCard">
    <div class="form-consultaMedica">
      <div>
        <label :style="{ color: paciente ? 'black' : 'red' }" for="paciente"
          >Paciente</label
        >
        <input v-model="paciente" type="text" id="paciente" />
      </div>
      <div>
        <label :style="{ color: fecha ? 'black' : 'red' }" for="fecha"
          >Fecha</label
        >
        <input v-model="fecha" type="date" id="fecha" />
      </div>
      <div>
        <label :style="{ color: hora ? 'black' : 'red' }" for="hora"
          >Hora</label
        >
        <input v-model="hora" type="time" id="hora" />
      </div>
      <div>
        <label :style="{ color: gravedad ? 'black' : 'red' }" for="gravedad"
          >Gravedad</label
        >
        <select v-model="gravedad" id="gravedad">
          <option value="">Seleccionar</option>
          <option value="alta">Alta</option>
          <option value="media">Media</option>
          <option value="baja">Baja</option>
        </select>
      </div>
      <div>
        <label :style="{ color: motivo ? 'black' : 'red' }" for="motivo"
          >Motivo</label
        >
        <input v-model="motivo" type="text" id="motivo" />
      </div>
    </div>
    <div class="boton-agregar">
      <button type="submit" :disabled="!formularioCompleto">Agregar</button>
    </div>
  </form>

  <section class="cards-container">
    <Card
      v-for="(card, i) in cards"
      :key="i"
      :paciente="card.paciente"
      :fecha="card.fecha"
      :hora="card.hora"
      :gravedad="card.gravedad"
      :motivo="card.motivo"
      @eliminar="eliminarCard(card.paciente)"
    />

    <p v-if="cards.length === 0" class="mensaje">
      Aún no hay consultas registradas
    </p>
  </section>
</template>

<style scoped>
* {
  font-family: "Roboto", sans-serif;
}

form {
  width: 55%;
  margin: 30px auto 0;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f9f9f9;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  font-weight: bold;
}

.form-consultaMedica {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  width: 100%;
}

.form-consultaMedica > div {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-width: 120px;
}

input,
select {
  width: 100%;
  padding: 5px;
  font-size: 14px;
}

.boton-agregar {
  margin-top: 15px;
  width: 100%;
  display: flex;
  justify-content: center;
}

button {
  background-color: #ccc;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 14px;
  cursor: pointer;
}

button:disabled {
  background-color: #eee;
  cursor: not-allowed;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: flex-start;
  margin-top: 20px;
}

h1,
.mensaje {
  text-align: center;
}

.mensaje {
  font-weight: bold;
  margin-top: 20px;
  color: red;
  width: 100%;
}
</style>
