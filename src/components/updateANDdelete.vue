<template>
    <body>
      <form>
         <!-- @submit.prevent="handelSubmit" -->
        <label for="employeeId">Employee ID:</label>
        <input type="text" id="ID" placeholder="Enter Employee ID" v-model="employeeId">
        <label for="employeeName">Employee Name:</label>
        <input type="text" id="Names" placeholder="Enter Employee Name" v-model="employeeName" required>
        <label for="employeeSalary">Employee Salary:</label>
        <input type="number" id="salary" placeholder="Enter Employee Salary" v-model="employeeSalary" required>
      </form>
      <div class="submit">
        <button v-on:click="updateEmployee">Update</button>
        <button v-on:click="deleteEmployee">Delete</button>
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
        role: ''
      }
    },
  
    // handelSubmit () {
    //   alert('Employee registered')
    // },
    methods: {
      async register () {
        try {
            const result = await axios.put(`https://localhost:7228/api/Employee/${this.employeeId}`, {
            ID: this.employeeId,
            Names: this.employeeName,
            salary: this.employeeSalary
          })
          console.warn(result)
        } catch (error) {
          console.error(error);
        }
      },
      async deleteEmployee() {
      try {
        const result = await axios.delete(`https://localhost:7228/api/Employee/${this.employeeId}`)
        console.warn(result)
        // Reset the form fields or show a success message
        this.employeeId = ''
        this.employeeName = ''
        this.employeeSalary = ''
      } catch (error) {
        console.error(error);
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
  
  form {
    background-color: #ffffff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    max-width: 400px;
    width: 100%;
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
  }
  
  button:hover {
    background-color: #0a2c69;
  }
  
  @media (max-width: 480px) {
    form {
      padding: 10px;
    }
  }
  </style>