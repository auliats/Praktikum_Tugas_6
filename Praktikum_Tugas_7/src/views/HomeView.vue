<script setup>
import { ref } from 'vue'
import ProductCard from '../components/ProductCard.vue'
import { useCartStore } from '../stores/cart'

const cartStore = useCartStore()

const produkList = ref([
  { id: 1, nama: "Laptop ASUS ROG", harga: 15000000, stok: 5 },
  { id: 2, nama: "Mechanical Keyboard", harga: 750000, stok: 12 },
  { id: 3, nama: "Mouse Gaming RGB", harga: 350000, stok: 0 }
])

const tambahKeCart = (produk) => {
  cartStore.tambahItem(produk)
  alert(`Berhasil menambahkan ${produk.nama} ke keranjang!`)
}
</script>

<template>
  <div class="container">
    <h2>🛍️ Tugas 07: Beranda Katalog Produk</h2>
    <div class="grid-produk">
      <ProductCard 
        v-for="p in produkList" 
        :key="p.id"
        :id="p.id"
        :nama="p.nama"
        :harga="p.harga"
        :stok="p.stok"
        @beli-produk="tambahKeCart"
      />
    </div>
  </div>
</template>

<style scoped>
.container { max-width: 800px; margin: 2rem auto; padding: 0 1rem; font-family: sans-serif; }
.grid-produk { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1rem; margin-top: 1rem; }
</style>