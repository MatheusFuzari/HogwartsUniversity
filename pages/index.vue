<script setup>
    definePageMeta({
        layout:'login'
    });
    const {data:usersFound} = await useFetch('http://localhost:8000/usuarios');
    const btnLogin = useState('btnLogin', () => '');
    console.log(btnLogin)
</script>
<template>
    <div>
        <section>
            <h2>Bem vindo, bruxo!</h2>
            <img style="height: 250px;" src="https://static3.tcdn.com.br/img/img_prod/460977/brasao_da_escola_hogwarts_harry_potter_the_noble_collection_22961_1_20201211173553.jpg">
        </section>
        <section>
            <select v-model="btnLogin">
                <option disabled value="" selected>Selecione o usuário!</option>
                <option v-for="(user, index) in usersFound.data" :key="index" :value="user.nome">
                    {{ user.email }}
                </option>
            </select>
        </section>
        <section v-if="btnLogin!=''">
            <NuxtLink :to="`/home/${btnLogin}`">
                <button>Entrar</button>
            </NuxtLink>
        </section>
    </div>
</template>