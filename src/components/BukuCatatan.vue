<script setup>
import { ref, computed } from "vue"

const judulBaru = ref("")
const kategoriBaru = ref("Teknologi")

const daftarBuku = ref([
  { id: 1, judul: "Pemrograman Web Vue.js 3", kategori: "Teknologi", selesai: true },
  { id: 2, judul: "Belajar Algoritma Dasar", kategori: "Pendidikan", selesai: false }
])

const tambahBuku = () => {
  if (!judulBaru.value.trim()) return
  daftarBuku.value.push({
    id: Date.now(),
    judul: judulBaru.value.trim(),
    kategori: kategoriBaru.value,
    selesai: false
  })
  judulBaru.value = ""
}

const hapusBuku = (id) => {
  daftarBuku.value = daftarBuku.value.filter(buku => buku.id !== id)
}

const totalSelesai = computed(() => {
  return daftarBuku.value.filter(buku => buku.selesai).length
})
</script>

<template>
  <div class="buku-container">
    <h2>📚 Tugas 06: Aplikasi Buku Catatan</h2>

    <form @submit.prevent="tambahBuku" class="form-group">
      <input v-model="judulBaru" placeholder="Judul buku baru..." required />
      <select v-model="kategoriBaru">
        <option value="Teknologi">Teknologi</option>
        <option value="Pendidikan">Pendidikan</option>
        <option value="Novel">Novel</option>
      </select>
      <button type="submit">Tambah Buku</button>
    </form>

    <p>Total Buku: <strong>{{ daftarBuku.length }}</strong> | Selesai Dibaca: <strong style="color: #10b981;">{{ totalSelesai }}</strong></p>

    <ul>
      <li v-for="buku in daftarBuku" :key="buku.id" class="item-buku">
        <div>
          <input type="checkbox" v-model="buku.selesai" />
          <span :style="{ textDecoration: buku.selesai ? 'line-through' : 'none' }">
            {{ buku.judul }} ({{ buku.kategori }})
          </span>
        </div>
        <button @click="hapusBuku(buku.id)" class="btn-hapus">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.buku-container { max-width: 500px; margin: 2rem auto; padding: 2rem; background: #fff; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); font-family: sans-serif; }
.form-group { display: flex; gap: 0.5rem; margin-bottom: 1rem; }
.form-group input, .form-group select { padding: 0.5rem; flex: 1; border: 1px solid #cbd5e1; border-radius: 4px; }
button { padding: 0.5rem 1rem; background: #2563eb; color: white; border: none; border-radius: 4px; cursor: pointer; }
.item-buku { display: flex; justify-content: space-between; align-items: center; padding: 0.5rem 0; border-bottom: 1px solid #e2e8f0; }
.btn-hapus { background: #ef4444; }
</style>