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
import { v4 as uuidv4 } from 'uuid';
Vue.use(WebCam);

function dataURLtoFile(dataurl, filename) {
    var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
    while(n--){
        u8arr[n] = bstr.charCodeAt(n);
    }
    return new File([u8arr], filename, {type:mime});
}

export default {
    name: 'app',
    components: {
        'vue-web-cam': WebCam,
    },
    data: function() {
        return {
            shots: [],
            subindex: 0,
            currentId: uuidv4()
        };
    },
    methods: {
        shoot: function(){
            this.shots.push(dataURLtoFile(this.$refs.cam.capture(), `${this.currentId}-${this.subindex}.jpg`))
            this.subindex += 1;
            console.log(this.shots)
        },
        send: function(){
            console.log("Sending shots to S3")
            this.shots = []
            this.subindex = 0
            this.currentId = uuidv4()
        }
    }
}
</script>
