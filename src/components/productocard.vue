<script setup>
const props = defineProps({
  nombre: String,
  precio: Number,
  imagen: String,
  cantidad: Number
})

const emit = defineEmits(['agregar', 'quitar'])
</script>

<template>
  <div class="card">
    <img :src="imagen" :alt="nombre" class="img-producto" />
    <h3>{{ nombre }}</h3>
    <p>${{ precio }}</p>
    <p>Cantidad: {{ cantidad }}</p>
    
    <div class="botones">
      <button @click="emit('agregar')">+</button>
      <button @click="emit('quitar')" :disabled="cantidad === 0" class="btn-quitar">-</button>
    </div>
  </div>
</template>

<style scoped>
.card {
  background: rgb(74, 31, 230);
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  text-align: center;
  width: 180px; /* Tamaño fijo */
  display: flex;
  flex-direction: column;
  align-items: center;
}

.img-producto {
  width: 100px;
  height: 100px;
  object-fit: contain; /* Ajusta la imagen sin deformarla */
  background: white;
  border-radius: 8px;
  margin-bottom: 10px;
}

.botones { display: flex; gap: 10px; justify-content: center; }

button {
  padding: 5px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background: rgb(6, 111, 143);
 
}

.btn-quitar:disabled { opacity: 0.5; cursor: not-allowed; }
</style>