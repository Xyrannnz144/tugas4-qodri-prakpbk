<template>
    <div class="edit-employee">
      <h2>Edit Pegawai</h2>
      <form @submit.prevent="validateAndSaveEmployee">
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
        <div class="button-container">
          <button class="save-btn" type="submit">Simpan</button> 
          <br />
          <button class="cancel-btn" type="button" @click="$emit('cancel-edit')">Batal</button>
        </div>
        <p v-if="error" class="error">{{ error }}</p>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      employee: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        nip: this.employee.nip,
        name: this.employee.name,
        experience: this.employee.experience,
        salary: this.employee.salary,
        position: this.employee.position,
        error: ''
      }
    },
    methods: {
      validateAndSaveEmployee() {
        if (!/^\d{1,10}$/.test(this.nip)) {
          this.error = 'NIP harus berupa angka dan maksimal 10 digit';
          return;
        }
        if (!/^[a-zA-Z\s.]+$/.test(this.name)) {
          this.error = 'Nama hanya boleh mengandung huruf dan titik';
          return;
        }
        this.error = '';
        this.$emit('save-employee', {
          id: this.employee.id,
          nip: this.nip,
          name: this.name,
          experience: this.experience,
          salary: this.salary,
          position: this.position
        });
      }
    }
  }
  </script>
  
  <style scoped>
  .edit-employee {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    background-color: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin-top: 20px;
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
  
  .button-container {
    display: flex;
    justify-content: space-between;
    width: 100%;
    max-width: 300px;
  }
  
  button {
    padding: 10px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    flex-grow: 1;
    margin: 5px;
  }
  
  .save-btn {
    background-color: #ffeb3b;
    color: black;
    
  }
  
  .save-btn:hover {
    background-color: #fbc02d;
  }
  
  .cancel-btn {
    background-color: #db8a11;
    color: white;
  }
  
  .cancel-btn:hover {
    background-color: #5a2c07;
  }
  
  .error {
    color: red;
    font-weight: bolder;
    margin-top: 10px;
  }
  </style>
  