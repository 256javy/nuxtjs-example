<template>
    <div class="container">
        <h1 class="title">{{album.title}}</h1>
        <nuxt-link to="/">Atrás</nuxt-link>
        <div class="columns is-multiline">
            <div class="column is-one-quarter"
                v-for="photo in photos" :key = photo.id >
                <img :src="photo.url" :alt="photo.title">
            </div>
        </div>
    </div>
</template>

<script>
import router from "vue-router";
import axios from 'axios';
import env from '../../config/env.js';
    export default {
        name : 'AlbumIndividualPage',
        data(){
            return {
                album : {},
                photos : []
            }
        },
        created: async function() {
            const albumId = this.$route.params.id;
            const albumRes = await axios.get(`${env.endpoint}/albums/${albumId}`);
            this.album = albumRes.data;
            const photosRes = await axios.get(`${env.endpoint}/albums/${albumId}/photos`);
            this.photos = photosRes.data;
            
        }
    }
</script>

<style scoped>
    .container{text-align: center;}
    h1{margin-top: 100p;}
</style>