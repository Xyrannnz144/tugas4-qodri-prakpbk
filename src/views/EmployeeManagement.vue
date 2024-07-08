<template>
    <div class="container">
      <h1>Manajemen Pegawai</h1>
      <EmployeeList
        :employees="employees"
        @edit-employee="editEmployee"
        @delete-employee="deleteEmployee"
      />
      <EditEmployee
        :employee="selectedEmployee"
        v-if="editing"
        @save-employee="saveEmployee"
        @cancel-edit="cancelEdit"
      />
      <AddEmployee @add-employee="addEmployee" />
    </div>
  </template>
  
  <script>
  import EmployeeList from '@/components/EmployeeList.vue';
  import AddEmployee from '@/components/AddEmployee.vue';
  import EditEmployee from '@/components/EditEmployee.vue';
  
  export default {
    components: {
      EmployeeList,
      AddEmployee,
      EditEmployee
    },
    data() {
      return {
        employees: this.loadEmployees(),
        selectedEmployee: null,
        editing: false
      };
    },
    methods: {
      addEmployee(newEmployee) {
        const exists = this.employees.some(emp => emp.nip === newEmployee.nip);
        if (exists) {
          alert('Nomor Induk Pegawai sudah ada. Masukkan NIP yang berbeda.');
          return;
        }
        this.employees.push(newEmployee);
        this.saveEmployees();
      },
      editEmployee(employee) {
        this.selectedEmployee = { ...employee };
        this.editing = true;
      },
      deleteEmployee(employeeId) {
        if (confirm('Anda yakin ingin menghapus data pegawai ini?')) {
          this.employees = this.employees.filter(emp => emp.id !== employeeId);
          this.selectedEmployee = null;
          this.editing = false;
          this.saveEmployees();
        }
      },
      saveEmployee(updatedEmployee) {
        const index = this.employees.findIndex(emp => emp.id === updatedEmployee.id);
        if (index !== -1) {
          const existsNip = this.employees.some(emp => emp.nip === updatedEmployee.nip && emp.id !== updatedEmployee.id);
          if (existsNip) {
            alert('NIP sudah ada. Masukkan NIP yang berbeda.');
            return;
          }
          this.employees.splice(index, 1, updatedEmployee);
          this.selectedEmployee = updatedEmployee;
          this.saveEmployees();
        }
        this.editing = false;
      },
      cancelEdit() {
        this.editing = false;
        this.selectedEmployee = null;
      },
      saveEmployees() {
        localStorage.setItem('employees', JSON.stringify(this.employees));
      },
      loadEmployees() {
        const data = localStorage.getItem('employees');
        return data ? JSON.parse(data) : [];
      }
    }
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 800px;
    margin: 40px auto;
    padding: 20px;
    background-color: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  h1 {
    color: #333;
    margin-bottom: 20px;
  }
  </style>
  