<script setup>
import { reactive, computed } from 'vue';
import productocard from './components/productocard.vue';

// Lista de productos
const productos = reactive([
  { id: 1, nombre: 'Laptop', precio: 12000, cantidad: 0, img: '/laptop.jpg' },
  { id: 2, nombre: 'Mouse', precio: 800, cantidad: 0, img: '/mouse.jpg' },
  { id: 3, nombre: 'Controles', precio: 200, cantidad: 0, img: '/controles.jpg' },
  { id: 4, nombre: 'Cargadores', precio: 100, cantidad: 0, img: '/cargador.jpg' },
  { id: 5, nombre: 'Audifonos', precio: 70, cantidad: 0, img: '/audifonos.jpg' },
  { id: 6, nombre: 'Lentes', precio: 200, cantidad: 0, img: '/lentes.jpg' }
]);

const agregar = (p) => p.cantidad++;
const quitar = (p) => { if (p.cantidad > 0) p.cantidad--; };

const total = computed(() => productos.reduce((sum, p) => sum + (p.precio * p.cantidad), 0));
const totalArticulos = computed(() => productos.reduce((sum, p) => sum + p.cantidad, 0));
</script>

<template>
  <div class="container">
    <h1>Mi Tienda</h1>
    <div class="resumen">
      <p>Artículos en carrito: {{ totalArticulos }}</p>
      <h3>Total: ${{ total }}</h3>
    </div>

    <div class="productos">
      <productocard 
        v-for="p in productos" :key="p.id"
        :nombre="p.nombre" 
        :precio="p.precio" 
        :imagen="p.img" 
        :cantidad="p.cantidad"
        @agregar="agregar(p)" 
        @quitar="quitar(p)"
      />
    </div>
  </div>
</template>

<style>
.container { text-align: center; padding: 20px; font-family: sans-serif; }

.productos {
  display: flex;
  flex-wrap: wrap; /* Permite que los elementos salten de línea */
  justify-content: center; /* Centra las tarjetas */
  gap: 20px; /* Espacio entre ellas */
  margin-top: 30px;
}
</style>