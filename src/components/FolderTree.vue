<template>
    <ul class="folder-list">
      <li
        v-for="folder in folders"
        :key="folder.id"
        class="folder-item"
        :class="{ selected: isSelected(folder) }" 
        @click="selectFolder(folder)"
      >
      <i class="fas fa-folder"></i>
        {{ folder.name }}
      </li>
    </ul>
  </template>
  
  <script>
  export default {
    props: {
      folders: Array,
    },
    data() {
      return {
        selectedFolderId: null,
      };
    },
    methods: {
      selectFolder(folder) {
        this.selectedFolderId = folder.id;
        this.$emit('folder-selected', folder);
      },
      isSelected(folder) {
        return this.selectedFolderId === folder.id;
      },
    },
  };
  </script>
  
  <style scoped>
  /* Hilangkan bullet points */
  .folder-list {
    list-style-type: none; /* Menghilangkan bullet points */
    padding-left: 0; /* Hilangkan padding bawaan pada <ul> */
  }
  
  .folder-item {
    padding: 10px;
    border-bottom: 1px solid #e0e0e0;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
  }
  
  /* Warna saat di-hover */
  .folder-item:hover {
    background-color: #e8f0fe;
    transform: scale(1.02);
  }
  
  /* Warna setelah folder dipilih */
  .folder-item.selected {
    background-color: #a3c1e0;
    transform: scale(1.05);
    color: white;
    font-weight: bold;
  }
  </style>
  