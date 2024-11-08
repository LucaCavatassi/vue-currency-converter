<script>
  import ChartsComponent from "./components/ChartsComponent.vue";
  import ConverterContainer from "./components/ConverterContainer.vue";

  export default {
    components: {
      ConverterContainer,
      ChartsComponent
    }
  }
</script>

<template>

  <div class="ms-cont text-white container pt-4">
    <ConverterContainer></ConverterContainer>
    <ChartsComponent></ChartsComponent>
  </div>

  <!-- HOW TO USE FAW -->
  <!-- <font-awesome-icon icon="coffee" /> -->
</template>

<style scoped lang="scss">

</style>
