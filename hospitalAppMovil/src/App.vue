<template>
  <ion-app>
    <ion-router-outlet />
    <!-- Aquí se renderizan las páginas según la ruta actual -->
    <router-view />
  </ion-app>
</template>

<script setup>
import { IonApp, IonRouterOutlet } from '@ionic/vue';
</script>
