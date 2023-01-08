<template>
    <v-layout class="fill-height">
        <v-row class="d-flex align-center justify-center text-left fill-height">
          <v-navigation-drawer>
            <v-list color="#00BCD4">
            <v-list-item class="nav-list-color" title="Pracownicy" to="/employees-table"></v-list-item>
            <v-list-item class="nav-list-color" title="Produkty" to="/products-table"></v-list-item>
            <v-list-item class="nav-list-color" title="Zamówienia" to="/orders-table"></v-list-item>
          </v-list>
          <template v-slot:append>
            <div class="pa-2">
              <v-btn 
              block 
              color="secondary"
              to="/"
              >
                Wyloguj się
              </v-btn>
            </div>
          </template>
          </v-navigation-drawer>
          <v-table
      fixed-header
      density="compact"
      class="w-50"
      style="border: 1px solid #00BCD4;"
      height="550px"
          >
      <thead>
        <tr>
          <th class="text-left">
            ID produktu
          </th>
          
          <th class="text-left">
            Nazwa produktu
          </th>
          <th class="text-left">
            Typ produktu
          </th>
          <th class="text-left">
            Rozmiar produktu
          </th>
          <th class="text-left">
            Kolor produktu
          </th>
          <th class="text-left">
           Stan magazynowy
          </th>
          <th class="text-left">
            Cena Produktu (ZŁ)
          </th>
        </tr>
      </thead>
      <tbody style="text-transform: capitalize;">
        <tr
          v-for="item in data"
          :key="item.id_pracownika"
        >
          <td>{{ item.idProduktu }}</td>
          <td>{{ item.nazwaProduktu }}</td>
          <td>{{ item.typProduktu }}</td>
          <td>{{ item.rozmiarProduktu }}</td>
          <td>{{ item.kolorProduktu }}</td>
          <td>{{ item.stanMagazynowy }}</td>
          <td>{{ item.cenaProduktu }}</td>
        </tr>
      </tbody>
    </v-table>
        </v-row>
      </v-layout>
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
          axios.get("http://localhost:3000/products")
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