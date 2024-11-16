<template>
  <div class="container-fluid">
    <br />
    <b-row>
      <b-col>
        <h2 class="alert alert-primary text-center uppercase text-">
          Operaciones CRUD Personal Medico
        </h2>
        <div class="grid grid-cols-1">
          <div class="md:col-span-3">
            <!-- buscador de la tabla   -->
            <nav
              class="flex items-center justify-between bg-white p-4 shadow-md"
            >
              <div class="flex items-center">
                <div class="">
                  <form action="#" class="flex items-center w-full">
                    <input
                      type="text"
                      class="border border-gray-300 rounded-full pl-4 pr-12 py-2 bg-gray-50 focus:outline-none focus:border-blue-500 w-full placeholder-gray-500"
                      title="searchField"
                      placeholder="Buscar"
                      v-model="searchInput"
                    />
                    <button
                      class="absolute right-0 mr-3 text-gray-500 hover:text-gray-700"
                    >
                      <i class="ri-search-line"></i>
                    </button>
                  </form>
                </div>
              </div>

              <!-- Notificación -->
              <!-- <div
                v-if="notification.show"
                :class="`flex items-center px-4 py-3 ${
                  notification.type === 'éxito' ? 'bg-red-500' : 'bg-green-500'
                } text-white text-sm font-bold border rounded-md`"
                role="alert"
              >
  
                <p>{{ notification.type }}</p>
                <svg
                  class="fill-current w-4 h-4 mr-2"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                >
                  <path
                    v-if="notification.type === 'éxito'"
                    d="M12.432 0c1.34 0 2.01.912 2.01 1.957 0 1.305-1.164 2.512-2.679 2.512-1.269 0-2.009-.75-1.974-1.99C9.789 1.436 10.67 0 12.432 0zM8.309 20c-1.058 0-1.833-.652-1.093-3.524l1.214-5.092c.211-.814.246-1.141 0-1.141-.317 0-1.689.562-2.502 1.117l-.528-.88c2.572-2.186 5.531-3.467 6.801-3.467 1.057 0 1.233 1.273.705 3.23l-1.391 5.352c-.246.945-.141 1.271.106 1.271.317 0 1.357-.392 2.379-1.207l.6.814C12.098 19.02 9.365 20 8.309 20z"
                  />
                  <path
                    v-if="notification.type === 'error'"
                    d="M10 2C5.029 2 1 6.029 1 11s4.029 9 9 9 9-4.029 9-9S14.971 2 10 2zm0 16a7 7 0 1 1 0-14 7 7 0 0 1 0 14zm-.707-7.707a1 1 0 0 0 0-1.414L8.586 8.586a1 1 0 1 0-1.414 1.414L8.293 11l-1.707 1.707a1 1 0 0 0 1.414 1.414L9 12.414l1.707 1.707a1 1 0 0 0 1.414-1.414L10.707 11z"
                  />
                </svg>
                <p>{{ notification.message }}</p>
              </div> -->

              <div>
                <!-- Regresar a uno -->
                <button
                  @click="showModal = true"
                  class="flex items-center text-blue-500 hover:text-blue-700"
                >
                  <svg
                    class="h-10 w-10"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  >
                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                    <line x1="12" y1="8" x2="12" y2="16" />
                    <line x1="8" y1="12" x2="16" y2="12" />
                  </svg>
                  <h5 class="ml-2 uppercase font-bold">crear</h5>
                  <!-- Añadimos un margen a la izquierda -->
                </button>
              </div>
            </nav>
            <div class="overflow-x-auto">
              <table class="min-w-full bg-white border border-gray-300 table-hover">
                <thead>
                  <tr class="bg-gray-200 text-gray-600 uppercase text-xs leading-normal">
                    <th class="py-3 px-6 text-left">No°</th>
                    <th class="py-3 px-6 text-left">Persona ID</th>
                    <th class="py-3 px-6 text-left">Departamento</th>
                    <th class="py-3 px-6 text-left">Cédula Profesional</th>
                    <th class="py-3 px-6 text-left">Tipo</th>
                    <th class="py-3 px-6 text-left">Especialidad</th>
                    <th class="py-3 px-6 text-left">Fecha de Contratación</th>
                    <th class="py-3 px-6 text-left">
                      Fecha de Término de Contrato
                    </th>
                    <th class="py-3 px-6 text-left">Salario</th>
                    <th class="py-3 px-6 text-left">Estatus</th>
                    <th class="py-3 px-6 text-left">Fecha de Registro</th>
                    <th class="py-3 px-6 text-left">Fecha de Actualización</th>
                    <th class="py-3 px-6 text-left">Edita</th>
                    <th class="py-3 px-6 text-left">Elimina</th>
                  </tr>
                </thead>
                <tbody class="text-gray-600 text-xs font-light">
                  <tr v-for="(personal, index) in personalData" :key="personal.Persona_ID" class="text-center">
                    <td class="py-3 px-6 text-left whitespace-nowrap truncate">
                      {{ index + 1 }}
                    </td>
                    <td class="text-sm">{{ personal.Persona_ID }}</td>
                    <td class="text-sm">{{ personal.Departamento_ID }}</td>
                    <td class="text-sm">{{ personal.Cedula_Profesional }}</td>
                    <td class="text-sm">{{ personal.Tipo }}</td>
                    <td class="text-sm">{{ personal.Especialidad }}</td>
                    <td class="text-sm">
                      {{ formatearFecha(personal.Fecha_Contratacion) }}
                    </td>
                    <td class="text-sm">
                      {{ formatearFecha(personal.Fecha_Termino_Contrato) }}
                    </td>
                    <td class="text-sm">{{ personal.Salario }}</td>
                    <td>
                      <span v-if="personal.Estatus === 'Activo'" class="text-green-500 font-bold">Activo</span>
                      <span v-else class="text-red-500 font-bold">{{
                        personal.Estatus
                      }}</span>
                    </td>
                    <td class="text-sm">
                      {{ formatearFecha(personal.Fecha_Registro) }}
                    </td>
                    <td class="text-sm">
                      {{ formatearFecha(personal.Fecha_Actualizacion) }}
                    </td>
                    <td class="text-center px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                      <a class="iq-icons-list" href="#" @click="openEditModal(personal)">
                        <div class="icon" style="color: blue; font-size: 25px">
                          <svg class="h-7 w-7 text-blue-500 hover:text-blue-900" viewBox="0 0 24 24" stroke-width="2"
                            stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">
                            <path stroke="none" d="M0 0h24v24H0z" />
                            <path d="M9 7 h-3a2 2 0 0 0 -2 2v9a2 2 0 0 0 2 2h9a2 2 0 0 0 2 -2v-3" />
                            <path d="M9 15h3l8.5 -8.5a1.5 1.5 0 0 0 -3 -3l-8.5 8.5v3" />
                            <line x1="16" y1="5" x2="19" y2="8" />
                          </svg>
                        </div>
                      </a>
                    </td>
                    <td class="text-center px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                      <a class="iq-icons-list" href="#" @click.prevent="deletePersonal(personal.Persona_ID)">
                        <div class="icon" style="
                            color: red;
                            font-size: 25px;
                            text-align: center;
                          ">
                          <svg class="h-7 w-7 text-red-500 hover:text-red-900" width="24" height="24"
                            viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none"
                            stroke-linecap="round" stroke-linejoin="round">
                            <path stroke="none" d="M0 0h24v24H0z" />
                            <line x1="4" y1="7" x2="20" y2="7" />
                            <line x1="10" y1="11" x2="10" y2="17" />
                            <line x1="14" y1="11" x2="14" y2="17" />
                            <path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
                            <path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
                          </svg>
                        </div>
                      </a>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <!-- Modal -->
          <div
            v-if="showModal"
            class="fixed inset-0 flex items-center justify-center bg-gray-900 bg-opacity-50"
          >
            <div
              class="bg-white p-6 rounded shadow-lg w-full max-w-2xl relative"
            >
              <button
                @click="(showModal = false), (this.formPersona = {})"
                class="absolute top-3 right-3 text-gray-600 hover:text-gray-900"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  aria-hidden="true"
                >
                  <path
                    fill-rule="evenodd"
                    d="M10 9.293L14.707 4.586a1 1 0 10-1.414-1.414L10 7.465 5.707 3.293a1 1 0 00-1.414 1.414L8.586 9.293 4.293 13.586a1 1 0 101.414 1.414L10 10.707l4.293 4.293a1 1 0 001.414-1.414L10 9.293z"
                    clip-rule="evenodd"
                  />
                </svg>
              </button>
              <h2 class="text-lg font-semibold text-center mb-4">
                <!-- {{ currentSolicitud.id ? 'Editar Solicitud' : 'Nueva Solicitud' }} -->
                Registrar Datos Personales
              </h2>
              <form ref="FormularioPersona">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                  <!-- Nombre Completo -->
                  <div class="flex flex-col">
                    <label
                      for="estatus"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Titulo de Cortesia
                    </label>
                    <select
                      v-model="formPersona.tituloCortesia"
                      name="tituloCortesia"
                      id="tituloCortesia"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option
                        v-for="tituloCortesia in tituloCortesia"
                        :key="tituloCortesia"
                        :value="tituloCortesia"
                      >
                        {{ tituloCortesia }}
                      </option>
                    </select>
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="nombre"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Nombre
                    </label>
                    <input
                      v-model="formPersona.nombre"
                      type="text"
                      name="nombre"
                      id="nombre"
                      placeholder="Nombre"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="primer-apellido"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Primer Apellido
                    </label>
                    <input
                      v-model="formPersona.primerApellido"
                      type="text"
                      name="primer-apellido"
                      id="primer-apellido"
                      placeholder="Primer Apellido"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="segundo-apellido"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Segundo Apellido
                    </label>
                    <input
                      v-model="formPersona.segundoApellido"
                      type="text"
                      name="segundo-apellido"
                      id="segundo-apellido"
                      placeholder="Segundo Apellido"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="curp"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      CURP
                    </label>
                    <input
                      v-model="formPersona.curp"
                      type="text"
                      name="curp"
                      id="curp"
                      placeholder="CURP"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="genero"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Género
                    </label>
                    <select
                      v-model="formPersona.genero"
                      name="genero"
                      id="genero"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option
                        v-for="genero in generos"
                        :key="genero"
                        :value="genero"
                      >
                        {{ genero }}
                      </option>
                    </select>
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="tipo-sangre"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Tipo de Sangre
                    </label>
                    <select
                      v-model="formPersona.tipoSangre"
                      name="tipo-sangre"
                      id="tipo-sangre"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option
                        v-for="tipoSangre in tiposSangre"
                        :key="tipoSangre.value"
                        :value="tipoSangre.value"
                      >
                        {{ tipoSangre.label }}
                      </option>
                    </select>
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="fecha-nacimiento"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Fecha de Nacimiento
                    </label>
                    <input
                      v-model="formPersona.fechaNacimiento"
                      type="date"
                      name="fecha-nacimiento"
                      id="fecha-nacimiento"
                      value="2003-01-01"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <!-- <div class="flex flex-col">
                    <label
                      for="fotografia"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Fotografía
                    </label>
                    <input
                      v-model="formPersona.fotografia"
                      type="text"
                      name="fotografia"
                      id="fotografia"
                      placeholder="URL de la Fotografía"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div> -->

                  <div class="flex flex-col">
                    <label
                      for="telefono"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Teléfono
                    </label>
                    <input
                      v-model="formPersona.telefono"
                      type="text"
                      name="telefono"
                      id="telefono"
                      placeholder="Teléfono"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="correo-electronico"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Correo Electrónico
                    </label>
                    <input
                      v-model="formPersona.correoElectronico"
                      type="email"
                      name="correo-electronico"
                      id="correo-electronico"
                      placeholder="Correo Electrónico"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <div class="flex flex-col">
                    <label
                      for="estatus"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Estatus
                    </label>
                    <select
                      v-model="formPersona.estatus"
                      name="estatus"
                      id="estatus"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option
                        v-for="estatus in estatuses"
                        :key="estatus.value"
                        :value="estatus.value"
                      >
                        {{ estatus.label }}
                      </option>
                    </select>
                  </div>

                  <div class="col-span-2 text-center">
                    <a
                      class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-base font-semibold text-white outline-none"
                      @click="extractFormPersona"
                      data-accordion-target="#accordion-color-body-1"
                      aria-expanded="true"
                      aria-controls="accordion-color-body-1"
                    >
                      Registrar
                    </a>
                  </div>
                </div>
              </form>
            </div>
          </div>

          <div
            v-if="showModal2"
            class="fixed inset-0 flex items-center justify-center bg-gray-900 bg-opacity-50"
          >
            <div
              class="bg-white p-6 rounded shadow-lg w-full max-w-2xl relative"
            >
              <button
                @click="(showModal2 = false), (this.formPersonalMedico = {})"
                class="absolute top-3 right-3 text-gray-600 hover:text-gray-900"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  aria-hidden="true"
                >
                  <path
                    fill-rule="evenodd"
                    d="M10 9.293L14.707 4.586a1 1 0 10-1.414-1.414L10 7.465 5.707 3.293a1 1 0 00-1.414 1.414L8.586 9.293 4.293 13.586a1 1 0 101.414 1.414L10 10.707l4.293 4.293a1 1 0 001.414-1.414L10 9.293z"
                    clip-rule="evenodd"
                  />
                </svg>
              </button>
              <h2 class="text-lg font-semibold text-center mb-4">
                <h2>Datos Laborales</h2>
              </h2>
              <form ref="FormularioPersona">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                  <!-- Departamento_ID -->
                  <div class="flex flex-col">
                    <label
                      for="Departamento"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Departamento
                    </label>
                    <select
                      v-model="formPersonalMedico.Departamento_ID"
                      name="Departamento"
                      id="Departamento"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option
                        v-for="Departamento in Departamentos"
                        :key="Departamento.value"
                        :value="Departamento.value"
                      >
                        {{ Departamento.label }}
                      </option>
                    </select>
                  </div>
                  <!-- Cédula Profesional -->
                  <div class="flex flex-col">
                    <label
                      for="cedula_profesional"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Cédula Profesional
                    </label>
                    <input
                      v-model="formPersonalMedico.Cedula_Profesional"
                      type="text"
                      name="cedula_profesional"
                      id="cedula_profesional"
                      placeholder="Cédula Profesional"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <!-- Tipo -->
                  <div class="flex flex-col">
                    <label
                      for="Tipo"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Tipo
                    </label>
                    <select
                      v-model="formPersonalMedico.Tipo"
                      name="Tipo"
                      id="Tipo"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option v-for="Tipo in Tipos" :key="Tipo" :value="Tipo">
                        {{ Tipo }}
                      </option>
                    </select>
                  </div>

                  <!-- Especialidad -->
                  <div class="flex flex-col">
                    <label
                      for="especialidad"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Especialidad
                    </label>
                    <input
                      v-model="formPersonalMedico.Especialidad"
                      type="text"
                      name="especialidad"
                      id="especialidad"
                      placeholder="Especialidad"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <!-- Fecha de Contratación -->
                  <div class="flex flex-col">
                    <label
                      for="fecha_contratacion"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Fecha de Contratación
                    </label>
                    <input
                      v-model="formPersonalMedico.Fecha_Contratacion"
                      type="date"
                      name="fecha_contratacion"
                      id="fecha_contratacion"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <!-- Fecha de Término de Contrato -->
                  <div class="flex flex-col">
                    <label
                      for="fecha_termino_contrato"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Fecha de Término de Contrato
                    </label>
                    <input
                      v-model="formPersonalMedico.Fecha_Termino_Contrato"
                      type="date"
                      name="fecha_termino_contrato"
                      id="fecha_termino_contrato"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <!-- Salario -->
                  <div class="flex flex-col">
                    <label
                      for="salario"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Salario
                    </label>
                    <input
                      v-model="formPersonalMedico.Salario"
                      type="number"
                      name="salario"
                      id="salario"
                      placeholder="Salario"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    />
                  </div>

                  <!-- Estatus -->
                  <div class="flex flex-col">
                    <label
                      for="estatus"
                      class="mb-2 text-base font-medium text-[#07074D]"
                    >
                      Estatus
                    </label>
                    <select
                      v-model="formPersonalMedico.Estatus"
                      name="estatus"
                      id="estatus"
                      class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
                    >
                      <option
                        v-for="estatus in estatuses"
                        :key="estatus.label"
                        :value="estatus.label"
                      >
                        {{ estatus.label }}
                      </option>
                    </select>
                  </div>

                  <div class="col-span-2 text-center">
                    <a
                      class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-base font-semibold text-white outline-none"
                      @click="extractFormPersonalMedico"
                    >
                      {{ isUpdating ? "Actualizar" : "Registrar" }}
                    </a>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </b-col>
    </b-row>
    <br />
    <!-- Pagination Controls -->
    <div class="flex justify-between items-center mt-2">
      <button
        @click="previousPage"
        :disabled="currentPage === 1"
        class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700"
      >
        Anterior
      </button>
      <span class="text-gray-700"
        >Página {{ currentPage }} de {{ totalPages }}</span
      >
      <button
        @click="nextPage"
        :disabled="currentPage === totalPages"
        class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700"
      >
        Siguiente
      </button>
    </div>
    <br />
  </div>
</template>

<style>
.hover-zoom {
  transition: transform 0.3s;
}

.hover-zoom:hover {
  transform: scale(1.05);
}
</style>

<script>
import axios from "axios";

import moment from "moment";

const body = document.getElementsByTagName("body");

const token =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6ImpvbmEyMyIsIkNvcnJlb19FbGVjdHJvbmljbyI6InN0cmluZyIsIkNvbnRyYXNlbmEiOiIxMjM0IiwiTnVtZXJvX1RlbGVmb25pY29fTW92aWwiOiJzdHJpbmcifQ.uGxblZ3LX-pRNbXaGEAs41QWESPwqCIdHmBqokYgPIA";

const apiClient = axios.create({
  baseURL: "https://back-end-hospital2-0.onrender.com/",
  headers: {
    Authorization: `Bearer ${token}`,
  },
});

// const apiClient = axios.create({
//   baseURL: 'https://back-end-hospital2-0.onrender.com/',
//   headers: {
//     'Authorization': `Bearer ${localStorage.getItem('token')}`
//   }
// });

export default {
  name: "AprobacionesModal",
  data() {
    return {
      isUpdating: false,
      formPersona: {
        tituloCortesia: "",
        nombre: "",
        primerApellido: "",
        segundoApellido: "",
        curp: "",
        genero: "",
        tipoSangre: "",
        fechaNacimiento: "",
        fotografia: "",
        telefono: "",
        correoElectronico: "",
        Estatus: "",
        fechaRegistro: "",
        fechaActualizacion: "",
      },

      formPersonalMedico: {
        Persona_ID: "",
        Departamento_ID: "",
        Cedula_Profesional: "",
        Tipo: "",
        Especialidad: "",
        Fecha_Contratacion: "",
        Fecha_Termino_Contrato: "",
        Salario: "",
        Estatus: false,
      },

      idInsertado: "",
      solicitudes: [],
      api: "http://127.0.0.1:8000/personal_medico/",

      estatuses: [
        { label: "Activo", value: true },
        { label: "Inactivo", value: false },
      ],
      tituloCortesia: [
        "Sr.",
        "Sra.",
        "Srta.",
        "Dr.",
        "Dra.",
        "Ing.",
        "Lic.",
        "Mtro.",
        "Prof.",
        "Arq.",
      ],

      generos: ["Masculino", "Femenino"],
      tiposSangre: [
        { label: "A+", value: "A+" },
        { label: "A-", value: "A-" },
        { label: "B+", value: "B+" },
        { label: "B-", value: "B-" },
        { label: "AB+", value: "AB+" },
        { label: "AB-", value: "AB-" },
        { label: "O+", value: "O+" },
        { label: "O-", value: "O-" },
      ],
      Tipos: [
        "Médico",
        "Enfermero",
        "Administrativo",
        "Directivo",
        "Apoyo",
        "Residente",
        "Interno",
      ],

      Departamentos: [
        { label: "Urgencias", value: 1 },
        { label: "Pediatría", value: 2 },
        { label: "Ginecología", value: 3 },
        { label: "Oncología", value: 4 },
        { label: "Cardiología", value: 5 },
        { label: "Cirugía General", value: 6 },
        { label: "Radiología", value: 7 },
        { label: "Laboratorio", value: 8 },
        { label: "Medicina Interna", value: 9 },
        { label: "Rehabilitación", value: 10 },
        { label: "Psiquiatría", value: 11 },
        { label: "Anestesiología", value: 12 },
        { label: "Dermatología", value: 13 },
        { label: "Endocrinología", value: 14 },
        { label: "Neumología", value: 15 },
        { label: "Traumatología", value: 16 },
        { label: "Oftalmología", value: 17 },
      ],

      showModal: false,
      showModal2: false,
      personData: [],
      personalData: [],
      searchInput: "",
      currentPage: 1, // Página actual
      resultsPerPage: 10, // Resultados por página
      totalPages: 1, // Total de páginas
      paginatedData: [], // Datos de la página actual
      currentPersonal: {},
      config: {
        dateFormat: "Y-m-d",
        inline: true,
      },

      dataTable: [], // Datos de la tabla

      notification: {
        show: false,
        message: "",
        type: "", // "success" o "error"
      },
    };
  },

  mounted() {
    body[0].classList.add("sidebar-main-menu");
    console.log("DOM is rendered");
    console.log(Object.keys(this.formPersona).length);
    this.getPersonalMedico();
  },

  unmounted() {
    body[0].classList.remove("sidebar-main-menu");
  },

  created() {
    console.log("DOM is created");
  },

  methods: {
    extractFormPersona() {
      // Obtener la fecha actual en formato ISO 8601 (incluye tiempo)
      const fechaActual = new Date().toISOString();

      // Crear un objeto con los datos del formulario
      const personaInformacion = {
        Titulo_Cortesia: this.formPersona.tituloCortesia,
        Nombre: this.formPersona.nombre,
        Primer_Apellido: this.formPersona.primerApellido,
        Segundo_Apellido: this.formPersona.segundoApellido,
        CURP: this.formPersona.curp,
        Genero: this.formPersona.genero,
        Tipo_Sangre: this.formPersona.tipoSangre,
        Fecha_Nacimiento: this.formPersona.fechaNacimiento,
        Fotografia: this.formPersona.fotografia || "No se guardo fotografia",
        Telefono: this.formPersona.telefono,
        Correo_Electronico: this.formPersona.correoElectronico,
        Estatus: this.formPersona.estatus || true,
        Fecha_Registro: fechaActual, // Asignar fecha actual
        Fecha_Actualizacion: fechaActual, // Asignar fecha actual
      };

      console.log(personaInformacion);

      const apiUrl = "http://127.0.0.1:8000/person/";

      axios
        .post(apiUrl, personaInformacion)
        .then((response) => {
          // Recupero el ID insertado

          this.idInsertado = response.data.ID;
          console.log("ID del nuevo registro:", this.idInsertado);
          console.log("Datos enviados a la base:", response.data);
          this.showModal2 = true;
          this.showModal = false;
        })
        .catch((error) => {
          // Handle API request errors (e.g., show error message)
          console.error("Error sending data:", error);
        });
    },

    extractFormPersonalMedico() {
      // Obtener la fecha actual en formato ISO 8601 (incluye tiempo)
      const fechaActual = new Date().toISOString();

      // Crear un objeto con los datos del formulario
      const personalMedicoInformacion = {
        Persona_ID: this.idInsertado,
        Departamento_ID: this.formPersonalMedico.Departamento_ID || "",
        Cedula_Profesional: this.formPersonalMedico.Cedula_Profesional || "",
        Tipo: this.formPersonalMedico.Tipo || "",
        Especialidad: this.formPersonalMedico.Especialidad || "",
        Fecha_Contratacion:
          this.formPersonalMedico.Fecha_Contratacion || fechaActual,
        Fecha_Termino_Contrato:
          this.formPersonalMedico.Fecha_Termino_Contrato || fechaActual,
        Salario: this.formPersonalMedico.Salario || 0,
        Estatus: this.formPersonalMedico.Estatus || "",
        Fecha_Registro: fechaActual, // Asignar fecha actual
        Fecha_Actualizacion: fechaActual, // Asignar fecha actual
      };

      console.log(personalMedicoInformacion);

      // Determinar la URL y el método según si estamos actualizando o creando
      const isUpdating = !!this.formPersonalMedico.Persona_ID; // Verifica si ya existe Persona_ID
      const apiUrl = isUpdating
        ? `http://127.0.0.1:8000/personal_medico/${this.formPersonalMedico.Persona_ID}`
        : "http://127.0.0.1:8000/personal_medico/";
      const method = isUpdating ? "PUT" : "POST"; // Determinar el método a usar

      // Usar axios para hacer la solicitud
      axios
        .request({
          method: method,
          url: apiUrl,
          data: isUpdating
            ? this.formPersonalMedico
            : personalMedicoInformacion, // Enviar datos correctos
        })
        .then((response) => {
          console.log(
            "Datos del personal médico enviados a la base:",
            response.data
          );
          this.showModal2 = false;
          // Aquí podrías actualizar la lista de personal médico si es necesario
          this.getPersonalMedico(); // Volver a cargar la lista de personal médico
        })
        .catch((error) => {
          // Manejar errores de la solicitud a la API (por ejemplo, mostrar un mensaje de error)
          console.error("Error enviando datos:", error);
        });
    },

    async getPersonalMedico() {
      try {
        const response = await apiClient.get(this.api);
        this.formPersonalMedico = response.data;
        this.personalData = response.data;
        console.log("Datos de la API personal médico:", this.personalData);
      } catch (error) {
        console.error("Error al obtener datos de personal:", error);
      }
    },

    openEditModal(personalData) {
      // Cargar los datos del registro seleccionado en el formulario
      this.formPersonalMedico = { ...personalData }; // Clonar el objeto para evitar referencias
      this.showModal2 = true; // Abrir el modal
      this.isUpdating = true;
    },

    deletePersonal(personaId) {
      // Define la URL de la API con el ID del personal médico a eliminar
      const apiUrl = `http://127.0.0.1:8000/personal_medico/${personaId}`;

      // Configura los encabezados para la solicitud
      const headers = {
        Authorization: `Bearer ${token}`, // Asegúrate de que 'token' esté definido
      };

      // Realiza la solicitud DELETE a la API
      axios
        .delete(apiUrl, { headers }) // Pasa los encabezados en la solicitud
        .then((response) => {
          console.log("Registro eliminado:", response.data);
          // Aquí puedes actualizar el estado o la lista de personal médico si es necesario
          this.getPersonalMedico(); // Por ejemplo, volver a cargar la lista
        })
        .catch((error) => {
          console.error("Error eliminando el registro:", error);
          // Manejar errores, por ejemplo, mostrando un mensaje al usuario
        });
    },

    // Actualiza la paginación basada en la búsqueda y el número total de solicitudes
    updatePagination() {
      console.log("Actualizando la paginación...");

      const searchQuery = this.searchInput.toLowerCase();

      const filteredData = this.solicitudes.filter((solicitud) => {
        // Convertimos todos los campos a cadena y a minúsculas para comparación
        const personaID = String(solicitud.Persona_ID || "").toLowerCase();
        const solicitudID = String(solicitud.Solicitud || "").toLowerCase();
        const comentario = String(solicitud.Comentario || "").toLowerCase();
        const estatus = String(solicitud.Estatus || "").toLowerCase();
        const tipo = String(solicitud.Tipo || "").toLowerCase();
        const fecha = String(solicitud.Fecha || "").toLowerCase();

        // Comprobamos si el query de búsqueda coincide con alguno de los campos
        return (
          personaID.includes(searchQuery) ||
          solicitudID.includes(searchQuery) ||
          comentario.includes(searchQuery) ||
          estatus.includes(searchQuery) ||
          tipo.includes(searchQuery) ||
          fecha.includes(searchQuery)
        );
      });

      this.totalPages = Math.ceil(filteredData.length / this.resultsPerPage);

      this.paginatedData = filteredData.slice(
        (this.currentPage - 1) * this.resultsPerPage,
        this.currentPage * this.resultsPerPage
      );
    },
    // Cambia a la página anterior
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },

    goToPage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
        console.log(`Ir a la página: ${this.currentPage}`);
        this.updatePagination();
      }
    },

    formatearFecha(fecha) {
      if (moment(fecha, moment.ISO_8601, true).isValid()) {
        return moment(fecha).format("DD/MM/YYYY HH:mm:ss");
      } else {
        return "Sin Fecha";
      }
    },
  },

  watch: {
    // Observa los cambios en el input de búsqueda
    searchInput() {
      this.updatePagination();
    },
  },

  computed: {
    // esta en adaptacion a la plantilla

    paginatedItems() {
      // Lógica para obtener los elementos paginados
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.items.slice(start, end);
    },

    paginatedData() {
      const startIndex = (this.currentPage - 1) * this.resultsPerPage;
      const endIndex = startIndex + this.resultsPerPage;
      return this.filteredData
        .slice(startIndex, endIndex)
        .map((item, index) => {
          return {
            ...item,
            index: startIndex + index + 1, // Ajusta el índice para mantener la secuencia numérica continua
          };
        });
    },

    totalPages() {
      return Math.ceil(this.solicitudes.length / this.resultsPerPage);
    },

    filteredData() {
      // Modifica la función para filtrar según el término de búsqueda
      console.log("Search input:", this.searchInput);
      return this.solicitudes.filter((solicitud) => {
        const matchSearchInput = Object.values(solicitud).some((value) => {
          return String(value)
            .toLowerCase()
            .includes(this.searchInput.toLowerCase());
        });

        // Obtener el texto correspondiente al servicio_paciente_id
        let servicioText = "";
        switch (solicitud.Personal_Medico_ID) {
          case 1:
            servicioText = "Urgencias";
            break;

          default:
            servicioText = String(solicitud.Nombre, solicitud.Descripcion); // Si no coincide con ninguno, mantener el valor original
        }

        const matchServicioId = servicioText
          .toLowerCase()
          .includes(this.searchInput.toLowerCase());

        let departamentoText = "";
        switch (solicitud.Solicitud_id) {
          case 1:
            departamentoText = "Dirección General";
            break;

          default:
            departamentoText = String(solicitud.Solicitud_id);
        }

        const matchDepartamentoId = departamentoText
          .toLowerCase()
          .includes(this.searchInput.toLowerCase());

        return matchSearchInput || matchServicioId || matchDepartamentoId;
      });
    },
  },
};
</script>

<style scoped>
/* Si estás usando Tailwind CSS, puedes definir estilos personalizados aquí */
.checked\:bg-blue-500:checked {
  background-color: #3b82f6;
  /* Azul en Tailwind CSS */
}

.checked\:border-blue-500:checked {
  border-color: #3b82f6;
  /* Azul en Tailwind CSS */
}
</style>
