<template>
    <div>
        <h2>Registro de Usuário</h2>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="err != undefined">
                    <div class="notification is-danger">
                        <p>{{ err }}</p>
                    </div>
                </div>

                <p>Nome</p>
                <input type="text" placeholder="Nome do usuário" class="input is-half" v-model="name">
                <p>E-mail</p>
                <input type="email" placeholder="exemplo@exemplo.com" class="input" v-model="email">
                <p>Senha</p>
                <input type="password" class="input" placeholder="Senha" v-model="password">
                <button class="button is-success" @click="register">Cadastrar</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return {
            name: '',
            password: '',
            email: '',
            err: undefined
        }
    },
    methods: {
        register(){
            axios.post("http://localhost:8686/user", {
                name: this.name,
                password: this.password,
                email: this.email
            }).then(() => {
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

