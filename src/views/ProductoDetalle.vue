<template>
  <div class="productoDetalle">
    <b-container>
      <b-card-group deck>
        <div v-for="instrumento in instrumentosData" :key="instrumento.id" style="margin-top:15px">
          <instrumento-item :instrumentoParam="instrumento"></instrumento-item>
        </div>
      </b-card-group>
    </b-container>
  </div>
  <!--  Puedo recorrer la coleccion con un vfor, la key me identifica los nodos del arbol
      (los dos puntos son v-bind) 
      instrumento-item es lo usamos con istrumentoParam de Instrumento.vue
      instrumentoParam declarado en Instrumento.vue

      En instrumento-item contengo instrumento-param y le paso el instrumento con todos sus datos
  -->
</template> 



<script>
import axios from "axios";
import Instrumento from "@/components/Instrumento.vue";

export default {
  name: "ProductoDetalle",
  components: {
    "instrumento-item": Instrumento
    //declaro componentes
  },

  mounted() {
    this.getInstrumentos();
  }, //Constructor de clase -

  data() {
    return {
      instrumentosData: []
      //objeto de datos
    };
  },

  methods: {
    getInstrumentos() {
      axios
        .get("http://localhost:9001/api/v1/instrumentosbd/all")
        .then(res => {
          this.instrumentosData = res.data;
        })
        .catch(error => {
          console.log(error);
        });
      //
    }
  } //
};
</script>