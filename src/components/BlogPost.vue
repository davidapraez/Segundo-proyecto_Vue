<script setup>
import { defineProps } from "vue";


//defineProps(['title','id','body','colorText'])
defineProps({
    title: String,
    id: Number,
    body:{
        type: String,
        default: 'Sin descripcion',
    },
    colorText:String
})
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">
            {{id}} - {{title}}</h5>
            <p>{{body}}</p>
            <button @click="$emit('cambiarFavorito',title)"
             class="btn btn-outline-primary"> Favorito</button>
        </div>
    </div>
</template>