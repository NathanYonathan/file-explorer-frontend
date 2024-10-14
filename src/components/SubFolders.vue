<template>
    <div class="sub-folder">
      <!-- Breadcrumb navigation -->
      <nav class="breadcrumb">
        <span>{{ selectedFolder.name }}</span>
      </nav>
  
      <div class="folder-file-view">
        <!-- Sub Folders Section -->
        <div class="sub-folders">
          <h3>Sub Folders</h3>
          <ul>
            <li v-for="subFolder in subFolders" :key="subFolder.id" class="folder-item">
              <i class="fas fa-folder"></i> <!-- Font Awesome Folder Icon -->
              {{ subFolder.name }}
            </li>
          </ul>
        </div>
  
        <!-- Files Section -->
        <div class="files">
          <h3>Files</h3>
          <ul>
            <li v-for="file in files" :key="file.id" class="file-item">
              <i class="fas fa-file-alt"></i> <!-- Font Awesome File Icon -->
              {{ file.name }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      selectedFolder: Object,
    },
    data() {
      return {
        subFolders: [],
        files: [],
      };
    },
    watch: {
      selectedFolder: {
        immediate: true,
        handler(newVal) {
          if (newVal) {
            this.fetchSubFoldersAndFiles(newVal.id);
          }
        },
      },
    },
    methods: {
      async fetchSubFoldersAndFiles(folderId) {
        try {
          // Fetch subfolders
          const subFoldersResponse = await axios.get(`http://localhost:3000/api/folders/${folderId}/subfolders`);
          this.subFolders = subFoldersResponse.data;
  
          // Fetch files for the selected folder
          const filesResponse = await axios.get(`http://localhost:3000/api/folders/${folderId}/files`);
          this.files = filesResponse.data;
        } catch (error) {
          console.error('Error fetching subfolders and files:', error);
        }
      },
    },
  };
  </script>

  <style scoped>
  .sub-folder {
    margin-top: 20px;
  }
  
  /* Breadcrumb Styles */
  .breadcrumb {
    padding: 10px 0;
    background-color: #f8f9fa;
    border-bottom: 1px solid #ddd;
    margin-bottom: 20px;
    font-size: 1.1em;
    color: #007bff;
  }
  
  .breadcrumb span {
    color: #007bff;
  }
  
  /* Folder and File Layout */
  .folder-file-view {
    display: flex;
    gap: 20px;
  }
  
  .sub-folders, .files {
    flex: 1;
    background-color: #ffffff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  h3 {
    font-size: 1.2em;
    margin-bottom: 15px;
  }
  
  ul {
    list-style: none;
    padding-left: 0;
  }
  
  .folder-item, .file-item {
    display: flex;
    align-items: center; /* Align icons and text */
    padding: 12px;
    margin-bottom: 8px;
    border-bottom: 1px solid #e0e0e0;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
  }
  
  .folder-item:hover, .file-item:hover {
    background-color: #f1f8ff;
    transform: translateX(5px);
  }
  
  .folder-item:active, .file-item:active {
    background-color: #e0f7fa;
  }
  
  .folder-item i, .file-item i {
    margin-right: 10px; /* Space between icon and text */
    font-size: 1.2em; /* Adjust icon size */
  }
  
  /* Responsive Styles */
  @media (max-width: 768px) {
    .folder-file-view {
      flex-direction: column; /* Layout stack vertically on small screens */
    }
  }
  </style>
  