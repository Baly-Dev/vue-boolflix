<template>
    <div class="card">
        <div class="card-header">
            <img class="cover" :src="configBaseUrl + configImageSize + datum.poster_path" alt="">
        </div>
        <div class="card-body">
            <div class="title">
                <h3>{{datum.title}}</h3>
                <p>{{datum.original_title}}</p>

                <h3>{{datum.name}}</h3>
                <p>{{datum.original_name}}</p>
            </div>
            <div class="meta">
                <p>{{datum.vote_average}}</p>
                <p>{{datum.type}}</p>
            </div>
            <span :class="'fi fi-' + datum.original_language"></span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCard',
    props:{
        datum: Object,
        configBaseUrl: String,
        configImageSize: String
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