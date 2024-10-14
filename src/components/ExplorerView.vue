<template>
    <div class="explorer-view">
      <div class="folder-tree">
        <FolderTree :folders="folders" @folder-selected="handleFolderSelected" />
      </div>
      <div class="sub-folder-view">
        <SubFolders v-if="selectedFolder" :selectedFolder="selectedFolder" />
      </div>
    </div>
  </template>
  
  <script>
  import FolderTree from '@/components/FolderTree.vue';
  import SubFolders from '@/components/SubFolders.vue';
  import axios from 'axios';
  
  export default {
    components: {
      FolderTree,
      SubFolders,
    },
    data() {
      return {
        folders: [],
        selectedFolder: null,
      };
    },
    created() {
      this.fetchFolders();
    },
    methods: {
      async fetchFolders() {
        try {
          const response = await axios.get('http://localhost:3000/api/folders');
          this.folders = response.data;
        } catch (error) {
          console.error('Error fetching folders:', error);
        }
      },
      handleFolderSelected(folder) {
        this.selectedFolder = folder;
      },
    },
  };
  </script>
  
  <style>
  .explorer-view {
    display: flex;
    height: 100vh; /* Mengisi tinggi viewport */
    background-color: #e9ecef; /* Warna latar belakang yang lebih lembut dan modern */
  }
  
  .folder-tree {
    width: 250px; /* Lebar tetap untuk panel kiri */
    border-right: 1px solid #ccc; /* Garis pemisah */
    padding: 20px;
    background-color: #d1e7fd; /* Warna biru muda untuk folder tree */
    overflow-y: auto; /* Scroll jika konten melebihi tinggi */
    position: relative; /* Agar dapat menempatkan elemen di dalamnya */
    transition: background-color 0.3s; /* Transisi warna latar belakang */
  }
  
  .sub-folder-view {
    flex-grow: 1; /* Mengambil sisa ruang */
    padding: 20px; /* Ruang dalam untuk sub-folder */
    background-color: #ffffff; /* Warna latar belakang putih untuk sub-folder */
    overflow-y: auto; /* Scroll jika konten melebihi tinggi */
  }
  
  h2 {
    font-size: 1.5em; /* Ukuran font judul */
    margin-bottom: 10px; /* Spasi di bawah judul */
  }
  
  .folder-item {
    padding: 10px;
    border-bottom: 1px solid #e0e0e0; /* Garis bawah untuk item folder */
    cursor: pointer; /* Menunjukkan bahwa item dapat diklik */
    transition: background-color 0.3s, transform 0.2s; /* Transisi untuk hover dan transform */
  }
  
  .folder-item:hover {
    background-color: #e8f0fe; /* Warna latar belakang saat hover */
    transform: scale(1.02); /* Sedikit membesar saat hover */
  }
  
  .folder-item.selected {
    background-color: #a3c1e0; /* Warna latar belakang biru saat item dipilih */
    transform: scale(1.05); /* Sedikit membesar saat dipilih */
  }
  
  /* Responsive Styles */
  @media (max-width: 768px) {
    .folder-tree {
      width: 100%; /* Panel kiri penuh pada perangkat kecil */
      border-right: none; /* Menghilangkan garis pemisah */
    }
  
    .sub-folder-view {
      padding: 10px; /* Padding lebih kecil pada perangkat kecil */
    }
  }
  </style>
  