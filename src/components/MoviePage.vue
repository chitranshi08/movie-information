<template>
    <div>
        <div class="informationContainer">
            <h1>Movie Information</h1>
            <input @input="hide" v-model="enterName" @keyup.enter="getValue" type="text" placeholder="Please enter movie name" /><br>
        </div>
        <div class="mainContainer">
            <img class="posterImage" :src="poster" alt="" />
            <div v-if="poster" class="container">
                <div class="rating"><strong>IMDB Rating - </strong>{{rating}}/10</div>
                <div class="released"><strong>Released - </strong>{{released}}</div>
                <div><strong>Language - </strong>{{language}}</div>
                <div class="genre"><strong>Genre - </strong>{{genre}}</div>
                <div class="plot"><strong>Plot - </strong>{{plot}}</div>
                
            </div>
        </div>
        <div v-if="showLoader" class="loader">
                    <img src="../assets/loader.gif" alt="">
                </div>
    </div>
</template>
<script>
export default {
    name: 'MoviePage',
    data: () => ({
        poster: null,
        enterName: null,
        rating: null,
        plot: null,
        released: null,
        errorMovie: false,
        showLoader: false,
        genre:null,
        language:null
    }),
    methods: {
        getValue: function() {
            var movie = this.enterName
            this.showLoader = true
            fetch(`http://www.omdbapi.com/?t=${movie}&apikey=51c54324`)
                .then((response) => { return response.json() })
                .then((response) => {
                    console.log(response)
                    this.poster = response.Poster
                    this.rating = response.imdbRating
                    this.released = response.Released
                    this.plot = response.Plot
                    this.genre = response.Genre
                    this.language = response.Language
                })
                .catch((err) => {
                    this.errorMovie = true
                })
                .finally(() => {
                    this.showLoader = false
                })
        },
        hide() {
            this.showLoader = false
            this.poster = false
        }
    }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
    color: red;
}

.mainContainer {
    display: flex;
    justify-content: space-between;
    margin-left: 50px;
    margin-right: 50px;
    margin-top: 20px;
    font-size: 20px;
}

.informationContainer {
    text-align: center;
}

.rating {
    color: #f2d564;
}
.released{
}


.loader {
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
    background-color: rgba(255, 255, 255, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;

}

input {
    font-size: 15px;
    padding: 10px;
    width: 200px;
}
.container{
  padding-left:25px;

}
.posterImage{
  width:40%;
}
.container > div{
margin-bottom:10px; 
}
strong{
  font-style: italic;
}

</style>