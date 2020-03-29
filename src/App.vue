<template>
    <div id="app">
        <vue-web-cam ref="cam" :selectFirstDevice="true"/>
            <button v-on:click="shoot()">Capture</button>
            <button v-on:click="send()">Next Form</button>
    </div>
</template>

<script>
import Vue from 'vue'
import { WebCam } from 'vue-web-cam';
Vue.use(WebCam);

export default {
    name: 'app',
    components: {
        'vue-web-cam': WebCam,
    },
    data: function() {
        return {
            shots: []
        };
    },
    methods: {
        shoot: function(){
            fetch(this.$refs.cam.capture()).then(res => res.blob).then(e => this.shots.push(e))
            console.log(this.shots)
        },
        send: function(){
            console.log("Sending shots to S3")
            this.shots = []
        }
    }
}
</script>
