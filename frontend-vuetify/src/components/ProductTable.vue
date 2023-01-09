<template>
  <v-layout class="fill-height d-flex flex-row align-center justify-center">
      <v-row class="d-flex flex-column align-center justify-center text-left fill-height">
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
        <th class="text-left pa-5">
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
        <th class="text-left">
        </th>
      </tr>
    </thead>
    <tbody style="text-transform: capitalize;">
      <tr
        v-for="item in data"
        :key="item.id_produktu"
      >
        <td class="pa-5">{{ item.idProduktu }}</td>
        <td>{{ item.nazwaProduktu }}</td>
        <td>{{ item.typProduktu }}</td>
        <td>{{ item.rozmiarProduktu }}</td>
        <td>{{ item.kolorProduktu  }}</td>
        <td>{{ item.stanMagazynowy }}</td>
        <td>{{ item.cenaProduktu }}</td>
        <td><v-btn @click="deleteProduct(item.idProduktu)" color="secondary">Usuń</v-btn></td>
      </tr>
    </tbody>
       </v-table>
       <v-dialog
       v-model="dialog"
       width="500" 
      >
        <template v-slot:activator="{ props }">
        <v-btn
          color="secondary"
          dark
          class="mt-5"
          v-bind="props"
          >
          Dodaj produkt
        </v-btn>
      </template>
       <v-form class="pa-15 bg-white dialog-form" >
            <v-text-field
              v-model="idProduktu"
              label="ID Produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="nazwaProduktu"
              label="Nazwa produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="typProduktu"
              label="Typ produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="rozmiarProduktu"
              label="Rozmiar produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="kolorProduktu"
              label="Kolor produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="stanMagazynowy"
              label="Stan magazynowy"
              required
            ></v-text-field>
            <v-text-field
              v-model="cenaProduktu"
              label="Cena produktu"
              required
            ></v-text-field>
            <v-btn
              color="secondary"
              @click="addProduct"
            >
              Dodaj
            </v-btn>
          </v-form>      
        </v-dialog>
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
      idProduktu: '',
      nazwaProduktu: '',
      typProduktu: '',
      rozmiarProduktu: '',
      kolorProduktu: '',
      stanMagazynowy: '',
      cenaProduktu: '',
      dialog: false
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

      deleteProduct(idProduktu) {
          axios.delete("http://localhost:3000/products/"+idProduktu)
          .then(() => {
          this.getItem();
        })
      },
      
      addProduct(){
            axios.post('http://localhost:3000/products', {
              idProduktu: this.idProduktu,
              nazwaProduktu: this.nazwaProduktu,
              typProduktu: this.typProduktu,
              rozmiarProduktu: this.rozmiarProduktu,
              kolorProduktu: this.kolorProduktu,
              stanMagazynowy: this.stanMagazynowy,
              cenaProduktu: this.cenaProduktu
              
            })
            .then(response => {
              console.log(response)
            })
            .catch(error => {
              console.log(error)
            })
            window.location.reload();
          }
      },
      mounted() {
        this.getItem();
      },
    }
</script>