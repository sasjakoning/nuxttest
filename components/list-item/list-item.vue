<template>
    <li class="list-item">
        <slot></slot>
        <button @click="$emit('remove')">Remove</button>
    </li>
</template>

<script setup>
</script>

<style lang="scss">
@import 'list-item.scss';
</style>