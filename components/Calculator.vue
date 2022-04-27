<template>
    <div class="calculator">
        <div class="points">
            <pointForm :header="'Point 1'" :point="point1" />
            <pointForm :header="'Point 2'" :point="point2" />
        </div>
        <div class="result" v-if="result" v-html="`Calculated distance is <b>${result}</b>`"></div>
        <div class="tools">
            <button type="button" @click="calculate">Calculate</button>
            <button type="button" @click="clearData">Clear</button>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import pointForm from './PointForm.vue';

const earthRadius = 6372795;

export default defineComponent({
        data(){
            return { 
                point1: {
                    lat: '',
                    lng: '',
                    error: false
                },
                point2: {
                    lat: '',
                    lng: '',
                    error: false
                },
                result: '',
            }
        },
        components: {
            pointForm
        },
        methods: {
            calculate(){
                this.result = '';
                if(!this.errors()){
                    let cl1: number = Math.cos(this.degToRad(+this.point1.lat));
                    let cl2: number = Math.cos(this.degToRad(+this.point2.lat));
                    let sl1: number = Math.sin(this.degToRad(+this.point1.lat));
                    let sl2: number = Math.sin(this.degToRad(+this.point2.lat));
                    let delta: number = this.degToRad(+this.point2.lng) - this.degToRad(+this.point1.lng);
                    let cdelta: number = Math.cos(delta);
                    let sdelta: number = Math.sin(delta);

                    let y: number = Math.sqrt(Math.pow(cl2 * sdelta, 2) + Math.pow(cl1 * sl2 - sl1 * cl2 * cdelta, 2));
                    let x: number = sl1 * sl2 + cl1 * cl2 * cdelta;

                    let distance = Math.floor(Math.atan2(y, x) * earthRadius);
                    this.result = this.format(distance);
                }
            },
            errors(): boolean{
                return this.point1.error || this.point2.error
            },
            degToRad(degree: number): number{
                return (degree * Math.PI) / 180;
            },
            format(distance: number): string{
                let km = distance / 1000;
                let m = distance % 1000;

                return (km > 1) ?  `${km.toFixed(0)} km and ${m} meters` : `${m} meters`;
            },
            clearData(){
                this.point1 = {
                    lat: '',
                    lng: '',
                    error: false
                };
                this.point2 = {
                    lat: '',
                    lng: '',
                    error: false
                };
                this.result = '';
            }
        }
    });
</script>