<template>
    <el-card class="custom-card mt-4" shadow="hover">
        <template #header>
            <div class="card-header">
                <h2 class="text-xl font-bold">Next 5 days</h2>
            </div>
        </template>


        <ul class="flex flex-col justify-between py-0">
            <li v-for="(item, index) in dailyData" :key="item.time"
                class="flex flex-row justify-between items-center border-b last:border-b-0 border-el-card p-4">
                <img :src="`https://openweathermap.org/img/wn/${item.icon}@2x.png`" alt="Weather Icon"
                    class="w-10 h-10" />

                <div class="text-base text-center">
                    <div class="font-bold">{{ item.date }}</div>
                    <div class="text-gray-600">{{ item.desc }}</div>
                </div>


                <div class="text-sm text-gray-600 font-bold">
                    {{ item.high }}° {{ item.low }}°
                </div>
            </li>

        </ul>

    </el-card>

</template>

<script setup>

const { dailyData } = defineProps({
    dailyData: Array
})

</script>


<style scoped>
.custom-card :deep(.el-card__body) {
    padding: 0 !important;
}
</style>
