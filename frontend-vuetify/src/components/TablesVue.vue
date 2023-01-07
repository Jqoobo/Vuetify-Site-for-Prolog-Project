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
          Nazwa gry
        </th>
        <th class="text-left">
          Ocena
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="item in desserts"
        :key="item.name"
      >
        <td>{{ item.name }}</td>
        <td>{{ item.ocena }}</td>
      </tr>
    </tbody>
  </v-table>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    data () {
      return {
        desserts: [
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
          {
            name: 'Elden Ring',
            ocena: 10,
          },
        ],
      }
    },
  }
</script>
  