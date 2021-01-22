<template>
  <div class="row">
    <div class="col-md-2">
      <div class="card mt-2 p-2">
        <h6 class="text-center">Warp Factor</h6>
        <p class="text-center">(in Mio.)</p>
        <JqxSlider ref="warpSlider" @change="setOLF()"
          :template="'danger'"
          :height="700" :width="100" :min="0" :max="5"
          :value="0" :step="0.1" :mode="'fixed'" :orientation="'vertical'"
          :showTickLabels="true" :ticksFrequency="1" :ticksPosition="'top'">
        </JqxSlider>
      </div>
    </div>
    <div class="col-md-10">
      <div class="card mt-2 p-2 bg-light">
        OL Factor:
        <JqxInput  ref="warpInput1"
          :width="40" :height="30" :value="'test'" :disabled="true">
        </JqxInput>
        OL Speed:
        <JqxInput  ref="warpInput"
          :width="200" :height="30" :value="'test'" :disabled="true">
        </JqxInput>
        
        <div class="row mt-1">
          <div class="d-flex justify-content-start">
            <p>Light years/second:&nbsp;&nbsp;</p>
            <p>
              <JqxInput  ref="lyPerSec"
                :width="80" :height="30" :value="'test'" :disabled="true">
              </JqxInput>
            </p>
          </div>
        </div>

        <div class="row mt-1">
          <div class="d-flex justify-content-start">
            <p>Time to Alpha Centauri:&nbsp;&nbsp;</p>
            <p>
              <JqxInput  ref="TimeToAlphaCentauri"
                :width="80" :height="30" :value="'test'" :disabled="true">
              </JqxInput>
            </p>
            <p>&nbsp;minutes.</p>
          </div>
        </div>
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
        this.$refs.TimeToAlphaCentauri.value = ((4.3*ly) / olspeed)/60;
        
      },
    }
  }
</script>

<style src='./assets/styles/jqwidgets/jqx.base.css'></style>
<style src='./assets/styles/jqwidgets/jqx.material-green.css'></style>