<template>
    <table class="styled-table">
        <thead>
            <tr>
                <th scope="col">Imagen</th>
                <th scope="col">Title</th>
                <th scope="col">Year</th>
                <th scope="col">Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-if="loading">
                <td colspan="4"><h3>Loading...</h3></td>
            </tr>
            <tr v-else v-for="(est, i) in dataMarvelSeries" :key="est.id">
                <td>
                    <a :href="est.thumbnail.path +'.'+ est.thumbnail.extension" target="_blank">
                        <img :src="est.thumbnail.path +'.'+ est.thumbnail.extension" alt="" class="img_table">
                    </a>
                </td>
                <td v-text="est.title"></td>
                <td v-text="est.endYear"></td>
                <td class="tbl_details">
                    <RouterLink :to="{path: 'detail/'+est.id}">🔎</RouterLink>
                </td>
            </tr>
        </tbody>
    </table>
 </template>

<script lang="ts">
    import axios from 'axios'
    export default {
        data(){
            return{
                dataMarvelSeries:null,
                loading:false
            }
        },
        mounted(){
            this.getDataMarvelSeries();
        },
        methods:{
            getDataMarvelSeries(){
                this.loading = true;
                axios
                .get('https://gateway.marvel.com/v1/public/series?apikey=bda5344a533213715e00c2d21b001804&ts=1&hash=75eb500b25640eba1ed982e4cb66eded')
                .then(
                    res => {
                        console.log(res.data.data.results);
                       this.dataMarvelSeries = res.data.data.results;
                       this.loading = false;
                    }
                );
            }
        }
    }
</script>

<style scoped>
    .styled-table{
        margin: 0 auto;
        border-collapse: collapse;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
    }
    .styled-table thead tr {
        background-color: #009879;
        color: #ffffff;
        font-size: 17px;
        font-weight: bold;
    }
    .styled-table th,
    .styled-table td {
        padding: 12px 15px;
    }
    .styled-table tbody tr {
        border-bottom: 1px solid #dddddd;
    }
    .styled-table tbody tr:nth-of-type(even) {
        background-color: #f3f3f3;
    }
    .styled-table tbody tr:last-of-type {
        border-bottom: 2px solid #009879;
    }
        .styled-table tbody tr.active-row {
        font-weight: bold;
        color: #009879;
    }
    .img_table{
        width: 65px;
        border-radius: 10px;
    }
    .tbl_details {
        text-align: center;
    }
</style>