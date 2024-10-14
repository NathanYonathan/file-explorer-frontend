<template>
  <div id="app">
    <header>
      <h1 class="app-title">Windows Explorer-like Application</h1>
    </header>
    <main>
      <ExplorerView />
    </main>
  </div>
</template>

<script>
import ExplorerView from './components/ExplorerView.vue'; // Import ExplorerView component

export default {
  name: 'App',
  components: {
    ExplorerView,
  }
}
</script>

<style>
/* Tambahkan gaya CSS di sini */
* {
  box-sizing: border-box; /* Pastikan padding dan border dihitung dalam total width dan height */
}

body {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: #f5f5f5; /* Background yang lebih lembut */
}

#app {
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* Pastikan konten mengisi tinggi penuh layar */
}

header {
  background-color: #007bff; /* Warna latar belakang header */
  color: white;
  padding: 1.5rem 1rem; /* Padding yang lebih baik untuk header */
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Menambahkan bayangan untuk kedalaman */
}

.app-title {
  margin: 0;
  font-size: 2rem; /* Ukuran font lebih besar */
}

main {
  padding: 2rem; /* Tambahan padding untuk konten utama */
  flex-grow: 1; /* Memungkinkan main untuk tumbuh dan mengisi ruang yang tersisa */
}

@media (max-width: 600px) {
  .app-title {
    font-size: 1.5rem; /* Ukuran font lebih kecil pada perangkat kecil */
  }
  
  main {
    padding: 1rem; /* Padding lebih kecil pada perangkat kecil */
  }
}
</style>
