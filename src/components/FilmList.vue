<template>
    <section class="container card-group">
        <FilmCard v-for="film in all" :key="film.id" 
        :film="film"
        :configBaseUrl="configBaseUrl" 
        :configImageSize="configImageSize"
        />
    </section>
</template>

<script>
import FilmCard from '@/components/FilmCard.vue'
export default {
    name: 'FilmList',
    props:{
        all: Array,
        configBaseUrl: String,
        configImageSize: String
    },
    components:{
        FilmCard
    }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/global.scss';

.card-group{
    display: flex;
    flex-wrap: wrap;

    .card{
        width: calc(100% / 4);
    }
}
</style>