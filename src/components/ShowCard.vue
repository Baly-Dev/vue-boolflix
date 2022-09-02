<template>
    <div class="card">
        <div class="card-header">
            <img v-if="show.poster_path == null" class="cover" src="https://fakeimg.pl/500x700/262626/" alt="">
            <img v-else class="cover" :src="configBaseUrl + configImageSize + show.poster_path" alt="">
            <div class="overlay">
                <div class="header">
                    <h3>{{show.name}}</h3>
                </div>
                <div class="body">
                    <h4>Overview</h4>
                    <p v-if="show.overview != ''">{{overview}}</p>
                    <p v-else>Overview non disponibile</p>
                </div>
            </div>
        </div>
        <div class="card-body">
            <div class="main-info">
                <div v-show="show.type == 'show'">
                    <h3>{{name}}</h3>
                    <p>{{show.original_name}}</p>
                </div>
            </div>
            <div class="meta-info">
                <div>
                    <i v-for="(fill, i) in rankingPoint" :key="i" class="fa-solid fill fa-star"></i>
                    <i v-show="reminder.length > 0" v-for="(empty, i) in reminder" :key="i + rankingPoint.length" class="fa-solid empty fa-star"></i>
                </div>
                <span :class="'fi fi-' + show.original_language"></span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCard',
    props:{
        show: Object,
        configBaseUrl: String,
        configImageSize: String
    },
    data(){
        return{
            rankingPoint: [],
            reminder: [],
            overview: null,
            name: null
        }
    },
    created(){
        this.overview = this.getExcerpt(this.show.overview, 30)
        this.name = this.getExcerpt(this.show.name, 4)
        this.getRanking()
    },
    methods:{
        getRanking(){
            const ranking = Math.ceil(this.show.vote_average / 2)
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