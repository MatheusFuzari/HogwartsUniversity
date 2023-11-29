<script setup>
    const {data:rolesFound} = await useFetch('http://localhost:8000/cargos')
</script>
<template>
    <main>
        <section>
            <h2>Cargos...</h2>
            <div v-for="(role, index) in rolesFound.data" :key="index">
                <p>Cargo: {{ role.nome }} -> Nivel: {{ role.nivelAcesso }}</p>
            </div>
        </section>
    </main>
</template>