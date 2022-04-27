<template>
    <div class="container">
        <h1>Calculator</h1>
        <h3>Application can calculate distance between two geographical points. Each point have to be defined by two coordiantes: longitude and latitude. Application support just only decimal degrees, uses the haversine formula to calculate the result.</h3>
        <Calculator />
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    import Calculator from './Calculator.vue';

    export default defineComponent({
        components:{
            Calculator
        }
    });
</script>