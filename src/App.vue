<template>
  <div id="app" class="small-container">     
    <!-- this is the same thing -->
    
    <Formulario @add:employee="addEmployee"></Formulario>
    <Tabla :employees="employees" 
    @delete:employee="deleteEmployee"
    @edit:employee="editEmployee"
    ></Tabla>
  </div>
</template>

<script>

import Formulario from './components/Formulario.vue';
import Tabla from './components/Tabla.vue';
export default {
  name: 'App',
  components: {
    Tabla,
    Formulario
  },
  data (){
    return {
      employees: [
        {
          id: 1,
          name : 'David Montiel',
          email : 'david.mercadoindustrial@gmail.com'
        },
        {
          id: 2,
          name : 'Rafael Montoya',
          email : 'timercadoindustrial@gmail.com'
        }
      ],
    }
  },
  methods: {
    addEmployee(employee) {
      const lastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };

      this.employees = [...this.employees, newEmployee];
      console.log(this.employees)
    },

    deleteEmployee(id) {
      this.employees = this.employees.filter(
        employee => employee.id !== id
      )
    },

    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map(employee =>
        employee.id === id ? updatedEmployee : employee
      )
    },
    cancelEdit(employee) {
      Object.assign(employee, this.cachedEmployee)
      this.editing = null;
    }

  }
}
</script>

<style>
button {
    background: #3d3d3d;
    border: 1px solid #000000;
  }

  .small-container {
    max-width: 680px;
  }
</style>
