<template>
    <ion-content class="ion-padding">
      <div class="flex justify-center items-center py-8">
        <ion-card class="w-full max-w-lg">
          <ion-card-header>
            <ion-card-title class="ion-text-center">PRIVILEGE CARE HOSPITAL</ion-card-title>
          </ion-card-header>
  
          <!-- Formulario de Personas -->
          <Personas
            v-if="!showUserForm"
            @person-registered="handlePersonRegistered"
          ></Personas>
  
          <!-- Formulario de Usuario -->
          <Usuario
            v-if="showUserForm"
            :persona-id="personaID"
            @user-registered="handleUserRegistered"
          ></Usuario>
  
          <!-- Botón para continuar con el registro -->
          <div v-if="!showUserForm" class="ion-text-center ion-margin-top">
            <ion-button expand="block" color="primary" @click="showUserForm = true">
              Continuar con Registro de Usuario
            </ion-button>
          </div>
        </ion-card>
      </div>
    </ion-content>
  </template>
  
  <script>
  import { IonContent, IonCard, IonCardHeader, IonCardTitle, IonButton } from "@ionic/vue";
/*   import Personas from "./personas.vue";
  import Usuario from "./usuario.vue"; */
  
  export default {
    components: {
/*    Personas,
      Usuario, */
      IonContent,
      IonCard,
      IonCardHeader,
      IonCardTitle,
      IonButton,
    },
    data() {
      return {
        showUserForm: false,
        personaID: null,
      };
    },
    methods: {
      handlePersonRegistered(personaID) {
        this.personaID = personaID;
        this.showUserForm = true;
      },
      handleUserRegistered() {
        // Lógica después de registrar al usuario
        this.showUserForm = false;
        this.personaID = null;
        alert("Usuario registrado exitosamente.");
      },
    },
  };
  </script>
  
  <style scoped>
  /* Agrega estilos personalizados si es necesario */
  </style>
  