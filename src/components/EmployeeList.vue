<template>
    <div class="employee-list">
      <h2>List Data Pegawai</h2>
      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>No</th>
              <th>NIP</th>
              <th>Nama</th>
              <th>Lama Bekerja (tahun)</th>
              <th>Gaji</th>
              <th>Posisi</th>
              <th>Aksi</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(employee, index) in employees" :key="employee.id">
              <td>{{ index + 1 }}</td>
              <td>{{ employee.nip }}</td>
              <td>{{ employee.name }}</td>
              <td>{{ employee.experience }}</td>
              <td>{{ employee.salary }}</td>
              <td>{{ employee.position }}</td>
              <td>
                <button class="edit-btn" @click="editEmployee(employee)">Edit</button>
                <button class="delete-btn" @click="deleteEmployee(employee.id)">Hapus</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      employees: {
        type: Array,
        required: true
      }
    },
    methods: {
      editEmployee(employee) {
        this.$emit('edit-employee', employee);
      },
      deleteEmployee(employeeId) {
        if (confirm('Anda yakin ingin menghapus data pegawai ini?')) {
          this.$emit('delete-employee', employeeId);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .employee-list {
    margin: 20px 0;
    overflow: hidden;
  }
  
  .table-container {
    max-height: 400px;
    overflow-y: auto;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 1em;
    min-width: 600px;
  }
  
  th, td {
    padding: 10px;
    text-align: left;
  }
  
  th {
    background-color: #f0f0f0;
    color: #333;
    font-weight: bold;
  }
  
  td {
    border-bottom: 1px solid #ddd;
    word-wrap: break-word;
    max-width: 200px;
  }
  
  button {
    padding: 5px 10px;
    margin: 2px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .edit-btn {
    background-color: #ffeb3b;
    color: black;
  }
  
  .edit-btn:hover {
    background-color: #fbc02d;
  }
  
  .delete-btn {
    background-color: #f44336;
    color: white;
  }
  
  .delete-btn:hover {
    background-color: #d32f2f;
  }
  </style>
  