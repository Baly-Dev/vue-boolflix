<template>
    <div class="card">
        <div class="card-header">
            <img v-if="datum.poster_path == null" class="cover" src="https://fakeimg.pl/500x700/262626/" alt="">
            <img v-else class="cover" :src="configBaseUrl + configImageSize + datum.poster_path" alt="">
            <div class="overlay">
                <h4>Overview</h4>
                <p v-if="datum.overview != ''">{{datum.overview}}</p>
                <p v-else>Overview non disponibile</p>
            </div>
        </div>
        <div class="card-body">
            <div class="main-info">
                <div v-show="datum.type == 'movie'">
                    <h3>{{datum.title}}</h3>
                    <p>{{datum.original_title}}</p>
                </div>
                <div v-show="datum.type == 'show'">
                    <h3>{{datum.name}}</h3>
                    <p>{{datum.original_name}}</p>
                </div>
            </div>
            <div class="meta-info">
                <div>
                    <i v-for="(fill, i) in rankingPoint" :key="i" class="fa-solid fill fa-star"></i>
                <i v-show="reminder.length > 0" v-for="(empty, i) in reminder" :key="i" class="fa-solid empty fa-star"></i>
                </div>
                <span :class="'fi fi-' + datum.original_language"></span>
            </div>
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

    .card-header{
        border: 2px solid $primary-dark;
        margin-bottom: 5px;
        height: 350px;
        border-radius: 6px;
        position: relative;
        cursor: pointer;

        .overlay{
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            z-index: 1;
            background-color: rgba(0,0,0,0.8);
            display: none;
            padding: 10px;
            color: #fff;

            h4{
                margin-bottom: 5px;
            }
            p{
                font-size: 0.8em;
                line-height: 1.3em;
            }
        }

        &:hover .overlay{
            display: block;
        }

        .cover{
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: top;
        border-radius: 4px;
        }
    }

    .card-body{
        padding: 10px;
        background-color: $primary-dark;
        border-radius: 6px;
        
        .main-info{
            color: #fff;
            margin-bottom: 10px;
            h3{
                font-size: 1em;
                margin-bottom: 5px;
            }
            p{
                font-size: 0.5em
            }
        }
    }

    .meta-info{
        display: flex;
        justify-content: space-between;
    }

    .empty{
    color: rgb(202, 202, 202);
    }

    .fill{
        color: rgb(234, 222, 2);
    }

    span{
        font-size: 0.7em;
    }
}
</style>