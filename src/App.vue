<script>
import Charts from "./components/Charts.vue";
import ConverterContainer from "./components/ConverterContainer.vue";

export default {
  components: {
    ConverterContainer,
    Charts
  },

  data() {
    return {
      firstCurr: 'EUR', // Initialize with default values
      secondCurr: 'USD',
    };
  },
  emits: ['update-first-curr', 'update-second-curr'],
  methods: {
    handleFirstCurrUpdate(newFirstCurr) {
      this.firstCurr = newFirstCurr;  // Update firstCurr in parent
    },
    handleSecondCurrUpdate(newSecondCurr) {
      this.secondCurr = newSecondCurr;  // Update secondCurr in parent
    },
  },
};

</script>

<template>

  <div class="ms-cont text-white container pt-4">
    <ConverterContainer @update-first-curr="handleFirstCurrUpdate" @update-second-curr="handleSecondCurrUpdate"></ConverterContainer>
    <Charts :first-curr="firstCurr" :second-curr="secondCurr"></Charts>
  </div>

  <!-- HOW TO USE FAW -->
  <!-- <font-awesome-icon icon="coffee" /> -->
</template>

<style scoped lang="scss"></style>
