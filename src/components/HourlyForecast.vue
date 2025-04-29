<template>
    <el-card class="weather-card" shadow="hover">
        <template #header>
            <div class="card-header">
                <h2 class="text-xl font-bold">Next hours</h2>
            </div>
        </template>

        <ul class="flex justify-between">
            <li v-for="(item, index) in hourlyData" :key="item.time" class="flex flex-col items-center relative px-2">
                <div class="text-2xl font-semibold">
                    {{ item.temp }}°
                </div>

                <div class="mt-2 text-[#15B1D6] text-sm ">
                    {{ item.rain }}
                </div>

                <img :src="`https://openweathermap.org/img/wn/${item.icon}@2x.png`" alt="Weather Icon"
                    class="w-10 h-10" />
                <div class=" text-sm text-gray-600">
                    {{ item.time }}
                </div>

                <div v-if="index !== hourlyData.length - 1"
                    class="absolute right-[-1px] top-[1.75rem] h-[3.75rem] w-px border-el-card border-l-1">
                </div>
            </li>

        </ul>
    </el-card>
</template>

<script setup>

const { hourlyData } = defineProps({
    hourlyData: Array
})

</script>
