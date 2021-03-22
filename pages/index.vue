<template lang="html">
    <div class="container ">
        <h1 class="title">Álbums de la página</h1>
        <div class="columns is-multiline">
            <AlbumCard :album="album" v-for="album in albums" :key="album.id"/>

        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import env from "../config/env.js";
    import AlbumCard from "../components/AlbumCard";
    export default {
        name: 'IndexPage',
        components : {
            AlbumCard
        },
        data(){
            return {
                albums : []
            }
        },
        created(){
            axios.get(`${env.endpoint}/albums`).then(res => {
                this.albums = res.data
            })
        }
    }
</script>

<style scoped>

</style>