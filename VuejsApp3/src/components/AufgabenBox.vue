<template>
    <div>
        <button type="button" v-on:click="Aufgabe1()">Aufgabe 1</button>
        <button type="button" v-on:click="Aufgabe2()">Aufgabe 2</button>
        <button type="button" v-on:click="Aufgabe3()">Aufgabe 3</button>
        <button type="button" disabled>Aufgabe 4</button>

        <p>{{ selectedComponent }}</p>
        <component :is="selectedComponent" :host="host" :User="User" ref="Aufgaben"></component>

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
    import Aufgabe2 from "./Aufgabe2.vue";

    export default {
        name: 'AufgabenBox',
        components: {
            Aufgabe1,
            Aufgabe2
        },
        props: ["host","User"],
        data() {
            return {
                Unterschied: '',
                selectedComponent: "Aufgabe1",
            }
        },
        methods: {
            async Aufgabe1() {
                this.$refs.Aufgaben.submit()
                this.selectedComponent= "Aufgabe1"
            },
            async Aufgabe2() {
                this.$refs.Aufgaben.submit()
                this.selectedComponent = "Aufgabe2"
            },
            async Aufgabe3() {
                await axios.get(`${this.host}/waitlist/GetAllWaitlistAdminStructure`, this.GetTokenConfig()).then(res => {
                    if (res.data !== null) {
                        console.log(res.data);
                    }
                })
            },
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
