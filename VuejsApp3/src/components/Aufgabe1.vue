<template>
    <div>       
        <h2>{{ UnterschiedOwn }}</h2>
    </div>
</template>

<script>
    import axios from "axios";
    export default {
        name: 'Aufgabe1',
        props: ['host','User'],
        data() {
            return {
                UnterschiedOwn:""
            }
        },
        methods: {
            async submit() {
                await axios.get(`${this.host}/Station/GetIndistinctCount`, this.User.config).then(res => {
                    if (res.data !== null) {
                        const Frage = "The difference between the total number of all cities in the station table and the number of all distinct/unique cities is: "
                        this.UnterschiedOwn = Frage + res.data;
                    }
                })
            },
        }
    }
</script>

<style></style>