<template>
    <div class="inputbox">
        <input v-model="searchParameter" @keyup.enter="emitSearchParameter" class="search-input" type="text" placeholder="Search">
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
@import '@/assets/scss/global.scss';

.inputbox{
    input{
        padding: 8px 12px;
        border-top-left-radius: 6px;
        border-bottom-left-radius: 6px;
        border: 3px solid $primary-light;

        &:focus,
        &:active{
            outline: none;
            border-color: $primary-light;
        }
    }

    button{
        padding: 8px 12px;
        border-top-right-radius: 6px;
        border-bottom-right-radius: 6px;
        border: 3px solid $primary-light;
        background-color: $primary-light;
        color: #fff;
        cursor: pointer;
    }

    button:hover{
        background-color: $primary-normal;
        border-top-right-radius: 6px;
        border-bottom-right-radius: 6px;
    }
}
</style>