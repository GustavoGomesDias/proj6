<template>
    <div>
        <h2>Edição de Usuário</h2>
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
                <button class="button is-success" @click="update">Editar</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    created(){
        const req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem("token")
            }
        };

        axios.get("http://localhost:8686/user/"+this.$route.params.id, req).then(res => {
            console.log(res);
            this.name = res.data.name;
            this.email = res.data.email;
            this.id = res.data.id;
        }).catch(err => {
            console.log("Entrou");
            console.log(err);
            this.$router.push({ name: "Users" });
        });
    },

    data(){
        return {
            name: '',
            email: '',
            id: -1,
            err: undefined
        }
    },

    methods: {
        update(){
            const req = {
                headers: {
                    Authorization: "Bearer " + localStorage.getItem("token")
                }
            };

            axios.put("http://localhost:8686/user", {
                name: this.name,
                email: this.email,
                id: this.id
            }, req).then(() => {
                this.$router.push({ name: 'Users' })
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

