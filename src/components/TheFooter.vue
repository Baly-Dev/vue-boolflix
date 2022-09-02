<template>
    <footer>
        <div class="container pagination">
            <a @click.prevent="decreasePage()" class="prev" href="">Prev</a>
            <a @click.prevent="increasePage()" class="next" href="">Next</a>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'TehFooter',
    props:{
        moviesPages: Object,
        showsPages: Object
    },
    data(){
        return{
            page: 1
        }
    },
    methods:{
        increasePage(){
            if (this.moviesPages.total_pages > this.showsPages.total_pages){
                if(this.page < this.moviesPages.total_pages){
                    this.page++
                }
            }else{
                if(this.page < this.showsPages.total_pages){
                    this.page++
                }
            }
    
            this.$emit('nextPage', this.page)
        },
        decreasePage(){
            if(this.page > 1){
                this.page--
            }
            this.$emit('prevPage', this.page)
        }
    }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/global.scss';

footer{
    height: 40px;
    background-color: $primary-dark;
    .pagination{
        height: 100%;
        padding: 0px 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        a, p{
            color: #fff;
            text-decoration: none;
        }
    }
}
</style>