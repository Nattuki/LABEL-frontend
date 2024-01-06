<template>
    <div :class="$style.container">
        <div class="$style.iframeWrapper">
            <iframe 
              ref="embed" 
              :src="url"
              width="560" 
              height="315" 
              title="YouTube video player" 
              frameborder="0" 
              allow="clipboard-write; encrypted-media">
            </iframe>
        </div>
        <div class="$style.labelsWrapper">
            <label-component @seek="seekTo" class="$style.label" />
        </div>
        <button class="$style.addLabelButton"></button>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import LabelComponent from './LabelComponent.vue';

const embed = ref<HTMLIFrameElement | null>(null)

const seekTo = function (TimeToSeek: number) {
    const target = embed.value
    target?.contentWindow?.postMessage(`{"event":"command","func":"seekTo","args":${TimeToSeek}}`, '*')
}

</script>

<style lang="scss" module>


</style>