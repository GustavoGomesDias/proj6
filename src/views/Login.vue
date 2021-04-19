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
            axios.post("http://localhost:8686/login", {
                password: this.password,
                email: this.email
            }).then((res) => {
                // Salvando o token no local storage do navegador
                
                localStorage.setItem('token', res.data.token);
                this.$router.push({ name: 'Home' })
            }).catch(err => {
                // Pra pegar o erro, na dúvida, console.log(err.response);
                const msgErr = err.response.data.err;
                this.err = msgErr; 
            });
        }
    }
}
</script>

<style scoped>

</style>

