<script setup>
    const {data:tasksFound} = await useFetch('http://localhost:8000/tarefas?all');
    const transformData = (date) => {
        if(date===null){
            return "Sem data!";
        }
        let dateN = new Date(date);
        const month = dateN.toLocaleString('pt-Br', { month : 'long'});
        let strDate = dateN.getDay()+" de "+month+" de "+dateN.getFullYear();
        return strDate;
    }
</script>
<template>
    <main>
        <h2>Tarefas: </h2>
        <div v-for="(task, index) in tasksFound.data" :key='index'>
            <p>Nome: {{ task.nome }}</p>
            <p>Status: {{ task.idStatusFK.nome }}</p>
            <p>Ambiente: {{ task.idAmbienteFK.nome }}</p>
            <p>Prazo final: {{ transformData(task.prazo) }}</p>
            <nuxt-link :to="`tasks/${task.id}`"><button>Ver detalhes...</button></nuxt-link>
            <br><hr>
        </div>
    </main>
</template>