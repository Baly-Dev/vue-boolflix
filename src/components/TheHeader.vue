<template>
    <header>
        <nav class="container navbar">
            <div class="right">
                <a class="navbar-brand" href="#">Boolflix</a>
            </div>
            <div class="left">
                <FilmSearch @emitSearch="getSearchParameter"/>
            </div>
        </nav>
    </header>
</template>

<script>
import FilmSearch from '@/components/FilmSearch.vue'
export default{
    name: 'TheHeader',
    data(){
        return{
            searchParameter: null
        }
    },
    methods:{
        getSearchParameter(parameter){
            this.searchParameter = parameter
            this.emitSearchParameter()
        },
        emitSearchParameter(){
            this.$emit('emitSearch', this.searchParameter)
        }
    },
    components:{
        FilmSearch
    }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/global.scss';
header{
    height: 60px;
    display: flex;
    background-color: darkgray;
    

    nav{
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0px 10px;
    }
}
</style>