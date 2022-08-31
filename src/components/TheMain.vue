<template>
    <main class="">
        <FilmList 
        :data="data"
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
        data: Array,
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
main{
    padding: 20px 0px;
}
</style>