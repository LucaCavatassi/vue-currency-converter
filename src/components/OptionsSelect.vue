<script>
    export default {
        props: {
            currencies: {
                type: Array,
                required: true
            }
        },
        
        methods: {
            getCurrencyName(code) {
                return currencyNames[code] || code; // Fallback to code if name not found
            }
        }
    }
</script>

<template>
    <option v-for="currency in currencies" :key="currency" :value="currency">
        {{ currency }}
    </option>
</template>

<style>
</style>