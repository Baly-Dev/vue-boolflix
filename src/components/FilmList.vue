<template>
    <section class="container card-group">
        <FilmCard v-for="datum in data" :key="datum.id" 
        :datum="datum"
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
        data: Array,
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