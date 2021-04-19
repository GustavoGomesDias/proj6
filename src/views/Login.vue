<template>
    <div>
        <h2>Login</h2>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="err != undefined">
                    <div class="notification is-danger">
                        <p>{{ err }}</p>
                    </div>
                </div>
                <p>E-mail</p>
                <input type="email" placeholder="exemplo@exemplo.com" class="input" v-model="email">
                <p>Senha</p>
                <input type="password" class="input" placeholder="Senha" v-model="password">
                <button class="button is-success" @click="login">Logar</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return {
            password: '',
            email: '',
            err: undefined
        }
    },
    methods: {
        login(){
            
        }
    }
}
</script>

<style scoped>

</style>

