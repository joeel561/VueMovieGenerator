<template>
    <button value='' @click='getResult'>Click</button>
    <div v-for='result in result' :key='result.id'>
        <p>{{result.title}}</p>
        <img v-bind:src="'http://image.tmdb.org/t/p/w500/' +    result.poster_path" width='100px'>
    </div>
</template>
<script>
    import axios from 'axios'
    export default {
        name: 'Base',
        data() {
            return {
                params: {
                    api_key: 'f4c26714ba3f4672f618f331893d064b',
                    with_genres: 27,
                    'vote_average.gte': 10,
                    'primary_release_date.gte': '2020-10-10'
                },
                URL: 'https://api.themoviedb.org/3/discover/movie',
                result: {}
               
            }
        },
        methods: {
            setFilter(name, value) {
                this.params[name] = value;
            },
            getResult() {
                axios.get(this.URL, {params:this.params })
                .then(response => {
                    this.result = response.data.results;
                        console.log(this.result);
                });
            }
        }
    }
</script>