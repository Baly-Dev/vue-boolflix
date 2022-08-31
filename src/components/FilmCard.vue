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
                <p>{{datum.type}}</p>
                
                <i v-for="(fill, i) in rankingPoint" :key="i" class="fa-solid fill fa-star"></i>
                <i v-show="reminder.length > 0" v-for="(empty, i) in reminder" :key="i" class="fa-solid empty fa-star"></i>
                
                
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
    },
    data(){
        return{
            rankingPoint: [],
            reminder: []
        }
    },
    created(){
        console.log(this.getRanking())
    },
    methods:{
        getRanking(){
            const ranking = Math.ceil(this.datum.vote_average / 2)
            for(let i = 0; i < ranking; i++){
                this.rankingPoint.push(i)
            }
            const reminderTrack = 5 - this.rankingPoint.length
            for(let i = 0; i < reminderTrack; i++){
                this.reminder.push(i)
            }
            
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

.empty{
    color: rgb(202, 202, 202);
}

.fill{
    color: rgb(234, 222, 2);
}
</style>