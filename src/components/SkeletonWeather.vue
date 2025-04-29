<template>
    <div class=" space-y-4 " shadow="hover">
        <el-card>
            <template #header>
                <div class="card-header">
                    <h2 class="text-xl font-bold">Next hours</h2>
                </div>
            </template>

            <ul class="flex justify-between h-[7.5rem]">
                <li v-for="n in 4" :key="n" class="flex flex-col items-center">
                </li>
            </ul>
        </el-card>


        <el-card class="custom-card mt-4" shadow="hover">
            <template #header>
                <div class="card-header">
                    <h2 class="text-xl font-bold">Next 5 days</h2>
                </div>
            </template>

            <ul class="flex flex-col justify-between py-0 h-[404px]">
                <li v-for="n in 5" :key="n"
                    class="flex flex-row justify-between items-center border-b last:border-b-0 border-el-card p-4 h-[5rem]">
                </li>
            </ul>
        </el-card>
    </div>
</template>

<style scoped>
.custom-card :deep(.el-card__body) {
    padding: 0 !important;
}
</style>