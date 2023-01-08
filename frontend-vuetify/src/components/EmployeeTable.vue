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
    <tbody style="text-transform: capitalize;">
      <tr
        v-for="item in data"
        :key="item.id_pracownika"
      >
        <td>{{ item.idPracownika }}</td>
        <td>{{ item.imiePracownika }}</td>
        <td>{{ item.nazwiskoPracownika }}</td>
        <td>{{ item.wiekPracownika }}</td>
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
  