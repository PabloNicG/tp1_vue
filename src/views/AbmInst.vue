<template>
  <div class="container mt-5">
    <div class="row mb-3" >
      <div class="col">
        <h1>Instrumentos</h1>
      </div>
      <div class="col">
        <!-- boton que abre la ventana modal para añadir un instrumento -->
        <button
          class="btn float-right btn-info"
          v-b-modal.modal
          @click="setTituloAdd"
        >
          + Agregar
        </button>
      </div>
    </div>
    <!-- Tabla que muestra el listado de datos -->
    <table class="table">
      <thead>
        <tr>
          <th>Id</th>
          <th>Instrumento</th>
          <th>Descripcion</th>
          <th>Modelo</th>
          <th>Marca</th>
          <th>Precio</th>
          <th>Costo Envío</th>
          <th>Cant. Vendida</th>
          <th>Imagen</th>
          <th>Acciones</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="instrumento in instrumentosData" :key="instrumento.id">
          <th>{{ instrumento.id }}</th>
          <td>{{ instrumento.instrumento }}</td>
          <td>{{ instrumento.descripcion | cortarDescripcion }}</td>
          <td>{{ instrumento.modelo }}</td>
          <td>{{ instrumento.marca }}</td>
          <td>{{ instrumento.precio }}</td>
          <td>{{ instrumento.costoEnvio }}</td>
          <td>{{ instrumento.cantidadVendida }}</td>
          <td>{{ instrumento.imagen }}</td>
          <td>
            <!--  ventana modal para editar un instrumento -->
            <button
              class="btn btn-block btn-info  "
              v-b-modal.modal
              @click="setEditar(instrumento)"
            >
              Editar
            </button>
            <!-- Boton para eliminar un instrumento -->
            <button
              class="btn btn-block btn-info"
              @click="deleteInstrumento(instrumento)"
            >
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Ventana modal -->
    <b-modal
      id="modal"
      ref="modal-ref"
      size="lg"
      :title="tituloModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <!-- Formulario -->
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
          id="nobreInstrumento"
          label="Nombre:"
          label-for="instrumento"
        >
          <b-form-input
            id="instrumento"
            type="text"
            v-model="$v.instrumentoActual.instrumento.$model"
            :state="validateState('instrumento')"
            placeholder="Nombre del instrumento"
            required
          ></b-form-input>
          <b-form-invalid-feedback id="input-1-live-feedback">
            ¡Este campo es requerido!
          </b-form-invalid-feedback>
        </b-form-group>
        <b-row>
          <b-col>
            <b-form-group
              id="marcaInstrumento"
              label="Marca:"
              label-for="marca"
            >
              <b-form-input
                id="marca"
                type="text"
                v-model="$v.instrumentoActual.marca.$model"
                :state="validateState('marca')"
                placeholder="Marca del instrumento"
                required
              ></b-form-input>
              <b-form-invalid-feedback id="input-1-live-feedback">
                ¡Este campo es requerido!
              </b-form-invalid-feedback>
            </b-form-group>
          </b-col>
          <b-col>
            <b-form-group
              id="modeloInstrumento"
              label="Modelo"
              label-for="modelo"
            >
              <b-form-input
                id="modelo"
                type="text"
                v-model="$v.instrumentoActual.modelo.$model"
                :state="validateState('modelo')"
                placeholder="Modelo del instrumento..."
                required
              ></b-form-input>
              <b-form-invalid-feedback id="input-1-live-feedback">
                ¡Este campo es requerido!
              </b-form-invalid-feedback>
            </b-form-group>
          </b-col>
        </b-row>

        <b-form-group
          id="descripcionInstrumento"
          label="Descripcion"
          label-for="descripcion"
        >
          <b-form-textarea
            id="descripcion"
            v-model="$v.instrumentoActual.descripcion.$model"
            :state="validateState('descripcion')"
            placeholder="descripcion del instrumento"
            required
          ></b-form-textarea>
          <b-form-invalid-feedback id="input-1-live-feedback">
            ¡Este campo es requerido!
          </b-form-invalid-feedback>
        </b-form-group>

        <b-row>
          <b-col>
            <b-form-group
              id="precioInstrumento"
              label="Precio"
              label-for="precio"
            >
              <b-form-input
                id="precio"
                type="number"
                v-model="$v.instrumentoActual.precio.$model"
                :state="validateState('precio')"
                placeholder="$"
                required
              ></b-form-input>
              <b-form-invalid-feedback id="input-1-live-feedback">
                ¡Este campo es requerido!
              </b-form-invalid-feedback>
            </b-form-group>
          </b-col>
          <b-col>
            <b-form-group
              id="envioInstrumento"
              label="Costo de envío"
              label-for="costoEnvio"
            >
              <b-form-input
                id="costoEnvio"
                type="text"
                v-model="$v.instrumentoActual.costoEnvio.$model"
                :state="validateState('costoEnvio')"
                placeholder="Envio gratis o Envio Pago"
                required
              ></b-form-input>
              <b-form-invalid-feedback id="input-1-live-feedback">
                ¡Este campo es requerido!
              </b-form-invalid-feedback>
            </b-form-group>
          </b-col>
          <b-col>
            <b-form-group
              id="vendidosInstrumento"
              label="Cant. vendida"
              label-for="cantidadVendida"
            >
              <b-form-input
                id="cantidadVendida"
                type="number"
                v-model="$v.instrumentoActual.cantidadVendida.$model"
                :state="validateState('cantidadVendida')"
                placeholder="Cantidad vendida"
                required
              ></b-form-input>
              <b-form-invalid-feedback id="input-1-live-feedback">
                ¡Este campo es requerido!
              </b-form-invalid-feedback>
            </b-form-group>
          </b-col>
        </b-row>

        <b-form-group
          id="imagenInstrumento"
          label="Imagen del instrumento"
          label-for="imagen"
        >
          <b-form-input
            id="imagen"
            type="text"
            v-model="$v.instrumentoActual.imagen.$model"
            :state="validateState('imagen')"
            placeholder="Imagen"
            title="Ingrese la descripcion del instrumento..."
            disabled
          ></b-form-input>
          <b-form-invalid-feedback id="input-1-live-feedback">
            ¡Este campo es requerido!
          </b-form-invalid-feedback>
        </b-form-group>
        <b-form-group>
          <div id="image">
            <input type="file" @change="onImageUpload" />
          </div>
        </b-form-group>
      </form>
      <!-- fin formulario -->
    </b-modal>
    <!-- fin ventana modal -->
  </div>
</template>

<script>
import axios from "axios";
import { validationMixin } from "vuelidate";
import { required } from "vuelidate/lib/validators";

export default {
  name: "ABM",
  mixins: [validationMixin],
  mounted() {
    this.getInstrumentos();
  },
  data() {
    return {
      tituloModal: null,
      instrumentosData: [],
      instrumentoActual: {
        id: 0,
        instrumento: null,
        marca: null,
        modelo: null,
        imagen: null,
        precio: null,
        costoEnvio: null,
        cantidadVendida: null,
        descripcion: null,
      },
    };
  },
  validations: {
    instrumentoActual: {
      instrumento: {
        required,
      },
      marca: {
        required,
      },
      modelo: {
        required,
      },
      imagen: {
        required,
      },
      precio: {
        required,
      },
      costoEnvio: {
        required,
      },
      cantidadVendida: {
        required,
      },
      descripcion: {
        required,
      },
    },
  },
  filters: {
    cortarDescripcion: function(value) {
      if (!value) return "";
      value = value.toString();
      return value.slice(0, 100) + "...";
    },
  },
  methods: {
    validateState(campo) {
      const { $dirty, $error } = this.$v.instrumentoActual[campo];
      return $dirty ? !$error : null;
    },
    /* Método que trae del servidor la lista completa de instrumentos */
    getInstrumentos() {
      axios
        .get("http://localhost:9001/api/v1/instrumentosbd/all")
        .then((res) => {
          this.instrumentosData = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    /* Método PARA cerrar la ventana modal */
    hideModal() {
      this.$refs["modal-ref"].hide();
    },
    /* Método resetear EL modal  */
    resetModal() {
      this.instrumentoActual = {
        id: 0,
        instrumento: null,
        marca: null,
        modelo: null,
        imagen: null,
        precio: null,
        costoEnvio: null,
        cantidadVendida: null,
        descripcion: null,
      };
    },
    /*  Editar: asigno el instrumento de la fila al instrumentoActual */
    setEditar(instrumento) {
      this.tituloModal = "Editar";
      this.instrumentoActual = instrumento;
    },
    /* Asigno el título Añadir a la ventana modal cuando hago click en el botón "Añadir" */
    setTituloAdd() {
      this.tituloModal = "Añadir existencia";
    },
    /* Controlo el evento click sobre el botón -ok- del footer del modal */
    handleOk(bvModalEvt) {
      bvModalEvt.preventDefault();
      this.handleSubmit();
    },
    /* Método para el submit del formulario */
    handleSubmit() {
      if (this.instrumentoActual.id !== 0) {
        this.updateInstrumento(this.instrumentoActual);
      } else {
        this.addInstrumento(this.instrumentoActual);
      }
    },
    /* Comunico al servidor para AGREGAR un instrumento */
    addInstrumento(instrumento) {
      axios
        .post("http://localhost:9001/api/v1/instrumentosbd/", instrumento)
        .then((response) => {
          console.log(response.data);
          this.instrumentosData.push(response.data);
          this.hideModal();
          alert("Instrumento agregado con éxito!");
        })
        .catch((e) => {
          console.log(e);
          alert("Ha ocurrido un error");
        });
    },
    /* Comunico al servidor para para ACTUALIZAR un instrumento */
    updateInstrumento(instrumento) {
      axios
        .put(
          "http://localhost:9001/api/v1/instrumentosbd/" + instrumento.id,
          instrumento
        )
        .then((response) => {
          console.log(response.data);
          this.hideModal();
          alert("Instrumento actualizado exitosamente!");
        })
        .catch((e) => {
          console.log(e);
          alert("Ha ocurrido un error");
        });
    },
    /* Comunico al servidor para para ELIMINAR un instrumento */
    deleteInstrumento(instrumento) {
      const confirmar = confirm("¿Esta seguro de eliminar este instrumento?");
      if (confirmar) {
        axios
          .delete("http://localhost:9001/api/v1/instrumentosbd/" + instrumento.id)
          .then((response) => {
            console.log(response.data);
            const index = this.instrumentosData.indexOf(instrumento);
            this.instrumentosData.splice(index, 1);
          })
          .catch((e) => {
            console.log(e);
          });
      }
    },
    /* Comunico con el servidor para agregar una imagen */
    onImageUpload(event) {
      const data = new FormData();
      data.append("file", event.target.files[0]);
      this.instrumentoActual.imagen = event.target.files[0].name;
      // Llamo al servicio y realizo el upload de la imagen
      axios
        .post("http://localhost:9001/api/v1/instrumentosbd/images", data)
        .then((response) => {
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
          alert("Error al cargar la imagen");
        });
    },
  },
};
</script>
