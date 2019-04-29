<template>
    <Page>
        <ActionBar title="Welcome to Yellow Bucket!" android:flat="true"/>
        <TabView tabBackgroundColor="#8AAAE5"
                 androidSelectedTabHighlightColor="#65580D"
                 tabTextColor="#ffffff"
                 selectedTabTextColor="#65580D">
            <TabViewItem title="Movies">
                <movie-component :movies="movies"></movie-component>
            </TabViewItem>
            <TabViewItem title="Customers">
                <customer-component :customers="customers"></customer-component>
            </TabViewItem>
            <TabViewItem title="About">
                <GridLayout columns="*" rows="*">
                    <Label class="message" text="About Yellow Bucket" col="0" row="0"/>
                </GridLayout>
            </TabViewItem>
        </TabView>
    </Page>
</template>

<script>
    import axios from "axios";
    import CustomerComponent from '@/components/CustomerComponent.vue';
    import MovieComponent from '@/components/MovieComponent.vue';
    function Customer({id, name, email, isAdmin}) {
        this.id = parseInt(id);
        this.name = name;
        this.email = email;
        this.isAdmin = isAdmin
    }
    function Movie({id, title,length, rating, description}) {
        this.id = parseInt(id);
        this.title = title;
        this.rating = rating;
        this.length = length + " mins";
        this.description = description;
    }

    export default {
        data() {
            return {
                customers: [],
                movies: [],
            }
        },
        methods: {
            onItemTap: function (args) {
                console.log("Item with index: " + args.index + " tapped");
            }
        },
        mounted() {
            axios.get("https://codeflare.tech/api/customers").then(result => {
                result.data.forEach(customer => {
                    console.log(customer.data);
                    this.customers.push(new Customer(customer));
                })
            },
                error => {
                console.error(error);
            }),
            axios.get("https://codeflare.tech/api/movies").then(result => {
                result.data.forEach(movie => {
                    console.log(movie.data);
                    this.movies.push(new Movie(movie));
                })
            }, error => {
                console.error(error);
            })
        },
        components: {
            MovieComponent,
            CustomerComponent,

        }
        /*movieMount() {
            axios.get("https://codeflare.tech/api/movies").then(result => {
                result.data.forEach(movie => {
                    console.log(movie.data);
                    this.movies.push(new Movie(movie));
                })
            }, error => {
                console.error(error);
            })
        },
        components: {
            MovieComponent,
            CustomerComponent,
        }*/
    }
</script>

<style scoped>
    ActionBar {
        background-color: #666666;
        color: #fafafa;
    }
    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #666666;
    }
    .label-text {
        color: #444444;
    }
</style>