<template>
    <div id="mi-componente">
        <hr/>
        <h1>{{titulo}}</h1>
        <h2>{{subtitulo}}</h2>
        <hr/>
    </div>
</template>

<script>

export default {
    name: 'MiComponente',
    data(){
        return {
            titulo: 'Este apartado va desde el nuevo componente',
            subtitulo : 'Este es el subtitulo del componente'
        }
    }
}
</script>
