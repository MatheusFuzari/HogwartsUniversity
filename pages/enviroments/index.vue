<script setup>
    const {data:enviromentsFound} = await useFetch('http://localhost:8000/ambientes',{
        key: 'pageLoad'
    });
    const btnPost = useState('btnPost', ()=> false);
    let enviromentName;
    const postEnviroment = async () => {
        console.log(enviromentName)
        await useFetch('http://localhost:8000/ambientes/',{
            method: 'POST',
            body: [{
                'nome':enviromentName,
            }],
            onResponse(){
                alert("Ambiente cadastrdo!");
                refreshNuxtData('pageLoad');
            },
            onRequestError(){
                alert("Erro ao cadastrar ambiente!");
            }
        })
    }
</script>

<template>
    <main>
        <section>
            <h2>Ambientes...</h2>
            <div v-for="(enviroment, index) in enviromentsFound.data" :key="index">
                <p>Nome: <span style="font-weight: 800;">{{ enviroment.nome }}</span></p>
            </div>
            <br><br>
            <button @click="()=>{btnPost = !btnPost}">Adicionar ambiente</button>
        </section>
        
        <section v-if="btnPost">
            <h4>Cadastrar novo ambiente...</h4>
            <br>
            <label>Nome do ambiente: <input type="text" v-model="enviromentName"></label>
            <br>
            <button @click="postEnviroment">Cadastrar!</button>
        </section>
    </main>
</template>