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
          ID zamówienia
        </th>
        <th class="text-left">
          ID produktu
        </th>
        <th class="text-left">
          Ilość produktu
        </th>
        <th class="text-left">
          ID magazyniera
        </th>
        <th class="text-left">
          ID przedawcy
        </th>
        <th class="text-left">
          Status zamówienia
        </th>
        <th class="text-left">
        </th>
      </tr>
    </thead>
    <tbody style="text-transform: capitalize;">
      <tr
        v-for="item in data"
        :key="item.idZamowienia"
        
      >
        <td class="pa-5">{{ item.idZamowienia }}</td>
        <td>{{ item.idProduktu }}</td>
        <td>{{ item.iloscProduktu }}</td>
        <td>{{ item.idMagazyniera }}</td>
        <td>{{ item.idSprzedawcy }}</td>
        <td>{{ item.statusZamowienia }}</td>
        <td><v-btn @click="deleteOrder(item.idZamowienia)" color="secondary">Usuń</v-btn></td>
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
          Dodaj zamówienie
        </v-btn>
      </template>
       <v-form class="pa-15 bg-white dialog-form">
            <v-text-field
              v-model="idProduktu "
              label="ID produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="iloscProduktu"
              label="Ilośc produktu"
              required
            ></v-text-field>
            <v-text-field
              v-model="idMagazyniera"
              label="ID magazyniera"
              required
            ></v-text-field>
            <v-text-field
              v-model="idSprzedawcy"
              label="ID sprzedawcy"
              required
            ></v-text-field>
            <v-text-field
              v-model="statusZamowienia"
              label="Status zamówienia"
              required
            ></v-text-field>
            <v-btn
              color="secondary"
              @click="addOrder"
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
      idZamowienia: '',
      idProduktu: '',
      iloscProduktu: '',
      idMagazyniera: '',
      idSprzedawcy: '',
      statusZamowienia: '',
      dialog: false
    }
      },
      methods: {

        async getItem() {
        axios.get("http://localhost:3000/orders")
        .then((response) => {
          this.data = response.data;
          console.log(response);
        })
      },

      async deleteOrder(idZamowienia) {
        let x = window.confirm("Czy na pewno chcesz usunąć to zamówienie?");
        if (x) {
          axios.delete("http://localhost:3000/orders/" + idZamowienia)
          .then(() => {
          this.getItem();
          alert("Zamówienie usunięte!");
        })
      }
      },
      
      async addOrder(){
            axios.post('http://localhost:3000/orders', {
              idProduktu: this.idProduktu,
              iloscProduktu: this.iloscProduktu,
              idMagazyniera: this.idMagazyniera,
              idSprzedawcy: this.idSprzedawcy,
              statusZamowienia: this.statusZamowienia
              
            })
            .then(response => {
              console.log(response)
            })
            .catch(error => {
              console.log(error)
            })
            alert("Zamówienie dodane!");
            window.location.reload();
          }
      },
      async mounted() {
        this.getItem();
      },
    }
</script>