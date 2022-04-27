<template>
    <div class="point">
        <h4 v-html="header"></h4>
        <div class="form-control">
            <input type="text" v-model="point.lat" placeholder="Latitude" />
        </div>
        <div class="form-control">
            <input type="text" v-model="point.lng" placeholder="Longitude" />
        </div>
        <div class="form-errors" v-if="errors.length > 0">
            <div class="form-error" v-for="(error, i) in errors" :key="i" v-html="error"></div>
        </div>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from "vue"
    export default defineComponent({
        props: {
            header: {type: String},
            point: {type: Object}
        },
        computed: {
            errors(){
                if(this.point){
                    let errors = [];

                    if(+this.point.lat < -90 || +this.point.lat > 90 || isNaN(+this.point.lat)){
                        errors.push('Point latitude must be decimal value between -90 and 90');
                    }

                    if(+this.point.lng < -180 || +this.point.lng > 180 || isNaN(+this.point.lng)){
                        errors.push('Point 1 longtitude must be decimal value between -180 and 180');
                    }

                    this.point.error = (errors.length > 0) ? true : false;

                    return errors;
                }
            }
        }
    });
</script>