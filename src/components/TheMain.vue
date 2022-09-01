<template>
    <main >
        <div class="header container">
            <h2 v-if="data.length > 1">Risultati ricerca</h2>
            <h2 v-else>Effettua una ricerca per ottenre i risultati</h2>
            <span class="tag">{{data.length}}</span>
        </div>
        <FilmList 
        :data="data"
        :configBaseUrl="configBaseUrl"
        :configImageSize="configImageSize"
        />
    </main>
</template>

<script>
import FilmList from '@/components/FilmList.vue'
export default{
    name: 'TheMain',
    props: {
        data: Array,
        configBaseUrl: String,
        configImageSize: String
    },
    components:{
        FilmList
    }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/global.scss';
main{
    padding: 60px 0px;
    background-color: $primary-normal;
    .header{
        padding: 0px 10px;
        display: flex;
        align-items: center;
        margin-bottom: 15px;

        h2{
            color: #fff;
            font-size: 1.3em;
        }

        .tag{
            padding: 2px 10px;
            border-radius: 6px;
            background-color: $primary-dark;
            color: #fff;
            font-weight: 600;
            margin-left: auto;
        }
    }
}
</style>