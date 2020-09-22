<template>
  <div>
      <div class="col-md-12 text-center mt-4">
        <h1 class="display-4">Movies</h1>
      </div>
      <div class="container">
          <b-card no-body>
            <b-tabs pills card>
                <b-tab title="Top Rated" active>
                    <b-card-text>
                        <div class="row">
                            <div class="col-md-3" v-for="(item, index) in topRatedMovies.results" :key="'top-rated-'+index">
                                <b-card
                                    :title="item.original_title"
                                    :img-src="imgPath + item.poster_path"
                                    :img-alt="item.original_title"
                                    @error="imageError"
                                    img-top
                                    class="mb-2"
                                >
                                    <b-card-text>
                                    <strong>Release Date:</strong> {{ item.release_date }}
                                    </b-card-text>

                                    <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
                                </b-card>
                            </div>
                        </div>
                        <div class="col-md-12">
                            <b-pagination
                            v-model="topratedCurrentPage"
                            :total-rows="topRatedMovies.total_results"
                            :per-page="per_page"
                            aria-controls="my-table"
                            ></b-pagination>
                        </div>
                    </b-card-text>
                </b-tab>
                <b-tab title="Upcoming">
                    <b-card-text>
                        <div class="row">
                            <div class="col-md-3" v-for="(item, index) in upcomingMovies.results" :key="'upcoming-movies-'+index">
                                <b-card
                                    :title="item.original_title"
                                    :img-src="imgPath + item.poster_path"
                                    :img-alt="item.original_title"
                                    @error="imageError"
                                    img-top
                                    class="mb-2"
                                >
                                    <b-card-text>
                                    <strong>Release Date:</strong> {{ item.release_date }}
                                    </b-card-text>

                                    <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
                                </b-card>
                            </div>
                        </div>
                        <div class="col-md-12">
                            <b-pagination
                            v-model="upcomingCurrentPage"
                            :total-rows="upcomingMovies.total_results"
                            :per-page="per_page"
                            aria-controls="my-table"
                            ></b-pagination>
                        </div>
                    </b-card-text>
                </b-tab>
            </b-tabs>
        </b-card>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Movies',
    data() {
        return {
            upcomingMovies: {},
            upcomingCurrentPage: 1,
            topRatedMovies: {},
            topratedCurrentPage: 1,
            upcomingError: {},
            topRatedError: {},
            baseUrl: '',
            apiKey: '',
            apiToken: '',
            imgPath: 'https://image.tmdb.org/t/p/w220_and_h330_face',
            per_page: 20,
            errImg: '',
        };
    },
    watch: {
        upcomingCurrentPage(val) {
            if (val != undefined && val != '' && val != null) {
                this.getUpcomingMovies(val);
            }
        },
        topratedCurrentPage(val) {
            if (val != undefined && val != '' && val != null) {
                this.getTopRatedMovies(val);
            }
        },
    },
    mounted() {
        this.apiKey = this.$store.state.apiKey;
        this.baseUrl = this.$store.state.baseUrl;
        this.apiToken = this.$store.state.apiToken;
        this.getUpcomingMovies();
        this.getTopRatedMovies();
        this.errImg = '../assets/no-image.jpg';
    },
    methods: {
        getUpcomingMovies(page=1) {
            let url = this.baseUrl + '/movie/upcoming?page=' + page + '&api_key=' + this.apiKey;
            axios.get(url)
            .then(res => {
                this.upcomingMovies = res.data;
            }).catch(err => {
                this.upcomingError = err.response.data;
            });
        },
        getTopRatedMovies(page) {
            let url = this.baseUrl + '/movie/top_rated?page=' + page + '&api_key=' + this.apiKey;
            axios.get(url)
            .then(res => {
                this.topRatedMovies = res.data;
            }).catch(err => {
                this.topRatedError = err.response.data;
            }); 
        },
        imageError(event) {
            console.log('error occured');
            event.target.src = this.errImg;
        }
    }
}
</script>
