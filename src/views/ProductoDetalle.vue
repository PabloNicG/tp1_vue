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
    async getInstrumentos() {
      const res = await fetch("/instrumentos.json");
      //Llamo a instrumentos.json de public y se lo asigno a res
      const resJson = await res.json();
      //transformo a res en json y lo asigno a resjson
      console.log(resJson);
      //muestro
      this.instrumentosData = resJson.instrumentos;
      //El resJson.instrumentos que los traigo desde el public y lo asigno a instrumentosData
      //este se convierte en mi coleccion de elementos y se almacenan
    }
  } //
};
</script>