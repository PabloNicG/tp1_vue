<template>
  <b-container>
    <div class="row" style="margin-top:100px">
      <b-row no-gutters>
        <b-col md="6" >
          <b-card-img 
            :src="'/images/' +instrumentoParam.imagen"
            alt="Image"
            class="rounded float-center"
            style="width: 435px; height: 450px; "
            
          ></b-card-img>
        </b-col>

        <b-col md="6">
          <b-list-group>
            <b-card-body>
              <!-- Titulo Instrumento-->
              <b-list-group-item show variant="info"> 
                <b-card-title class="text-left" :title="instrumentoParam.instrumento"></b-card-title>
              </b-list-group-item>
              <!-- Marca -->
              <b-list-group-item>
                <b-card-sub-title cclass="text-left">
                  <b>Marca:</b>
                  {{instrumentoParam.marca}}
                </b-card-sub-title>
              </b-list-group-item>
              <!-- Modelo -->
              <b-list-group-item>
                <b-card-sub-title cclass="text-left">
                  <b>Modelo:</b>
                  {{instrumentoParam.modelo}}
                </b-card-sub-title>
              </b-list-group-item>
              <!-- Descripcion -->
              <b-list-group-item>
                <b-card-text>{{instrumentoParam.descripcion}}</b-card-text>
              </b-list-group-item>
              <!-- Precio producto -->
              <b-list-group-item>
                <b-card-sub-title class="text-left">
                  <b>Precio: $</b>
                  {{instrumentoParam.precio}}
                </b-card-sub-title>
                <br>
                <!-- Vendidos -->
                <b-card-sub-title style="font-size:95%;" class="text-left">
                 <b> Vendidos: 
                  {{instrumentoParam.cantidadVendida}}</b>
                </b-card-sub-title>
              </b-list-group-item>
              <!-- Costo de envio -->
              <b-list-group-item>
                <b-card-sub-title>
                  <b-card-sub-title class="text-left">
                    
                  </b-card-sub-title>
                  <div style="color: #25ac25" v-if="this.instrumentoParam.costoEnvio === 'G'">
                    <img alt="logo" :src="'/images/camion.png'" />
                    <b>Envío Gratis</b>
                  </div>

                  <div
                    v-else-if="this.instrumentoParam.costoEnvio !== 'G'"
                  ><b>Costo del Envío: $</b>{{instrumentoParam.costoEnvio}}</div>
                </b-card-sub-title>
              </b-list-group-item>
              <!-- Botones -->

              <b-list-group-item>
                <b-button block variant="outline-info">Agregar al Carrito</b-button>

                <b-button block variant="outline-info" href="/productoDetalle">Volver</b-button>
              </b-list-group-item>
            </b-card-body>
          </b-list-group>
        </b-col>
      </b-row>
    </div>
  </b-container>
</template>


<script>
export default {
  name: "DetalleProducto",
  components: {},
 
  mounted() {
    this.getInstrumentosxId();
  },

  data() {
    return {
      instrumentoParam: []
    };
  },

  methods: {
    async getInstrumentosxId() {
      const parametroId = this.$route.params.id;
      //Recupero el parametro - a travez de la ruta, los parametros y el id
      const res = await fetch("/instrumentos.json");
      //fetch me trae todos los elementos
      const resJson = await res.json();
      //lo convierto en json

      this.instrumentoParam = await resJson.instrumentos.find(
        instrumento => instrumento.id === parametroId
      ); //Uso find me retorna un objeto (evito [0]) 
      //
    }
  }
};
</script>

<style lang=""></style>
