<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      absolute
      permanent
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
            Bienvenido!
          </v-list-item-title>
          <v-list-item-subtitle>
            Sistema de Registro
          </v-list-item-subtitle>
          <br>
          <br>
          <v-list-item-subtitle>
            Acciones realizables:
          </v-list-item-subtitle>
          <v-list-item-subtitle>
            Inicio de sesión
          </v-list-item-subtitle>
          <v-list-item-subtitle>
            Muestra de usuarios registrados
          </v-list-item-subtitle>
          <v-list-item-subtitle>
            Registro de nuevos usuarios
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-toolbar-title>CRUD con Firebase🔥 y Nuxt.js💻 - 🍄</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <Nuxt />
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({ drawer: null }),
  }
</script>