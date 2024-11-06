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
        currencies: {
            type: Object,
            required: true
        },
        modelValue: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            selectedCurrency: this.modelValue
        };
    },
    methods: {
        updateCurrency() {
            this.$emit('update:modelValue', this.selectedCurrency);
        }
    },
}
</script>

<!-- Il model value passa firstCurr e secondCurr dal genitore in modo tale da passargli eur e usd come default che associo a selectedCurrency -->
<!-- Allo stesso tempo selectedCurrency, è anche la variabile su cui aggiorno il v-model del componente stesso -->
<!-- Al cambio quindi quando scelgo un altra opzione, emitto l'update del modelValue passandogli la selectedCurrency aggiornata al genitore -->
<!-- Nel genitore il v-model come detto è associato a firstCurr e secondCurr quindi aggiornerà le due variabili di conseguenza -->