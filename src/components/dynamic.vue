<template>
  <div class="dynamic">
      <router-view></router-view>
  </div>
</template>

<script>
import rightBar from './rightBar'
export default {
  name: 'dynamic',
    components: {
        rightBar
    },
  data () {
    return {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
