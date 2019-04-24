<template>
    <GridLayout columns="*, *" rows="auto" width="100%">
        <Label @onTap="onTap" :text="movie.title" row="0" col="0" class="list-group-item-heading label-text"
               style="width: 60%"/>
        <Label @onTap="onTap" :text="movie.length" row="0" col="1" class="list-group-item-heading label-text"
               style="width: 60%"/>
    </GridLayout>
</template>

<script>
    import MovieRentals from '@/components/MovieRentals';
    export default {
        data() {
            return {}
        },
        methods: {
            onTap: function () {
                // console.log("Item with name: " + this.customer.name + " tapped");
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
        movieMount() {
        }
    }
</script>

<style scoped>
    .label-text {
        font-size: 14;
        color: #444444;
    }
</style>
