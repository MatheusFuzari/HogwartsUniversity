<script setup>
    const route = useRoute()
</script>
<template>
    <main>
        <div>
            <h2>Bem-vindo, {{ route.params.name }}</h2>
        </div>
    </main>
</template>