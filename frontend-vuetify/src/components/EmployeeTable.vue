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
          ID
        </th>
        <th class="text-left">
          Stanowisko
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
        <th class="text-left">
        </th>
      </tr>
    </thead>
    <tbody style="text-transform: capitalize;">
      <tr
        v-for="item in data"
        :key="item.id_pracownika"
        
      >
        <td class="pa-5">{{ item.idPracownika }}</td>
        <td>{{ item.stanowisko }}</td>
        <td>{{ item.imiePracownika }}</td>
        <td>{{ item.nazwiskoPracownika }}</td>
        <td>{{ item.wiekPracownika }}</td>
        <td><v-btn @click="deleteEmployee(item.idPracownika)" color="secondary">Usuń</v-btn></td>
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
          Dodaj pracownika
        </v-btn>
      </template>
       <v-form class="pa-15 bg-white dialog-form">
            <v-text-field
              v-model="imiePracownika"
              label="Imię pracownika"
              required
            ></v-text-field>
            <v-text-field
              v-model="nazwiskoPracownika"
              label="Nazwisko pracownika"
              required
            ></v-text-field>
            <v-text-field
              v-model="wiekPracownika"
              label="Wiek"
              required
            ></v-text-field>
            <v-text-field
              v-model="stanowisko"
              label="Stanowisko"
              required
            ></v-text-field>
            <v-btn
              color="secondary"
              @click="addEmployee"
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
      imiePracownika: '',
      nazwiskoPracownika: '',
      wiekPracownika: '',
      stanowisko: '',
      dialog: false
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

      deleteEmployee(id_pracownika) {
          axios.delete("http://localhost:3000/employees/"+id_pracownika)
          .then(() => {
          this.getItem();
        })
      },

      addEmployee(){
            axios.post('http://localhost:3000/employees', {
              imiePracownika: this.imiePracownika,
              nazwiskoPracownika: this.nazwiskoPracownika,
              wiekPracownika: this.wiekPracownika,
              stanowisko: this.stanowisko,
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
  