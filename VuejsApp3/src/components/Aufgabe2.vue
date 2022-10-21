<template>
    <div>
        <table>
            <tr>
                <th>SatationId</th>
                <th>City</th>
                <th>State</th>
                <th>Lat_N</th>
                <th>Long_W</th>
            </tr>
            <tr v-for="Station in Stations">
                <td>{{Station.SatationId}}</td>
                <td>{{Station.City}}</td>
                <td>{{Station.State}}</td>
                <td>{{Station.Lat_N}}</td>
                <td>{{Station.Long_W}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    import axios from "axios";
    export default {
        name: 'Aufgabe2',
        props: ['host', 'User'],
        data() {
            return {
                Stations: {
                    SatationId: '',
                    City: '',
                    Lat_N: '',
                    Long_W: '',
                }
            }
        },
        methods: {
            async submit() {
                await axios.get(`${this.host}/Station/GetAllCitiesEndWithVowels`, this.User.config).then(res => {
                    if (res.data !== null) {
                        console.log(res.data);
                        console.log("Ehsan");
                    }
                })
            }
        }
    }
</script>

<style></style>