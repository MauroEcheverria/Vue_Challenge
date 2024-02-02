<template>
    <div class="card">
        <div class="card-header">
            History
        </div>
        <div class="card-body" v-if="loading">
            <div>Nothing to show...!!!</div>
        </div>
        <div class="card-body" v-else v-for="(est, i) in dataMarvelSeries" :key="est.id">
            <div class="car-title">
                <span>{{ est.title }}</span>
            </div>
            <div class="card-label">
                <div class="card-control">
                    <label for="">Type:</label>
                    <span>{{ est.type }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
    import axios from 'axios'
    import { useRoute } from 'vue-router';

    export default {
        data(){
            return{
                id:0,
                url:'',
                loading:false,
                dataMarvelSeries:null,
                url_1:'https://gateway.marvel.com/v1/public/series/',
                url_2:'/stories?apikey=bda5344a533213715e00c2d21b001804&ts=1&hash=75eb500b25640eba1ed982e4cb66eded',
            }
        },
        mounted(){
            const route = useRoute();
            this.id = route.params.id;
            this.url = this.url_1+this.id+this.url_2;
            this.getDataMarvelSeries();
        },
        methods:{
            getDataMarvelSeries(){
                axios
                .get(this.url)
                .then(
                    res => {
                        console.log(res.data.data.results);
                        this.dataMarvelSeries = res.data.data.results;
                        if(res.data.data.results.length == 0) {
                            this.loading = true;
                        }
                        else {
                            this.loading = false;
                        }
                    }
                );
            }
        }
    }
</script>

<style scoped>
    .card {
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        width: 500px;
    }
    .card:hover {
        box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
    }
    .card-body {
        padding: 2px 16px;
    }
    .card-header {
        font-size: 25px;
        font-weight: 500;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        margin-bottom: 20px;
        border-radius: 9px;
    }
    .car-title{
        font-size: 17px;
        font-weight: bold !important;
        text-decoration: underline;
        margin: 15px 0 15px 0;
    }
    .card-label {
        margin-bottom: 20px;
    }
    .card-control {
        text-align: left;
        margin: 6px 0 6px 10px;
    }
    .card-control label {
        font-weight: 500;
    }
    .card-control span {
        margin-left: 10px;
    }
</style>