<template>
    <h1>Painel Adm</h1>

    <table class="table">
        <thead>
            <tr>
                <th>Nome</th>
                <th>E-mail</th>
                <th>Cargo</th>
                <th>Ações</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="user in users" :key="user.id">
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>
                <td>{{ processRole(user.role) }}</td>
                <td>
                    <button class="button is-success">Editar</button>|<button class="button is-danger">Deletar</button>
                </td>
            </tr>
        </tbody>

    </table>

</template>

<script>
import axios from 'axios';

export default {
    // created é gerado assim que carrega a página
    created(){
        const req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem("token")
            }
        }
        
        axios.get("http://localhost:8686/user", req).then(res => {
            console.log(res);
            this.users = res.data;
        }).catch(err => console.log(err))
    },
    data(){
        return {
            users: []
        }
    },
    methods: {
        processRole: function(value){
            if(value == 0){
                return "Usuário comum";
            }else if(value == 1){
                return "Admin";
            }
        }
    }
}

</script>


<style scoped>

</style>