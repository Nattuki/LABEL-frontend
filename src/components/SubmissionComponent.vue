<template>
    <div :class="$style.container">
        <div :class="$style.iframeWrapper">
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
        <div :class="$style.labelsWrapper">
            <label-component 
              @seek="seekTo" 
              :class="$style.label"
              :text="'seek1'"
              :TimeToSeek="10"
            />
            <label-component 
              @seek="seekTo" 
              :class="$style.label"
              :text="'seek2'"
              :TimeToSeek="20"
            />
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import LabelComponent from './LabelComponent.vue';

const embed = ref<HTMLIFrameElement | null>(null)
const url = 'https://www.youtube.com/embed/ef41Q2-DQ2Q?enablejsapi=1'

const seekTo = (TimeToSeek: number[]) => {
    const TimeToSeekJSON = TimeToSeek !== undefined ? JSON.stringify(TimeToSeek) : '""'
    embed.value?.contentWindow?.postMessage(`{"event":"command","func":"seekTo","args":${TimeToSeekJSON}}`, '*')
}

</script>

<style lang="scss" module>
.container{
    border:1px solid red;
}

</style>