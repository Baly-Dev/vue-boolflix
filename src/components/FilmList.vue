<template>
    
    <section class="container">
        <div v-show="movies.length > 0" class="movies">
            <div class="header">
                <h3>Movies</h3>
            </div>
            <div class=" card-group">
                <MovieCard v-for="movie in movies" :key="movie.id" 
                :movie="movie"
                :configBaseUrl="configBaseUrl" 
                :configImageSize="configImageSize"
                />
            </div>
        </div>

        
        <div v-show="shows.length > 0" class="shows">
            <div class="header">
                <h3>Tv Shows</h3>
            </div>
            <div class=" card-group">
                <ShowCard v-for="show in shows" :key="show.id" 
                :show="show"
                :configBaseUrl="configBaseUrl" 
                :configImageSize="configImageSize"
                />
            </div>
        </div>
        
    </section>
</template>

<script>
import MovieCard from '@/components/MovieCard.vue'
import ShowCard from '@/components/ShowCard.vue'
export default {
    name: 'FilmList',
    props:{
        movies:Array,
        shows:Array,
        configBaseUrl: String,
        configImageSize: String
    },
    components:{
        MovieCard,
        ShowCard
    }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/global.scss';
section{
    overflow-y: auto;
    height: 95%;
    border-top: 5px solid $primary-dark;
    border-bottom: 5px solid $primary-dark;
    padding: 10px 0px;

    &::-webkit-scrollbar {
        display: none;
    }

    .movies{
        margin-bottom: 25px;
    }

    .header{
        padding: 0px 10px;

        h3{
            color: #fff;
            font-size: 1.3em;
        }
    }

    .card-group{
        display: flex;
        flex-wrap: wrap;

        .card{
            width: calc(100% / 4);
        }
    }
}

</style>