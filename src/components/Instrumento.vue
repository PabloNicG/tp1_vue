<template>
  <div class="mt-3">
    <b-container>
      <b-row>
        <b-card-group >
          <!-- Estilo de tarjeta e Imagen -->
          <b-card
            border-variant="info"
            tag="article"
            style="width: 20rem;"
            class="mb-1"
            bg-variant="li"
          >
            <b-card-img
              :src="'/images/' + instrumentoParam.imagen"
              alt="Image"
              style="height:250px; max-height:300px"
            ></b-card-img>
            <!-- Titulo -->
            <hr />
            <b>
              <b-card-title class="text-center" :title="instrumentoParam.instrumento"></b-card-title>
            </b>
            <hr />
            <!-- Marca -->
            <b-card-sub-title class="mb-2 text-center">{{instrumentoParam.marca}}</b-card-sub-title>
            <hr />
            <!-- Precio y cantidad Vendida-->
            <b-card-text>
              <h5>
                <b-badge variant="info">Precio: ${{instrumentoParam.precio}}</b-badge>
              </h5>
              <b-card-sub-title style="font-size:90%;" class="text-left">
                <b>
                  Vendidos:
                  {{instrumentoParam.cantidadVendida}}
                </b>
              </b-card-sub-title>
            </b-card-text>
            <!-- Costo de envio con V-If -->
            <b-card-sub-title>
              <div style="color: #25ac25" v-if="this.instrumentoParam.costoEnvio === 'G'">
                <img alt="logo" :src="'/images/camion.png'" />
                <b>Costo del Envío: {{instrumentoParam.costoEnvio}}</b>
              </div>

              <div
                v-else-if="this.instrumentoParam.costoEnvio !== 'G'"
              ><b>Costo del Envío: $ {{instrumentoParam.costoEnvio}}</b></div>
            </b-card-sub-title>
            <br>
            <!-- Detalle del instrumento navegando por ID -->
            <div style="text-aling:center">
              <b-button
                :href="'/detalleInstrumento/' + instrumentoParam.id"
                variant="info"
                style="width:100%"
                size="sm"
              >
              <!--  -->
                <b>Detalle</b>
              </b-button>
            </div>
          </b-card>
        </b-card-group>
      </b-row>
      <br />
    </b-container>
  </div>
</template>

<script>
export default {
  props: ["instrumentoParam"]
  //Propiedades de instrumento

  //Desde acá leo las propiedades
};
</script>

<style>
</style>

