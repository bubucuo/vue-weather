<template>
    <el-tabs v-model="localSelectedCity" @tab-click="handleTabChange" class="px-4 bg-[#F9F9F9]">
        <el-tab-pane v-for="city in cities" :key="city" :label="city" :name="city" />
    </el-tabs>
</template>

<script setup>
const props = defineProps({
    cities: {
        type: Array,
        required: true
    },
    selectedCity: {
        type: String,
        required: true
    }
})

const emit = defineEmits(['update:selectedCity'])

import { ref, watch } from 'vue'

const localSelectedCity = ref(props.selectedCity)

watch(() => props.selectedCity, (newVal) => {
    localSelectedCity.value = newVal
})

// change tab and emit event to parent
const handleTabChange = (tab) => {
    emit('update:selectedCity', tab.props.name)
}
</script>

<style scoped>
:deep(.el-tabs__item) {
    color: #656565;
}

:deep(.el-tabs__active-bar) {
    background-color: #F4492F;
}

:deep(.el-tabs__item.is-active),
:deep(.el-tabs__item:hover) {
    color: #191919;
    font-weight: bold;
}

:deep(.el-tabs__nav-wrap:after) {
    background-color: transparent;
}

:deep(.el-tabs__header) {
    margin: 0;
}
</style>