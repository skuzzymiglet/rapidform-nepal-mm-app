<template>
    <div id="app">
        <vue-web-cam height="500" width="500"/>
    </div>
</template>

<script>
    import Vue from 'vue'
    import { WebCam } from 'vue-web-cam';
    Vue.use(WebCam);
</script>
