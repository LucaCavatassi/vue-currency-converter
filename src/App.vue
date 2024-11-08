<script>
  import Charts from "./components/Charts.vue";
import ConverterContainer from "./components/ConverterContainer.vue";

  export default {
    components: {
      ConverterContainer,
      Charts
    }
  }
  
</script>

<template>

  <div class="ms-cont text-white container pt-4">
    <ConverterContainer></ConverterContainer>
    <Charts></Charts>
  </div>

  <!-- HOW TO USE FAW -->
  <!-- <font-awesome-icon icon="coffee" /> -->
</template>

<style scoped lang="scss">

</style>
