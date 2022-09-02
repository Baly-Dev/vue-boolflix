<template>
    <main>
        <div class="header container">
            <h2 v-if="movies.length > 0 || shows.length > 0">Risultati ricerca</h2>
            <h2 v-else>Effettua una ricerca per ottenre i risultati</h2>
            <!--<span class="tag">{{movie.length}}</span>-->
        </div>
        <FilmList 
        :movies="movies"
        :shows="shows"
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
        movies:Array,
        shows:Array,
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
    height: calc(100vh - (60px + 40px));
    .header{
        padding: 0px 10px;
        display: flex;
        align-items: center;
        margin-bottom: 15px;

        h2{
            color: #fff;
            font-size: 1.6em;
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