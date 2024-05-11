<template>
  <EmployeeForm />
</template>

<script>
import EmployeeForm from './components/EmployeeForm.vue';

export default {
  name: 'App',
  components: { EmployeeForm }

  // async mounted(){
  //   let result = await axios.get("https://localhost:7228/api/Employee")
  //   console.warn(result)
  // }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>