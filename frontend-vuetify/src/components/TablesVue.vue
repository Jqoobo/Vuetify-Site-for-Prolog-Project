<template>
    <v-container class="fill-height">
      <v-row class="d-flex align-center justify-center text-left fill-height">

        <v-table
    fixed-header
    class="w-50"
    style="border: 1px solid #00BCD4; border-radius: 10px;"
        >
    <thead>
      <tr>
        <th class="text-left">
          ID
        </th>
        
        <th class="text-left">
          Imię pracownika
        </th>
        <th class="text-left">
          Nazwisko pracownika
        </th>
        <th class="text-left">
          Wiek
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="item in data"
        :key="item.id_pracownika"
      >
        <td>{{ item.idPracownika }}</td>
        <td>{{ item.imiePracownika }}</td>
        <td>{{ item.nazwiskoPracownika }}</td>
        <td>{{ item.wiekPracownika }}</td>
        <td></td>
      </tr>
    </tbody>
  </v-table>
      </v-row>
    </v-container>
  </template>
  
  
<script>
    import axios from 'axios'
    export default{
      name:'TabelsVue',
      data(){
     return {
      data: [],
    }
      },
      methods: {
        getItem() {
        axios.get("http://localhost:3000/employees")
        .then((response) => {
          this.data = response.data;
          console.log(response);
        })
      },
      },
      created() {
        this.getItem();
      },
    }

</script>
  