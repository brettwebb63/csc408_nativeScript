<template>
    <FlexboxLayout flexDirection="row" class="list-group-item">
        <GridLayout columns="4*,6*" rows="*,*,*,*" width="100%" >
            <Image @onTap="onTap" :src="imageUrl" row="0" col="0" rowSpan="4"  class="thumbnail" style="padding-right: 20px"/>

            <Label @onTap="onTap" :text="movie.title" row="0" col="1" class="list-group-item-heading label-text" style="text-align: center"/>
            <Label @onTap="onTap" :text="movie.rating" row="1" col="1" class="list-group-item-heading label-text" style="text-align: center"/>
            <Label @onTap="onTap" :text="movie.length" row="2" col="1" class="list-group-item-heading label-text"style="text-align: center"/>
            <Label @onTap="onTap" :text="movie.description" row="3" col="1" class="list-group-item-heading label-text"/>
        </GridLayout>
    </FlexboxLayout>
</template>

<script>
    import MovieRentals from '@/components/MovieRentals';
    export default {
        data() {
            return {}
        },
        computed: {
            /* Build URL for image */
            imageUrl: function(){
                return "https://codeflare.tech/images/movie_" + this.movie.id + ".jpg";
            }
        },
        methods: {
            onTap: function () {
                console.log("Item with name: " + this.movie.title + " tapped");
                this.$navigateTo(MovieRentals, {
                    props: {
                        id: this.movie.id
                    }
                });
            }
        },
        props: ['movie'],
        components: {
            MovieRentals
        },
        mounted() {
        }
    }
</script>

<style scoped>
    .label-text {
        font-size: 14;
        color: #444444;
    }
</style>
