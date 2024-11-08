<template>
    <h3 class="text-center text-uppercase mt-3">Rates in the last 30 days</h3>
    <div>
        <!-- Render the chart only when chartData is available -->
        <LineChart v-if="chartData" :data="chartData" :options="chartOptions" />
        <p v-else>Loading chart...</p>
    </div>
</template>

<script>
import { Line } from 'vue-chartjs'
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    LineElement,
    CategoryScale,
    LinearScale,
    PointElement,
    Filler
} from 'chart.js'

// Register required components globally
ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale, PointElement, Filler)

export default {
    name: 'Charts',
    components: {
        LineChart: Line
    },
    props: {
        firstCurr: String,
        secondCurr: String,
    },
    data() {
        return {
            chartData: null,
            chartOptions: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: true,
                        position: 'top'
                    }
                }
            }
        }
    },
    async mounted() {
        await this.fetchChartData(); // Initial chart data fetch
    },
    watch: {
        firstCurr(newValue, oldValue) {
            if (newValue !== oldValue) {
                this.fetchChartData(); // Re-fetch data when firstCurr changes
            }
        },
        secondCurr(newValue, oldValue) {
            if (newValue !== oldValue) {
                this.fetchChartData(); // Re-fetch data when secondCurr changes
            }
        }
    },
    methods: {
        async fetchChartData() {
            const baseCurrency = this.firstCurr
            const targetCurrency = this.secondCurr
            const endDate = new Date().toISOString().slice(0, 10)
            const startDate = new Date()
            startDate.setDate(startDate.getDate() - 30)
            const startDateString = startDate.toISOString().slice(0, 10)

            try {
                const response = await fetch(`https://api.frankfurter.app/${startDateString}..${endDate}?from=${baseCurrency}&to=${targetCurrency}`)
                if (!response.ok) throw new Error('Failed to fetch data')
                const data = await response.json()

                // Validate and process the API response data
                if (data && data.rates) {
                    const labels = Object.keys(data.rates)
                    const values = labels.map(date => data.rates[date][targetCurrency])

                    // Ensure the structure of chartData is correct for vue-chartjs
                    this.chartData = {
                        labels,
                        datasets: [
                            {
                                label: `${baseCurrency} to ${targetCurrency} Exchange Rate`,
                                data: values,
                                borderColor: '#5ffe74',
                                backgroundColor: '#79a47155',
                                fill: true,
                                tension: 0.4
                            }
                        ]
                    }
                } else {
                    console.error("Unexpected data format from API")
                }
            } catch (error) {
                console.error("Error fetching data from Frankfurter API:", error)
            }
        }
    }
}
</script>

<style scoped lang="scss">
@import '../style/general.scss';

h3 {
    color: $white;
}
div {
    color: $white;
    background-color: $white;
    border-radius: 0.5rem;
    width: 100%;
    margin: 0 auto;
    padding: 3rem;
}
</style>