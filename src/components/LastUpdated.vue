<template>
    <div class="-mt-2 pb-2 py-1 pr-4 bg-[#0053B6] text-white text-sm text-right text-gray-500">
        Last updated on {{ timestamp }}
    </div>
</template>

<script setup>
defineProps(['timestamp'])
</script>