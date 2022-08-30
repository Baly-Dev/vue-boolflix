<template>
    <main class="">
        <FilmList 
        :all="all" 
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
        all: Array,
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
</style>