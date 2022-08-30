<template>
    <div class="card">
        <div class="card-header">
            <img class="cover" :src="configBaseUrl + configImageSize + film.poster_path" alt="">
        </div>
        <div class="card-body">
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
    .cover{
        width: 100%;
    }
}
</style>