<template>
    <div>
        <button type="button" v-on:click="Aufgabe1">Aufgabe 1 </button>
        <button type="button" v-on:click="Aufgabe2">Aufgabe 2</button>
        <button type="button" v-on:click="Aufgabe3">Aufgabe 3</button>
        <button type="button" disabled>Aufgabe 4</button>
        <Aufgabe1 :Unterschied="Unterschied" />

        <!--aufgabe2-->
        <!--<h2>HTML Table</h2>
        <table>
            <tr>
                <th>SatationId</th>
                <th>City</th>
                <th>State</th>
                <th>Lat_N</th>
                <th>Long_W</th>
            </tr>
            <tr v-for="station in stations">
                <td>{{Station.SatationId}}
                <td>{{Station.City}}</td>
                <td>{{Station.State}}</td>
                <td>{{Station.Lat_N}}</td>
                <td>{{Station.Long_W}}</td>
            </tr>
        </table>-->
        <!--aufgabe3-->
        <!--<h2>HTML Table</h2>
        <table>
            <tr>
                <th>rownum</th>
                <th>listname</th>
                <th>fullname</th>
            </tr>
            <tr v-for="waitlist in waitlists">
                <td>{{waitlist.rownum}}</td>
                <td>{{waitlist.listname}}</td>
                <td>{{waitlist.fullname}}</td>
            </tr>
        </table>-->

    </div>
</template>

<script>
    import axios from "axios";
    import Aufgabe1 from "./Aufgabe1.vue";

    export default {
        name: 'AufgabenBox',
        components: {
            Aufgabe1
        },
        data() {
            return {
                host: 'https://localhost:44384/api',
                Unterschied: '',
            }
        },
        methods: {
            async Aufgabe1() {
                await axios.get(`${this.host}/Station/GetIndistinctCount`, this.GetTokenConfig()).then(res => {
                    if (res.data !== null) {
                        const Frage = "The difference between the total number of all cities in the station table and the number of all distinct/unique cities is: "
                        this.Unterschied = Frage + res.data;
                    }
                })
            },
            async Aufgabe2() {
                await axios.get(`${this.host}/Station/GetAllCitiesEndWithVowels`, this.GetTokenConfig()).then(res => {
                    if (res.data !== null) {
                        console.log(res.data);
                    }
                })
            },
            async Aufgabe3() {
                await axios.get(`${this.host}/waitlist/GetAllWaitlistAdminStructure`, this.GetTokenConfig()).then(res => {
                    if (res.data !== null) {
                        console.log(res.data);
                    }
                })
            },
            GetTokenConfig() {
                var token = JSON.parse(localStorage.getItem('token'));
                const config = {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                };
                return config;
            }
        }
    }
</script>




<style>
    .Aufgabe Button {
        font-family: "Roboto", sans-serif;
        text-transform: uppercase;
        outline: 0;
        background: #4CAF50;
        width: 20%;
        border: 0;
        padding: 15px;
        margin: 5px;
        color: #FFFFFF;
        font-size: 14px;
        -webkit-transition: all 0.3 ease;
        transition: all 0.3 ease;
        cursor: pointer;
    }
</style>
