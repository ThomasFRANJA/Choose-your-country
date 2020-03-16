<template lang="pug">
  section.countries
    <Autocomplete />


</template>

<script>
import Autocomplete from './components/Autocomplete';
export default {
  name: 'App',

  components: {
    Autocomplete,
  },
};
</script>

<style lang="scss">
.countries {
  background:  #f2f5f7;
  height: 100vh;
  display: flex;
  justify-content: center;
}
  
</style>


