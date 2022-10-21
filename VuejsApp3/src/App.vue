<template>
    <div>
        <div class="login-page">
            <div class="form" v-if="!isLogin">
                <input type="text" placeholder="username" v-model="User.userName" />
                <input type="password" placeholder="password" v-model="User.password" />
                <button type="button" v-on:click="Login">login</button>
            </div>
        </div>
        <div class="Aufgabe" v-if="isLogin">
            <h1>Welcome Dear {{ User.firstName }}</h1>
            <AufgabenBox :host="host" :User="User" />
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import AufgabenBox from "./components/AufgabenBox.vue"

    export default {
        name: 'app',
        components: {
            AufgabenBox
        },
        data() {
            return {
                host: 'https://localhost:7257/api',
                User: {
                    firstName: '',
                    userName: '',
                    password: '',
                    config: '',
                },
                isLogin: false
            }
        },
        methods: {
            Login() {
                axios.get(`${this.host}/login/login?user=${this.User.userName}&password=${this.User.password}`).then(res => {
                    if (res.data.token !== null) {
                        localStorage.setItem('token', JSON.stringify(res.data.token));
                        res.data.token = "";
                        this.isLogin = true;
                        this.User.firstName = res.data.firstName;
                        this.GetTokenConfig();
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
                this.User.config = config;
            }
        }
    }
</script>




<style>
    @import url(https://fonts.googleapis.com/css?family=Roboto:300);

    .Aufgabe {
        width: 50%;
        padding: 2% 0 0;
        margin: auto;
    }

    .login-page {
        width: 360px;
        padding: 2% 0 0;
        margin: auto;
    }

    .form {
        position: relative;
        z-index: 1;
        background: #FFFFFF;
        max-width: 360px;
        margin: 0 auto 100px;
        padding: 45px;
        text-align: center;
        box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
    }

        .form input {
            font-family: "Roboto", sans-serif;
            outline: 0;
            background: #f2f2f2;
            width: 100%;
            border: 0;
            margin: 0 0 15px;
            padding: 15px;
            box-sizing: border-box;
            font-size: 14px;
        }

        .form button {
            font-family: "Roboto", sans-serif;
            text-transform: uppercase;
            outline: 0;
            background: #4CAF50;
            width: 100%;
            border: 0;
            padding: 15px;
            color: #FFFFFF;
            font-size: 14px;
            -webkit-transition: all 0.3 ease;
            transition: all 0.3 ease;
            cursor: pointer;
        }


            .form button:hover, .form button:active, .form button:focus {
                background: #43A047;
            }

        .form .message {
            margin: 15px 0 0;
            color: #b3b3b3;
            font-size: 12px;
        }

            .form .message a {
                color: #4CAF50;
                text-decoration: none;
            }

        .form .register-form {
            display: none;
        }

    .container {
        position: relative;
        z-index: 1;
        max-width: 300px;
        margin: 0 auto;
    }

        .container:before, .container:after {
            content: "";
            display: block;
            clear: both;
        }

        .container .info {
            margin: 50px auto;
            text-align: center;
        }

            .container .info h1 {
                margin: 0 0 15px;
                padding: 0;
                font-size: 36px;
                font-weight: 300;
                color: #1a1a1a;
            }

            .container .info span {
                color: #4d4d4d;
                font-size: 12px;
            }

                .container .info span a {
                    color: #000000;
                    text-decoration: none;
                }

                .container .info span .fa {
                    color: #EF3B3A;
                }

    body {
        background: #76b852; /* fallback for old browsers */
        background: rgb(141,194,111);
        background: linear-gradient(90deg, rgba(141,194,111,1) 0%, rgba(118,184,82,1) 50%);
        font-family: "Roboto", sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }
</style>
