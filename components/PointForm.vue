<template>
    <div class="point">
        <h4 v-html="header"></h4>
        <div class="form-control">
            <input type="text" v-model="point.lat" placeholder="Latitude" />
        </div>
        <div class="form-control">
            <input type="text" v-model="point.lng" placeholder="Longitude" />
        </div>
        <div class="form-errors" v-if="point.errors.length > 0">
            <div class="form-error" v-for="(error, i) in point.errors" :key="i" v-html="error"></div>
        </div>
    </div>
</template>

<script lang="ts">
    export default {
        props: {
            header: {type: String},
            point: {type: Object}
        },
    };
</script>