<template>
   <v-container class="fluid fill-height">
    <v-row class="align-center justify-center text-center fill-height">
        <v-card class="w-50 pa-15" variant="outlined" style="border: 1px solid #A7C7E7; border-radius: 10px;">
            <h1 class="pb-15">Logowanie</h1>
            <v-form
    ref="form"
    lazy-validation
  >
    <v-text-field
      :counter="10"
      :rules="nameRules"
      label="Login"
      required
    ></v-text-field>
    <v-text-field
            :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
            :rules="[rules.required, rules.min]"
            :type="show1 ? 'text' : 'password'"
            name="input-10-2"
            label="Hasło"
            hint="Co najmniej 8 znaków"
            class="input-group--focused mt-5"
            @click:append="show1 = !show1"
    ></v-text-field>
    <v-btn
      color="secondary"
      class="mr-4 mt-5"
      to="/employees-table"
    >
      Zaloguj się
    </v-btn>

</v-form>
</v-card>
</v-row>
  </v-container>
 </template>

<script> 
  export default {
    data () {
      return {
        show1: false,
        password: 'Password',
        rules: {
          required: value => !!value || 'Wymagane',
          min: v => v.length >= 8 || 'Co najmniej 8 znaków',
          emailMatch: () => (`Hasło jest nieprawidłowe`),
        },
      }
    },
  }
</script>

