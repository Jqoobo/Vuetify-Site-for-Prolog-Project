<template>
   <v-container class="fluid fill-height">
    <v-row class="align-center justify-center text-center fill-height">
        <v-card class="w-50 pa-15" variant="outlined" style="border: 1px solid #A7C7E7; border-radius: 10px;">
            <h1 class="pb-15">Logowanie</h1>
            <v-form
    ref="form"
    lazy-validation
    @submit.prevent="handleSubmit"
  >
  <v-alert type="error" title="Błąd logowania" class="mb-5 text-left" v-if="error">{{ error }}</v-alert>
    <v-text-field
      :counter="10"
      :rules="nameRules"
      label="Login"
      required
      v-model="username"
    ></v-text-field>
    <v-text-field
      :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
      :type="show1 ? 'text' : 'password'"
      name="input-10-2"
      label="Hasło"
      class="input-group--focused mt-5"
      @click:append="show1 = !show1"
      v-model="password"
      :counter="10"
    ></v-text-field>
    <v-btn
      color="secondary"
      class="mr-4 mt-5"
      type="submit"
    >
      Zaloguj się
    </v-btn>

</v-form>
</v-card>
</v-row>
  </v-container>
 </template>

<script>
import axios from 'axios';
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name:'Login',
    data () {
      return {
        username:'',
        password:'',
        show1: false,
        error: '',
      }
    },
    methods: {
      async handleSubmit () {
        try{
        const response = await axios.post('http://localhost:3000/auth/login', {
          username: this.username,
          password: this.password
        });
        console.log(response.data);
        localStorage.setItem('access_token', response.data.access_token);
        this.$router.push('/employees-table');
      } catch (e) {
        this.error = 'Niepoprawny login lub hasło.';
      }
    },
  },
}
</script>

