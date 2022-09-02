<template>
    <div class="card">
        <div class="card-header">
            <img v-if="movie.poster_path == null" class="cover" src="https://fakeimg.pl/500x700/262626/" alt="">
            <img v-else class="cover" :src="configBaseUrl + configImageSize + movie.poster_path" alt="">
            <div class="overlay">
                <div class="header">
                    <h3>{{movie.title}}</h3>
                </div>
                <div class="body">
                    <h4>Overview</h4>
                    <p v-if="movie.overview != ''">{{overview}}</p>
                    <p v-else>Overview non disponibile</p>
                </div>
                
            </div>
        </div>
        <div class="card-body">
            <div class="main-info">
                <div v-show="movie.type == 'movie'">
                    <h3>{{title}}</h3>
                    <p>{{movie.original_title}}</p>
                </div>
            </div>
            <div class="meta-info">
                <div>
                    <i v-for="(fill, i) in rankingPoint" :key="i" class="fa-solid fill fa-star"></i>
                    <i v-show="reminder.length > 0" v-for="(empty, i) in reminder" :key="i + rankingPoint.length" class="fa-solid empty fa-star"></i>
                </div>
                <span :class="'fi fi-' + movie.original_language"></span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCard',
    props:{
        movie: Object,
        configBaseUrl: String,
        configImageSize: String
    },
    data(){
        return{
            rankingPoint: [],
            reminder: [],
            overview: null,
            title: null
        }
    },
    created(){
        // content, chars
        this.overview = this.getExcerpt(this.movie.overview, 30)
        this.title = this.getExcerpt(this.movie.title, 4)
        this.getRanking()
    },
    methods:{
        getRanking(){
            const ranking = Math.ceil(this.movie.vote_average / 2)
            for(let i = 0; i < ranking; i++){
                this.rankingPoint.push(i)
            }
            const reminderTrack = 5 - this.rankingPoint.length
            for(let i = 0; i < reminderTrack; i++){
                this.reminder.push(i)
            }
        },
        getExcerpt(content, chars){
            const words = content.split(' ')

            if(words.length > chars){
                words.splice(chars, words.length - chars)
                return words.join(' ') + ' ...'
            }else{
                return words.join(' ')
            }
        }
    }
}
</script>
<style scoped lang="scss">
@import '@/assets/scss/global.scss';
@import '@/assets/scss/card.scss';
</style>