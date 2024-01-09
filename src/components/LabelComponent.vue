<template>
    <div class="container">
        <button @click="$emit('seek', [TimeToSeek])">
            {{ props.text }}
        </button>
    </div>
</template>

<script setup lang="ts">

const props = withDefaults(
    defineProps<{
        text?: string
        TimeToSeek: number
    }>(),
    {
        text: 'seek!'
    }
)

</script>

<style>

</style>