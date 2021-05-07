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
      employees: [],
    }
  },

  mounted() {
    this.getEmployees()
  },

  methods: {
    async getEmployees() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users')
        const data = await response.json()
        this.employees = data
      } catch (error) {
        console.error(error)
      }
    },

     async addEmployee(employee) {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users', {
          method: 'POST',
          body: JSON.stringify(employee),
          headers: { "Content-type": "application/json; charset=UTF-8" }
        })
        const data = await response.json()
        this.employees = [...this.employees, data]
      } catch (error) {
        console.error(error)
        }
      },
      async editEmployee(id, updatedEmployee) {
        try {
          const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
            method: 'PUT',
            body: JSON.stringify(updatedEmployee),
            headers: { "Content-type": "application/json; charset=UTF-8" }
          })
          const data = await response.json()
          this.employees = this.employees.map(employee => employee.id === id ? data : employee)
        } catch (error) {
          console.error(error)
        }
      },
      async deleteEmployee(id) {
        try {
          await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
            method: 'DELETE'
          })
          this.employees = this.employees.filter(employee => employee.id !== id)
        } catch (error) {
          console.error(error)
        }
      },


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
