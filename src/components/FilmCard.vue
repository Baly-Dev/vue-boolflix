<template>
    <div class="card">
        <div class="card-header">
            <img class="cover" :src="configBaseUrl + configImageSize + film.poster_path" alt="">
        </div>
        <div class="card-body">
            <h3>{{film.title}}</h3>
            <p>{{film.original_title}}</p>

            <h3>{{film.name}}</h3>
            <p>{{film.original_name}}</p>

            <p>{{film.original_language}}</p>
            <p>{{film.vote_average}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCard',
    props:{
        film: Object,
        configBaseUrl: String,
        configImageSize: String
    },
    data(){
        return{
            imgPath: ''
        }
    }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/global.scss';
.card{
    padding: 10px;
    .cover{
        width: 100%;
    }
}
</style>