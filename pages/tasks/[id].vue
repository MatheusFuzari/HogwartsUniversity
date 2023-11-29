<script setup>
    const route = useRoute();
    let {data:taskFound} = await useFetch(`http://localhost:8000/tarefas/${route.params.id}`);
    taskFound = taskFound._rawValue.data;
    const {data:workersFound} = await useFetch(`http://localhost:8000/tarefasUsuarios?tarefa=${taskFound.id}`);
    const {data:tarefaStatusFound} = await useFetch(`http://localhost:8000/tarefasStatus?tarefa=${taskFound.id}`)
    const transformData = (date) => {
        if(date===null){
            return "Sem data!";
        }
        let dateN = new Date(date);
        console.log(dateN)
        const month = dateN.toLocaleString('pt-Br', { month : 'long'});
        let strDate = dateN.getDay()+" de "+month+" de "+dateN.getFullYear()+" às "+dateN.getHours()+":"+dateN.getMinutes();
        return strDate;
    }
    console.log(taskFound.dataFim)
</script>
<template>
    <main>
        <section>
            <h2>Sobre a tarefa...</h2>
            <p>Nome: {{ taskFound.nome }}</p>
            <p>Status: {{ taskFound.idStatusFK.nome }}</p>
            <p>Ambiente: {{ taskFound.idAmbienteFK.nome }}</p>
            <p>Prazo: {{ transformData(taskFound.prazo) }}</p>
            <p>Data de início: {{ transformData(taskFound.dataInicio) }}</p>
            <p>Data de entrega: {{ transformData(taskFound.dataFim) }}</p>
            <p>Descrição: {{ taskFound.descricao }}</p>
            <h2>Solicitante...</h2>
            <p>Nome: {{ taskFound.idSolicitanteFK.nome }}</p>
            <img :src="taskFound.idSolicitanteFK.image" style="height: 150px;">
        </section>
        <hr>
        <section>
            <h2>Responsáveis pela tarefa...</h2>
            <div v-for="(worker, index) in workersFound.data" :key="index">
                <p>Nome: {{ worker.idUsuarioFK.nome }}</p>
                <img :src="worker.idUsuarioFK.image" style="height: 150px;">
            </div>
        </section>
        <hr>
        <section>
            <h2>Andamento da tarefa...</h2>
            <div v-for="(status, index) in tarefaStatusFound.data" :key="index">
                <p>{{ status.idStatusFK.nome }} em {{ transformData(status.data) }}</p>
            </div>
        </section>
    </main>
</template>