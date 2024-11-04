<template>
    <select v-model="selectedCurrency" @change="updateCurrency">
        <option v-for="(fullName, code) in currencies" :key="code" :value="code">
            {{ code }} - {{ fullName }} 
        </option>
    </select>
</template>

<script>
export default {
    props: {
        // Props from Main of all currencies
        currencies: {
            type: Object,
            required: true
        },
        // Props from Main of v-model
        modelValue: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            // The selectedCurrency it's the v-model value (the value it's the code)
            selectedCurrency: this.modelValue // Initialize with the v-model value
        };
    },

    methods: {
        // Selecting a new value, emits the selected currency to parent v-model 
        // -> the v-model updates the firstCurr or secondCurr variable that again will be passed to the component
        updateCurrency() {
            this.$emit('update:modelValue', this.selectedCurrency);
        }
    },

    watch: {
        // Watch for changes in the DOM when the props it's changed, the v-model syncs to the new value
        modelValue(newValue) {
            this.selectedCurrency = newValue;
        }
    },
}
</script>

<style>
select {
    width: 150px; /* Set desired width */
    white-space: nowrap; /* Prevent wrapping */
    overflow: hidden; /* Hide overflow */
    text-overflow: ellipsis; /* Display ellipsis (...) for overflowed text */
}
</style>