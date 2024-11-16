<template>
    <ion-content class="ion-padding">
      <div class="flex justify-center items-center py-8">
        <ion-card class="max-w-sm lg:max-w-4xl w-full shadow-lg overflow-hidden">
          <ion-row class="no-padding">
            <ion-col size-lg="6" class="hidden lg:block p-0">
              <div
                class="w-full h-full bg-cover"
                style="
                  background-image: url('https://media.revistagq.com/photos/5ca5fd6e3492a940f5bf1bf0/1:1/w_511,h_511,c_limit/doctor_mike_gq_5080.jpg');
                "
              ></div>
            </ion-col>
            <ion-col size-lg="6" size-xs="12" class="p-8">
              <h2 class="text-2xl font-semibold text-center">PRIVILEGE CARE</h2>
              <p class="text-xl text-center text-gray-600">HOSPITAL</p>
  
              <ion-button expand="block" fill="outline" class="mt-4" color="medium">
                <ion-icon name="logo-google" slot="start"></ion-icon>
                Inicia Sesión con Google
              </ion-button>
  
              <div class="mt-4 flex items-center justify-between">
                <span class="border-b w-1/5"></span>
                <p class="text-xs text-center text-gray-500 uppercase">
                  o Inicia Sesión con tu email
                </p>
                <span class="border-b w-1/5"></span>
              </div>
  
              <form @submit.prevent="login" class="mt-4">
                <ion-item>
                  <ion-select  label="Selecciona un Rol" label-placement="floating"
                    v-model="selectedRole"
                    @ionChange="fetchRole"
                    interface="popover"
                  >
                    <ion-select-option
                      v-for="role in roles"
                      :key="role.id"
                      :value="role.id"
                    >
                      {{ role.Nombre }}
                    </ion-select-option>
                  </ion-select>
                </ion-item>
  
                <ion-item>
                    <ion-input
                    v-model="usuario.Correo_Electronico"
                    type="email"
                    required label="Email"
                    label-placement="floating"
                    placeholder="Escribe tu email">
                    </ion-input>
                </ion-item>

                <ion-item>
                    <ion-input
                    v-model="usuario.Contrasena"
                    type="password"
                    required label="Contraseña"
                    label-placement="floating"
                    placeholder="Escribe tu contraseña">
                    <ion-input-password-toggle slot="end"></ion-input-password-toggle>
                    </ion-input>
                </ion-item>

  
                <ion-button expand="block" class="mt-8" type="submit" color="primary">
                  Iniciar Sesión
                </ion-button>
              </form>
  
              <div class="mt-4 flex items-center justify-between">
                <span class="border-b w-1/5"></span>
                <RouterLink to="/register">
                  <p class="text-xs text-gray-500 uppercase">o ¡Regístrate!</p>
                </RouterLink>
                <span class="border-b w-1/5"></span>
              </div>
  
              <ion-text
                v-if="mensaje"
                class="mt-4 text-center text-danger"
                color="danger"
              >
                {{ mensaje }}
              </ion-text>
              <ion-text
                v-if="token"
                class="mt-4 text-center text-success"
                color="success"
              >
                Token: {{ token }}
              </ion-text>
            </ion-col>
          </ion-row>
        </ion-card>
      </div>
    </ion-content>
  </template>
  
  <script>
  import {
    IonContent,
    IonButton,
    IonInput,
    IonItem,
    IonSelect,
    IonSelectOption,
    IonText,
    IonCard,
    IonRow,
    IonCol,
    IonIcon,
  } from "@ionic/vue";
  import axios from "axios";

  
  const apiClient = axios.create({
    baseURL: "https://back-end-hospital2-0.onrender.com/",
    headers: {
      Authorization: `Bearer ${localStorage.getItem("token")}`,
    },
  });
  
  export default {
    components: {
      IonContent,
      IonButton,
      IonInput,
      IonItem,
      IonSelect,
      IonSelectOption,
      IonText,
      IonCard,
      IonRow,
      IonCol,
      IonIcon,
    },
    data() {
      return {
        usuario: {
          Nombre_Usuario: "",
          Correo_Electronico: "",
          Numero_Telefonico_Movil: "",
          Contrasena: "",
        },
        roles: [],
        selectedRole: null,
        mensaje: "",
        token: "",
      };
    },
    async created() {
      try {
        const response = await apiClient.get("roles/");
        this.roles = response.data;
      } catch (error) {
        this.mensaje = "Error al cargar los roles";
      }
    },
    methods: {
      async login() {
        try {
          const response = await apiClient.post("login/", {
            ...this.usuario,
            Rol: this.selectedRole,
          });
          this.token = response.data.token;
          localStorage.setItem("token", this.token);
          localStorage.setItem("role", this.selectedRole);
          localStorage.setItem("correo", this.usuario.Correo_Electronico);
          this.$router.push("/dashboard");
        } catch (error) {
          this.mensaje =
            error.response?.data?.detail || "Error de conexión o acceso denegado";
        }
      },
      async fetchRole() {
        try {
          const response = await apiClient.get(`roles/${this.selectedRole}`);
          console.log(response.data);
        } catch (error) {
          this.mensaje = "Error al obtener el rol";
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Personaliza los estilos según sea necesario */
  </style>
  