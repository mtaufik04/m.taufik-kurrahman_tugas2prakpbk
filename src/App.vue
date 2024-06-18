<template>
      <!-- BEBERAPA ELEMEN HTML DALAM HALAMAN" -->

  <div id="app">
    <div class="logo">TOKO SEJAHTERA</div>

    <h1>FORM INPUTAN BARANG</h1>

    <form @submit.prevent="addBarang">
      <!--ELEMEN INPUT TEKS-->
      <div class="input-container">
        <!-- Menambahkan class binding untuk menampilkan warna border merah jika input kosong -->
        <!-- Menambahkan style binding untuk mengubah warna latar belakang input menjadi abu-abu saat input sudah diisi -->
        <input v-model="newBarang.name" placeholder=" " class="barang-input white-placeholder" :class="{ 'input-error': newBarang.name === '' }" :style="{ 'background-color': newBarang.name !== '' ? 'transparent' : 'transparent' }">
        <label class="placeholder-label" :class="{ 'placeholder-active': newBarang.name !== '' }">Masukan Nama barang</label>
      </div>
      <div class="input-container">
        <input v-model="newBarang.harga" placeholder=" " class="barang-input white-placeholder" :class="{ 'input-error': newBarang.harga === '' }" :style="{ 'background-color': newBarang.harga !== '' ? 'transparent' : 'transparent' }">
        <label class="placeholder-label" :class="{ 'placeholder-active': newBarang.harga !== '' }">Masukan Harga barang</label>
      </div>
      <button type="submit">Add barang</button>
    </form>

    <table>
      <thead>
        <tr>
          <th>Nama Barang</th>
          <th>Harga</th>
          <th>Aksi</th>
        </tr>
      </thead>
      <tbody>
        <!-- 3. Interaksi dinamis dengan menggunakan event listeners untuk merubah nilai data Vue -->
        <tr v-for="(barang, index) in barangs" :key="index">
          <td>{{ barang.name }}</td>
          <td>{{ barang.harga }}</td>
          <td><button @click="deleteBarang(index)" class="hapus-btn">Hapus</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const barangs = ref([
  { name: 'Shampo', harga: 'Rp 20.000' },
  { name: 'Beras', harga: 'Rp 15.000' }
]);

const newBarang = ref({ name: '', harga: '' });

function addBarang() {
  if (newBarang.value.name.trim() !== '' && newBarang.value.harga.trim() !== '') {
    barangs.value.push({ name: newBarang.value.name, harga: newBarang.value.harga });
    newBarang.value = { name: '', harga: '' };
    window.alert('Barang berhasil ditambahkan!');
  }
}

function deleteBarang(index) {
  barangs.value.splice(index, 1);
  window.alert('Barang berhasil dihapus!');
}
</script>

