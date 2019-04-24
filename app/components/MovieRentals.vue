<template>
    <Page>
        <ActionBar :title="'Rentals for ' + movie_title" android:flat="true"/>
        <ListView for="customer in customers" class="list-group" style="height:100%">
            <v-template>
                <movie-rental-history :customer="customer"></movie-rental-history>
            </v-template>
        </ListView>
    </Page>
</template>
<script>
    function Customer ({id, name, email, pivot}) {
        this.id = parseInt(pivot.id)
        this.name = name
        this.email = email
        this.transaction = pivot
    }
    import axios from "axios";
    import MovieRentalHistory from '@/components/MovieRentalHistoryComponent.vue'

    export default {
        data() {
            return {
                movie_title: '',
                customers: []
            }
        },
        methods: {
            read() {
                let url = 'https://codeflare.tech/api/movies/' + this.id + '/rentals'
                axios.get(url).then(({data}) => {
                    this.movie_title = data[0].title;
                    console.log('Name is: ' + this.movie_title + '-------');
                    // console.log(data[0]);
                    data[0].customers.forEach(customer => {
                        this.customers.push(new Customer(customer))
                    });
                }, error => {
                    console.error(error);
                })
            }
        },
        components: {
            MovieRentalHistory
        },
        props: ['id'],
        created() {
            this.read()
        }
    }
</script>

<style scoped lang="scss">
</style>
