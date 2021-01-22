<template>
  <div class="row">
    <div class="col-md-2">
      <div class="card mt-2 p-2">
        <h6 class="text-center">Warp Factor</h6>
        <p class="text-center">(in Mio.)</p>
        <JqxSlider ref="warpSlider" @change="setOLF()"
          :template="'danger'"
          :height="460" :width="100" :min="0" :max="5"
          :value="0" :step="0.2" :mode="'fixed'" :orientation="'vertical'"
          :showTickLabels="true" :ticksFrequency="1" :ticksPosition="'top'">
        </JqxSlider>
      </div>
    </div>
    <div class="col-md-10">
      <div class="card mt-2 p-2">
        OL Factor:
        <JqxInput  ref="warpInput1"
          :width="40" :height="30" :value="'test'" :disabled="true">
        </JqxInput>
        OL Speed:
        <JqxInput  ref="warpInput"
          :width="200" :height="30" :value="'test'" :disabled="true">
        </JqxInput>
        Light years/ second:
        <JqxInput  ref="lyPerSec"
          :width="80" :height="30" :value="'test'" :disabled="true">
        </JqxInput>
      </div> 
    </div>
  </div>
</template>

<script>
  //import JqxGrid from "jqwidgets-scripts/jqwidgets-vue/vue_jqxgrid.vue";
  import JqxSlider from "jqwidgets-scripts/jqwidgets-vue/vue_jqxslider.vue";
  import JqxInput from "jqwidgets-scripts/jqwidgets-vue/vue_jqxinput.vue";

  export default {
    components: {
      JqxSlider,
      JqxInput
    },

    data: function () {
      return { }
    },

    mounted: function () {
      this.setOLF();
    },
    methods: {
      setOLF: function () {
        const c = 300000; // Lightspeed in km/s
        const ly = 9.4607e12; // Light year in km

        let olf = Math.round(this.$refs.warpSlider.value * 10)/10;
        let olspeed = olf * c * 1e6;
        let TimeToAlphaCentauri = (4.3*ly) / olspeed;
        let lyPerSecond = olspeed / ly;

        // Outputs, Signalisation
        this.$refs.warpInput1.value = olf;
        this.$refs.warpInput.value = olspeed;
        this.$refs.lyPerSec.value = Math.round(lyPerSecond * 10000) / 10000;
        
      },
    }
  }
</script>

<style src='./assets/styles/jqwidgets/jqx.base.css'></style>
<style src='./assets/styles/jqwidgets/jqx.material-green.css'></style>