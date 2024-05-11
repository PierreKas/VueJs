<template>
  <body>
    <div class="container">
      <form>
        <label for="employeeId">Employee ID:</label>
        <input type="text" id="ID" placeholder="Enter Employee ID" v-model="employeeId" />
        <label for="employeeNameSS">Employee Name:</label>
        <input type="text" id="Names" placeholder="Enter Employee Name" v-model="employeeName" required />
        <label for="employeeSalary">Employee Salaryyy:</label>
        <input type="number" id="salary" placeholder="Enter Employee Salary" v-model="employeeSalary" required />
        <div class="submit">
          <button v-on:click="register">Register</button>
          <button v-on:click="updateEmployee">Update</button>
          <button v-on:click="deleteEmployee">Delete</button>
        </div>
      </form>

      <table>
        <thead>
          <tr>
            <th>Employee ID</th>
            <th>Employee Names</th>
            <th>Employee Salary</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="employee in employees" :key="employee.id">
            <td>{{ employee.id }}</td>
            <td>{{ employee.names }}</td>
            <td>{{ employee.salary }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </body>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      employeeId: '',
      employeeName: '',
      employeeSalary: '',
      role: '',
      employees: []
    }
  },
  created () {
    this.fetchEmployees()
  },
  methods: {
    async fetchEmployees () {
      try {
        const response = await axios.get('https://localhost:7228/api/Employee')
        this.employees = response.data
      } catch (error) {
        console.error(error)
      }
    },
    async register () {
      try {
        const result = await axios.post('https://localhost:7228/api/Employee', {
          //  ID: this.employeeId,
          Names: this.employeeName,
          salary: this.employeeSalary
        })
        console.warn(result)
        this.fetchEmployees()
      } catch (error) {
        console.error(error)
      }
    },
    async updateEmployee () {
      try {
        const result = await axios.put(`https://localhost:7228/api/Employee?id=${this.employeeId}`, {
          ID: this.employeeId,
          Names: this.employeeName,
          salary: this.employeeSalary
        })
        console.warn(result)
        this.fetchEmployees()
      } catch (error) {
        console.error(error)
      }
    },
    async deleteEmployee () {
      try {
        const result = await axios.delete(`https://localhost:7228/api/Employee/${this.employeeId}`)
        console.warn(result)
        this.employeeId = ''
        this.employeeName = ''
        this.employeeSalary = ''
        this.fetchEmployees()
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #ffffff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.container {
  max-width: 800px;
  width: 100%;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

form {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
  color: #0c3f92;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #0c3f92;
  border-radius: 3px;
  box-sizing: border-box;
}

input:focus {
  outline: none;
  box-shadow: 0 0 5px rgba(12, 63, 146, 0.5);
}

.submit {
  text-align: center;
}

button {
  background-color: #0c3f92;
  color: #ffffff;
  border: none;
  padding: 10px 20px;
  border-radius: 3px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-right: 10px;
}

button:last-child {
  margin-right: 0;
}

button:hover {
  background-color: #0a2c69;
}

table {
  width: 100%;
  border-collapse: collapse;
  background-color: #ffffff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

th, td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #0c3f92;
  color: #ffffff;
}

@media (max-width: 480px) {
  form {
    padding: 10px;
  }
}
</style>