<template>
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
    PointElement
} from 'chart.js'

// Register required components globally
ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale, PointElement)

export default {
    name: 'Charts',
    components: {
        LineChart: Line
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
        const baseCurrency = 'USD'
        const targetCurrency = 'EUR'
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
                            borderColor: '#42A5F5',
                            backgroundColor: 'rgba(66, 165, 245, 0.2)',
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
</script>

<style scoped>
div {
    background-color: white;
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
}
</style>