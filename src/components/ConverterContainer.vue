<script>
import axios from 'axios';
import OptionsSelect from '../components/OptionsSelect.vue'

export default {
    data() {
        return {
            // All currencies
            currencies: {
                "AED": "United Arab Emirates Dirham",
                "AFN": "Afghan Afghani",
                "ALL": "Albanian Lek",
                "AMD": "Armenian Dram",
                "ANG": "Netherlands Antillean Guilder",
                "AOA": "Angolan Kwanza",
                "ARS": "Argentine Peso",
                "AUD": "Australian Dollar",
                "AWG": "Aruban Florin",
                "AZN": "Azerbaijani Manat",
                "BAM": "Bosnia and Herzegovina Convertible Mark",
                "BBD": "Barbadian Dollar",
                "BDT": "Bangladeshi Taka",
                "BGN": "Bulgarian Lev",
                "BHD": "Bahraini Dinar",
                "BIF": "Burundian Franc",
                "BMD": "Bermudian Dollar",
                "BND": "Brunei Dollar",
                "BOB": "Bolivian Boliviano",
                "BRL": "Brazilian Real",
                "BSD": "Bahamian Dollar",
                "BTN": "Bhutanese Ngultrum",
                "BWP": "Botswana Pula",
                "BYN": "Belarusian Ruble",
                "BZD": "Belize Dollar",
                "CAD": "Canadian Dollar",
                "CHF": "Swiss Franc",
                "CLP": "Chilean Peso",
                "CNY": "Chinese Yuan",
                "COP": "Colombian Peso",
                "CRC": "Costa Rican Colón",
                "CUP": "Cuban Peso",
                "CVE": "Cape Verdean Escudo",
                "CZK": "Czech Koruna",
                "DJF": "Djiboutian Franc",
                "DKK": "Danish Krone",
                "DOP": "Dominican Peso",
                "DZD": "Algerian Dinar",
                "EGP": "Egyptian Pound",
                "ERN": "Eritrean Nakfa",
                "ETB": "Ethiopian Birr",
                "EUR": "Euro",
                "FJD": "Fijian Dollar",
                "FKP": "Falkland Islands Pound",
                "GBP": "British Pound",
                "GEL": "Georgian Lari",
                "GGP": "Guernsey Pound",
                "GHS": "Ghanaian Cedi",
                "GIP": "Gibraltar Pound",
                "GMD": "Gambian Dalasi",
                "GNF": "Guinean Franc",
                "GTQ": "Guatemalan Quetzal",
                "GYD": "Guyanese Dollar",
                "HKD": "Hong Kong Dollar",
                "HNL": "Honduran Lempira",
                "HRK": "Croatian Kuna",
                "HTG": "Haitian Gourde",
                "HUF": "Hungarian Forint",
                "IDR": "Indonesian Rupiah",
                "ILS": "Israeli New Shekel",
                "INR": "Indian Rupee",
                "IQD": "Iraqi Dinar",
                "IRR": "Iranian Rial",
                "ISK": "Icelandic Króna",
                "JMD": "Jamaican Dollar",
                "JOD": "Jordanian Dinar",
                "JPY": "Japanese Yen",
                "KES": "Kenyan Shilling",
                "KGS": "Kyrgyzstani Som",
                "KHR": "Cambodian Riel",
                "KPW": "North Korean Won",
                "KRW": "South Korean Won",
                "KWD": "Kuwaiti Dinar",
                "KYD": "Cayman Islands Dollar",
                "KZT": "Kazakhstani Tenge",
                "LAK": "Laotian Kip",
                "LBP": "Lebanese Pound",
                "LKR": "Sri Lankan Rupee",
                "LRD": "Liberian Dollar",
                "LSL": "Lesotho Loti",
                "LYD": "Libyan Dinar",
                "MAD": "Moroccan Dirham",
                "MDL": "Moldovan Leu",
                "MGA": "Malagasy Ariary",
                "MKD": "Macedonian Denar",
                "MMK": "Myanma Kyat",
                "MNT": "Mongolian Tögrög",
                "MOP": "Macanese Pataca",
                "MRU": "Mauritanian Ouguiya",
                "MUR": "Mauritian Rupee",
                "MVR": "Maldivian Rufiyaa",
                "MWK": "Malawian Kwacha",
                "MXN": "Mexican Peso",
                "MYR": "Malaysian Ringgit",
                "MZN": "Mozambican Metical",
                "NAD": "Namibian Dollar",
                "NGN": "Nigerian Naira",
                "NOK": "Norwegian Krone",
                "NPR": "Nepalese Rupee",
                "NZD": "New Zealand Dollar",
                "OMR": "Omani Rial",
                "PAB": "Panamanian Balboa",
                "PEN": "Peruvian Sol",
                "PGK": "Papua New Guinean Kina",
                "PHP": "Philippine Peso",
                "PKR": "Pakistani Rupee",
                "PLN": "Polish Zloty",
                "PYG": "Paraguayan Guarani",
                "QAR": "Qatari Rial",
                "RON": "Romanian Leu",
                "RSD": "Serbian Dinar",
                "RUB": "Russian Ruble",
                "RWF": "Rwandan Franc",
                "SAR": "Saudi Riyal",
                "SBD": "Solomon Islands Dollar",
                "SCR": "Seychellois Rupee",
                "SDG": "Sudanese Pound",
                "SEK": "Swedish Krona",
                "SGD": "Singapore Dollar",
                "SHP": "Saint Helena Pound",
                "SLL": "Sierra Leonean Leone",
                "SOS": "Somali Shilling",
                "SRD": "Surinamese Dollar",
                "SSP": "South Sudanese Pound",
                "STN": "São Tomé and Príncipe Dobra",
                "SVC": "Salvadoran Colón",
                "SZL": "Swazi Lilangeni",
                "THB": "Thai Baht",
                "TJS": "Tajikistani Somoni",
                "TMT": "Turkmenistani Manat",
                "TND": "Tunisian Dinar",
                "TOP": "Tongan Paʻanga",
                "TRY": "Turkish Lira",
                "TTD": "Trinidad and Tobago Dollar",
                "TWD": "New Taiwan Dollar",
                "TZS": "Tanzanian Shilling",
                "UAH": "Ukrainian Hryvnia",
                "UGX": "Ugandan Shilling",
                "USD": "United States Dollar",
                "UYU": "Uruguayan Peso",
                "UZS": "Uzbekistani Som",
                "VES": "Venezuelan Bolívar",
                "VND": "Vietnamese Dong",
                "VUV": "Vanuatu Vatu",
                "WST": "Samoan Tala",
                "XAF": "Central African CFA Franc",
                "XCD": "East Caribbean Dollar",
                "XOF": "West African CFA Franc",
                "XPF": "CFP Franc",
                "YER": "Yemeni Rial",
                "ZAR": "South African Rand",
                "ZMW": "Zambian Kwacha",
                "ZWL": "Zimbabwean Dollar",
            },
            // Filtered currencies
            currenciesWithRates: {},

            // Default value for the first select
            firstCurr: 'EUR',  
            // Default value for the second select
            secondCurr: 'USD',
            // FirstAmount
            firstAmount: 1,
            // SecondAmount
            secondAmount: 0,
            // Flag to prevent loop
            recalculating: false
        }
    },

    components: {
        OptionsSelect,
    },

    mounted() {
        this.fetchAvailableRates();
    },

    methods: {
        fetchAvailableRates() {
            // Fetch the latest conversion rates from the API
            axios.get(`https://api.frankfurter.app/latest?from=${this.firstCurr}`)
                .then(resp => {
                    const rates = resp.data.rates; // Store available rates

                    // Filter currencies based on available rates
                    // Object.keys(rates): gets an array of the currency codes from the rates object returned by the API. 
                    // Each key represents a currency that has a conversion rate available
                    this.currenciesWithRates = Object.keys(rates).reduce((obj, key) => {
                        // The reduce create a empty object, which will be built during the reduce
                        // For each currency code in rates (API response) checks if exists in hardcoded rates
                        // If it exist add it to the new object
                        if (this.currencies[key]) {
                            // This is the way to add it
                            obj[key] = this.currencies[key];
                        }
                        // Return the object
                        return obj;
                    }, {});

                    // If eur it's not included
                    if (!this.currenciesWithRates['EUR']) {
                        // Eur it's included with the from of the hardcoded element
                        this.currenciesWithRates['EUR'] = this.currencies['EUR'];
                    }

                    // Perform initial conversion
                    this.defaultConversion(); 
                })
                .catch(error => {
                    console.error("Error fetching available rates:", error);
                });
        },

        defaultConversion() {
            if (this.recalculating) return //basically skips if it's inverse calculating so recalculating it's true
            // Passing to api link, the first Amount and the currencies
            axios.get(`https://api.frankfurter.app/latest?amount=${this.firstAmount}&from=${this.firstCurr}&to=${this.secondCurr}`)
                .then(resp => {
                    console.log(resp.data.rates);
                    // In the secondAmount i print the rates given back for the selected curr
                    this.secondAmount = resp.data.rates[this.secondCurr];
                })
                .catch(error => {
                    console.error("Error fetching conversion data:", error);
                });
        },
        inverseConversion() {
            this.recalculating = true; // Set flag to avoid loop
            axios.get(`https://api.frankfurter.app/latest?amount=${this.secondAmount}&from=${this.secondCurr}&to=${this.firstCurr}`)
                .then(resp => {
                    this.firstAmount = resp.data.rates[this.firstCurr];
                    this.recalculating = false; // Reset flag after calculation
                })
                .catch(error => {
                    console.error("Error fetching inverse conversion data:", error);
                    this.recalculating = false; // Reset flag in case of error
                });
        },
    },

    watch: {
        firstAmount: 'defaultConversion',
        firstCurr: 'defaultConversion',
        secondCurr: 'defaultConversion',
        // If recalculating it's false (always except input on second by user), and the newVal in the second amount it's differnt to oldVal
        secondAmount(newVal, oldVal) {
            if (!this.recalculating && newVal !== oldVal) {
                this.inverseConversion(); // Trigger inverse calculation on secondAmount change
            }
        }
    }
}
</script>

<template>
    <h1>Currency Convert</h1>
    <div class="row align-items-center">
        <div class="col-3">
            <input v-model="firstAmount" type="number" class="form-control" aria-label="Amount">
        </div>
        <div class="col-2">
            <OptionsSelect v-model="firstCurr" :currencies="currenciesWithRates"></OptionsSelect>
        </div>

        <div class="col-3">
            <input v-model="secondAmount" type="number" class="form-control" aria-label="Amount">
        </div>
        <div class="col-2">
            <OptionsSelect v-model="secondCurr" :currencies="currenciesWithRates"></OptionsSelect>
        </div>
    </div>
</template>

<style>
</style>