<template>
    <div class="container">
        <button @click="$emit('seek', TimeToSeek)">

        </button>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const TimeToSeek = ref(10);

</script>

<style>

</style>