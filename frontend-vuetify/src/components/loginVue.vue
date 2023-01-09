<template>
   <v-container class="fluid fill-height">
    <v-row class="align-center justify-center text-center fill-height">
        <v-card class="w-50 pa-15" variant="outlined" style="border: 1px solid #00BCD4; border-radius: 10px;">
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
      :rules="emailRules"
      :counter="10"
      label="E-mail"
      required
    ></v-text-field>

    <v-btn
      color="secondary"
      class="mr-4"
      to="/employees-table"
    >
      Zaloguj się
    </v-btn>

</v-form>
</v-card>
</v-row>
  </v-container>
 </template>

<script setup>
//
</script>

