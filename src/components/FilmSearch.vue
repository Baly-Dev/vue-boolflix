<template>
    <div class="">
        <input type="text" v-model="searchParameter">
        <button @click="emitSearchParameter" class="btn">Search</button>
    </div>
</template>

<script>
    export default {
        name: 'FilmSearch',
        data(){
            return{
                searchParameter: null
            }
        },
        methods:{
            emitSearchParameter(){
                this.$emit('emitSearch', this.searchParameter)
            }
        }
    }
</script>

<style scoped lang="scss">

</style>