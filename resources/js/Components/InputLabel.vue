<script setup>
defineProps(["value"]);
</script>

<template>
    <label class="font-normal text-lg text-white block mb-3">
        <span v-if="value">{{ value }}</span>
        <span v-else><slot /></span>
    </label>
</template>