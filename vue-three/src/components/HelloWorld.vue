<template>
  <div>
    <aside class="control-panel">
      <h3>Position</h3>
      <label>x<input type="range" v-model="x"></label>
      <label>y<input type="range" v-model="y"></label>
      <label>z<input type="range" v-model="z"></label>
    </aside>
    <vgl-renderer antialias style="height: 100vh;">
      <vgl-scene>
        <vgl-sphere-geometry name="sphere" radius=25></vgl-sphere-geometry>
        <vgl-mesh-standard-material name="std"></vgl-mesh-standard-material>
        <vgl-mesh geometry="sphere" material="std" :position="`${x} ${y} ${z}`"></vgl-mesh>
        <vgl-axes-helper size=140></vgl-axes-helper>
        <vgl-ambient-light color="#ffeecc"></vgl-ambient-light>
        <vgl-directional-light position="0 1 1"></vgl-directional-light>
      </vgl-scene>
      <vgl-perspective-camera orbit-position="200 1 0.5"></vgl-perspective-camera>
    </vgl-renderer>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.control-panel {
    background: #fff;
    font-family: 'Architects Daughter', 'Helvetica Neue', Helvetica, Arial, serif;
    left: 1ex;
    margin: 0;
    max-height: calc(100vh - 4ex);
    opacity: 0.85;
    overflow: auto;
    padding: 1ex;
    position: fixed;
    top: 1ex;
}
</style>
