<script>
    import axios from 'axios';
    import OptionsSelect from '../components/OptionsSelect.vue'

    export default {
        data() {
            return {
                currencies: [],
                firstCurr: 'EUR',  // Default value for the first select
                secondCurr: 'USD'  // Default value for the second select
            }
        },

        components: {
            OptionsSelect,
        },

        methods: {
            fetchCurrency() {
                axios.get('https://api.frankfurter.app/latest').then(resp => {
                    let currenciesData = resp.data.rates;
                    // console.log(currenciesData);

                    // Creat an array of currency codes
                    this.currencies = ["EUR", ...Object.keys(currenciesData)];
                })
            }
        },

        mounted() {
            this.fetchCurrency()
            console.log(this.currencies);
        }
    }
</script>

<template>
    <h1>Currency Convert</h1>
    <div class="row">
        <div class="col-6">
            <select v-model="firstCurr" name="firstCurr" id="firstCurr">
                <OptionsSelect :currencies="currencies"></OptionsSelect>
            </select>
        </div>

        <div class="col-6">
            <select v-model="secondCurr" name="secondCurr" id="secondCurr">
                <OptionsSelect :currencies="currencies"></OptionsSelect>
            </select>
        </div>
    </div>
</template>

<style>
</style>