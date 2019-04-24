<template>
    <ListView for="movie in movies" class="list-group" style="height:1250px">
        <v-template>
            <FlexboxLayout flexDirection="row" class="list-group-item">
                <movie-details :movie="movie"></movie-details>
            </FlexboxLayout>
        </v-template>
    </ListView>
</template>

<script>
    import MovieDetails from '@/components/MovieDetails.vue';
    export default {
        data() {
            return {}
        },
        methods: {
            onNameTap: function (args) {
                console.log("Item with id: " + args.item.id + " tapped");
                // console.log(args);
            }
        },
        props: ['movies'],
        components: {
            MovieDetails
        },
        movieMount() {
        }
    }
</script>

<style scoped>
    .label-text {
        color: #444444;
    }
</style>
