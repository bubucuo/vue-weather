<template>
    <el-header class="bg-blue-700 text-white h-14 px-4 flex items-center">
        <div class="flex justify-between items-center w-full">
            <div class="text-lg font-bold">Simple Weather</div>
            <el-icon class="w-6 h-6 cursor-pointer ">
                <Search />
            </el-icon>
        </div>
    </el-header>
</template>

<script setup>
import { ElHeader, ElIcon } from 'element-plus'
import { Search } from '@element-plus/icons-vue'
</script>