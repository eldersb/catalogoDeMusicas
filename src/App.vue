<template>
  <v-card
    variant="flat"
  >
    <v-layout>
      <v-app-bar
        color="pink-lighten-1"
      >
        <template v-slot:prepend>
          <v-app-bar-nav-icon></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>Catálogo de músicas</v-app-bar-title>
        </v-app-bar>

        <v-main>
          <v-container fluid>
            <v-row>
              <v-col cols="12">
                  <createMusic></createMusic>
              </v-col>
            </v-row>
          </v-container>
        </v-main>

     
    </v-layout>
  </v-card>
</template>
