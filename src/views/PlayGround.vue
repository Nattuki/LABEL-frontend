<template>
  <iframe ref="embed" :src="url"
    width="560" height="315" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  <div class="controller">
    <button @click="onStop">■</button>
    <button @click="onPause">||</button>
    <button @click="onPlay">▶</button>
    <input type="number" min="0" v-model="seekPosition" />
    <button @click="onSeek">シーク</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    data () {
    return {
        url: 'https://www.youtube.com/embed/ef41Q2-DQ2Q?enablejsapi=1',
        seekPosition: 0 // シーク位置
    }
},
methods: {
    onPlay () {
        this.sendVideoControl(this.$refs.embed, 'playVideo') // 再生
    },
    onPause () {
        this.sendVideoControl(this.$refs.embed, 'pauseVideo') // 一時停止
    },
    onStop () {
        this.sendVideoControl(this.$refs.embed, 'stopVideo') // 停止（一時停止＋再生位置を0秒に）
    },
    onSeek () {
        this.sendVideoControl(this.$refs.embed, 'seekTo', [this.seekPosition]) // 指定秒数へシーク
    },
    sendVideoControl (target, method, args?) {
    const _args = args !== undefined ? JSON.stringify(args) : '""'
    target.contentWindow.postMessage(`{"event":"command","func":"${method}","args":${_args}}`, '*')
}
}
})



</script>