<template>
    <div class="text-gray-800">
        <SearchTab />
        <CityTabs :cities="cities" :selectedCity="selectedCity" v-model:selectedCity="selectedCity"
            @update:selectedCity="handleCityChange" />

        <div class="px-4 py-1 bg-gradient-to-b from-[#006FA2] from-70% to-[#D5C2B3] to-30% ">
            <template v-if="isLoading">
                <SkeletonWeather />
            </template>
            <template v-else>
                <HourlyForecast :hourlyData="hourlyData" />
                <DailyForecast :dailyData="dailyData" />
            </template>
        </div>

        <LastUpdated v-if="!isLoading" :timestamp="lastUpdated" />
    </div>
</template>

<script setup>
import { ref, reactive, watch, onMounted, onBeforeUnmount } from 'vue'
import { fetchWeatherData } from './mock'
import SearchTab from '@/components/SearchTab.vue'
import CityTabs from '@/components/CityTabs.vue'
import HourlyForecast from '@/components/HourlyForecast.vue'
import DailyForecast from '@/components/DailyForecast.vue'
import LastUpdated from '@/components/LastUpdated.vue'
import SkeletonWeather from '@/components/SkeletonWeather.vue'

const isLoading = ref(true)


const weatherData = reactive({
    current: {},
    hourly: [],
    daily: [],
})


const updateWeatherData = (data) => {
    weatherData.current = data.current
    weatherData.hourly = data.hourly
    weatherData.daily = data.daily

    hourlyData.value = data.hourly.map(item => ({
        time: new Date(item.dt * 1000).toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: true }),
        temp: Math.round(item.temp - 273.15),
        rain: Math.round(item.pop * 100) + '%',
        icon: item.weather[0].icon
    }));

    dailyData.value = data.daily.map(item => ({
        date: new Date(item.dt * 1000).toLocaleDateString('en-US', { weekday: 'short', month: 'short', day: 'numeric' }),
        desc: item.weather[0].description,
        high: Math.round(item.temp.max - 273.15),
        low: Math.round(item.temp.min - 273.15),
        icon: item.weather[0].icon
    }));

    lastUpdated.value = new Date(data.current.dt * 1000).toLocaleString('en-US', {
        weekday: 'short',
        month: 'short',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
    });
}

const cities = ['RIO DE JANEIRO', 'BEIJING', 'LOS ANGELES']
const selectedCity = ref('LOS ANGELES')

const hourlyData = ref([])
const dailyData = ref([])
const lastUpdated = ref('')


const handleCityChange = async (newCity) => {
    isLoading.value = true
    try {
        // const res = await fetch(`https://api.example.com/weather?city=${encodeURIComponent(newCity)}`)
        // const data = await res.json()
        const data = await fetchWeatherData(newCity)
        updateWeatherData(data)
    } catch (err) {
        console.error('Failed to fetch weather data:', err)
    } finally {
        isLoading.value = false
    }
}




onMounted(() => {
    handleCityChange(selectedCity.value)
})


// refresh when pull down
let startY = 0
let isRefreshing = false

const onTouchStart = (e) => {
    if (window.scrollY === 0) {
        startY = e.touches[0].clientY
    }
}

const onTouchMove = (e) => {
    const deltaY = e.touches[0].clientY - startY
    if (window.scrollY === 0 && deltaY > 100 && !isRefreshing) {
        isRefreshing = true
        console.log('Refreshing weather data...')
        handleCityChange(selectedCity.value).finally(() => {
            setTimeout(() => {
                isRefreshing = false
            }, 1000)
        })
    }
}

onMounted(() => {
    handleCityChange(selectedCity.value)

    window.addEventListener('touchstart', onTouchStart)
    window.addEventListener('touchmove', onTouchMove)
})

onBeforeUnmount(() => {
    window.removeEventListener('touchstart', onTouchStart)
    window.removeEventListener('touchmove', onTouchMove)
})
</script>