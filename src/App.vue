<template>
    <div id="app">
        <vue-web-cam ref="cam" :selectFirstDevice="true"/>
        <button v-on:click="send()">Honkass</button>
    </div>
</template>

<script>
import Vue from 'vue'
import { WebCam } from 'vue-web-cam';
Vue.use(WebCam);
import { base64ToBlob } from 'base64toblob';

export default {
    name: 'app',
    components: {
        'vue-web-cam': WebCam,
    },
    methods: {
        send: function(){
            console.log(this.$refs.cam.capture())
        }
    }
}
</script>
