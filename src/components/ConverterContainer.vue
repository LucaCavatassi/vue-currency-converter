<script>
import axios from 'axios';
import OptionsSelect from '../components/OptionsSelect.vue';
import debounce from 'lodash/debounce';

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
            currenciesWithRates: {},
            firstCurr: 'EUR',
            secondCurr: 'USD',
            firstAmount: 1,
            secondAmount: 0,
            isCalculating: false,
        }
    },

    components: {
        OptionsSelect,
    },

    mounted() {
        this.fetchAvailableRates();
        this.defaultConversion();
    },

    methods: {
        fetchAvailableRates() {
            axios.get(`https://api.frankfurter.app/latest?from=${this.firstCurr}`)
                .then(resp => {
                    let rates = resp.data.rates;

                    // Check if EUR is missing, if not add manually and gives a dull value of 1
                    if (!rates['EUR']) {
                        rates['EUR'] = 1; 
                    }

                    // Object keys extract only the keys (EUR, USD etc...)
                    this.currenciesWithRates = Object.keys(rates)
                        .sort()  // Sort currency codes in rates alphabetically
                        // Reduce takes obj as an accumulator (final result) and iterate the second element so the keys and apply the function
                        .reduce((obj, key) => {
                            // This function for each currency code (key), it checks if there’s a corresponding value in this.currencies 
                            obj[key] = this.currencies[key] || rates[key];  // if not apply it's rate
                            return obj;
                        }, {});
                })
                .catch(error => {
                    console.error("Error fetching available rates:", error);
                });
        },

        defaultConversion() {
            if (this.firstAmount < 0 || this.secondAmount < 0 || this.firstCurr === this.secondCurr) {
                alert('error')
            } else {
                if (!this.isCalculating) {
                    axios.get(`https://api.frankfurter.app/latest?amount=${this.firstAmount}&from=${this.firstCurr}&to=${this.secondCurr}`)
                        .then(resp => {
                            this.secondAmount = resp.data.rates[this.secondCurr];
                        })
                        .catch(error => {
                            console.error("Error fetching conversion data:", error);
                        });
                } else {
                    axios.get(`https://api.frankfurter.app/latest?amount=${this.secondAmount}&from=${this.secondCurr}&to=${this.firstCurr}`)
                        .then(resp => {
                            this.firstAmount = resp.data.rates[this.firstCurr];
                        })
                        .catch(error => {
                            console.error("Error fetching inverse conversion data:", error);
                        });
                }
            }
        },

        inverseConversion() {
            this.isCalculating = true;
        },

        // Debounced version of the conversion method
        debouncedDefaultConversion: debounce(function () {
            this.defaultConversion();
        }, 500)

    },

    watch: {
        firstAmount() {
            this.debouncedDefaultConversion();
        },
        secondAmount() {
            this.debouncedDefaultConversion();
        },
        firstCurr() {
            this.debouncedDefaultConversion();
        },
        secondCurr() {
            this.debouncedDefaultConversion();
        },
    },
}
</script>

<template>
    <h1 class="mb-3 fs-1 text-center text-uppercase">Currency Converter</h1>
    <div class="mt-3 container ms-cont p-5">

        <div class="ms-info">
            <p class="fs-4 ms-1 mb-0">
                <strong>{{ Math.trunc(firstAmount*100)/100  }} {{ firstCurr }}</strong> -
                <span class="fs-5">{{ currenciesWithRates[firstCurr] }}</span> 
                <span class="fs-6 ms-3"><i>equals</i></span>
            </p>
            <p class="fs-5 ms-1">
                <strong>{{ Math.trunc(secondAmount*100)/100 }} {{ secondCurr }}</strong> -
                <span class="fs-5">{{ currenciesWithRates[secondCurr] }}</span>
            </p>
        </div>

        <!-- First -->
        <div class="row align-items-center mb-3">
            <!-- Input -->
            <div class="col-8">
                <input @keyup="isCalculating = false" v-model="firstAmount" type="number" class="ms-input form-control bg-dark"
                    aria-label="amount">
            </div>
            <!-- Input -->
    
            <!-- Option -->
            <div class="col-4">
                <OptionsSelect v-model="firstCurr" :currencies="currenciesWithRates" />
            </div>
            <!-- Option -->
        </div>
        <!-- First -->
    
        <!-- Second -->
        <div class="row align-items-center">
            <!-- Input -->
            <div class="col-8">
                <input @keyup="inverseConversion" v-model="secondAmount" type="number" class="ms-input form-control bg-dark"
                    aria-label="amount">
            </div>
            <!-- Input -->
    
            <!-- Option -->
            <div class="col-4">
                <OptionsSelect v-model="secondCurr" :currencies="currenciesWithRates" />
            </div>
            <!-- Option -->
        </div>
        <!-- Second -->
    </div>

</template>

<style scoped lang="scss">
    @import '../style/general.scss';

    // Container
    .ms-cont{
        border: 0.3rem solid $white;
        border-radius: 0.5rem;
        color: $white;
    }

    // Title
    h1 {
        color: $white
    }

    // Inputs
    .ms-input {
        @include inputsStyles($dollarGreen, $focusGreen);
    }
</style>