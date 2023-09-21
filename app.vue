<template>
  <v-layout class="d-block">
    <v-app-bar v-if="!isHomePath" scroll-behavior="elevate" color="primary" variant="tonal" class="text-center">
      <v-app-bar-title class="font-weight-bold">
        Gerador de CPF Online
      </v-app-bar-title>
    </v-app-bar>
    <v-main style="min-height: 300px;" class="w-100">
      <NuxtPage/>
    </v-main>
    <v-divider></v-divider>
    <v-footer class="w-100 text-center" color="grey-1">
      <v-container>
        <v-row>
          <v-col>
            <p class="text-body-2">Gerador de CPF Online {{ new Date().getFullYear() }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-footer>
  </v-layout>
</template>
<style lang="css">
  .v-container {
    max-width: 980px;
  }
</style>
<script lang="ts" setup>
import { useRoute } from '#vue-router';
import { ref } from 'vue';
const route = useRoute();

const isHomePath = ref<boolean>(route.fullPath === '/');


</script>