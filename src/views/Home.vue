<template>
  <div class="home">
    <Buscador msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Buscador from '@/components/Buscador.vue'

export default {
  name: 'Home',
  components: {
    Buscador
  }
}
</script>
