<template>
    <div class="add-employee">
      <h2>Tambah Pegawai</h2>
      <form @submit.prevent="validateAndAddEmployee">
        <input type="text" v-model="nip" placeholder="NIP" required />
        <input type="text" v-model="name" placeholder="Nama" required />
        <input type="number" v-model="experience" placeholder="Lama Bekerja" required />
        <input type="number" v-model="salary" placeholder="Gaji" required />
        <select v-model="position" required>
          <option disabled value="">Pilih Divisi dan Posisi</option>
          <option value="Developer (Staff)">Developer (Staff)</option>
          <option value="Developer (Manager)">Developer (Manager)</option>
          <option value="Dokumentasi (Staff)">Dokumentasi (Staff)</option>
          <option value="Dokumentasi (Manager)">Dokumentasi (Manager)</option>
          <option value="Editor (Staff)">Editor (Staff)</option>
          <option value="Editor (Manager)">Editor (Manager)</option>
          <option value="Intern">Intern</option>
        </select>
        <button class="add-btn" type="submit">Tambah</button>
        <p v-if="error" class="error">{{ error }}</p>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        nip: '',
        name: '',
        experience: 0,
        salary: 0,
        position: '',
        error: ''
      }
    },
    methods: {
      validateAndAddEmployee() {
        if (!/^\d{1,10}$/.test(this.nip)) {
          this.error = 'NIP harus berupa angka dan maksimal 10 digit';
          return;
        }
        if (!/^[a-zA-Z\s.]+$/.test(this.name)) {
          this.error = 'Nama hanya boleh mengandung huruf dan titik';
          return;
        }
        this.error = '';
        this.$emit('add-employee', {
          id: Date.now(),
          nip: this.nip,
          name: this.name,
          experience: this.experience,
          salary: this.salary,
          position: this.position
        });
        this.clearForm();
      },
      clearForm() {
        this.nip = '';
        this.name = '';
        this.experience = 0;
        this.salary = 0;
        this.position = '';
      }
    }
  }
  </script>
  
  <style scoped>
  .add-employee {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    background-color: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
  }
  
  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
  }
  
  input, select {
    margin: 10px 0;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 6px;
    width: 100%;
    max-width: 300px;
  }
  
  button {
    margin-top: 20px;
    padding: 10px;
    background-color: #2196f3;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #1976d2;
  }
  
  .error {
    color: red;
    font-weight: bolder;
    margin-top: 10px;
  }
  </style>
  