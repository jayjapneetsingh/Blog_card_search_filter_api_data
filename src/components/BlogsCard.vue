<template>
    <div>


        <div class="wrap">
            <div class="search">
                <input type="text" class="searchTerm" placeholder="What are you looking for?" v-model="searchbar"
                    @click="artcilesdata()">
                <button type="submit" class="searchButton">
                    <i class="fa fa-search"></i>
                </button>
            </div>

        </div>

        <!-- 

GRADIENT BANNER DESIGN BY SIMON LURWER ON DRIBBBLE:
https://dribbble.com/shots/14101951-Banners

-->
        <div class="main-container">

            <div class="heading">
                <h1 class="heading__title">Gradient Banner Cards</h1>
                <p class="heading__credits"><a class="heading__link" target="_blank"
                        href="https://dribbble.com/sl">Design by Simon Lurwer on Dribbble</a></p>
            </div>

            <br>
            <div class="cards">
                <div class="card" v-for="content in filteredarticles" :key="content.title">
                    <img :src="content.urlToImage" class="recipe-image">
                    <div class="card__icon"><i class="fas fa-bolt"></i></div>
                    <p class="card__exit"><i class="fas fa-times"></i></p>
                    <a target="_blank" :href="content.url">Read More</a>

                    <h2 class="card__title">{{content.title}} hi</h2>
                    <p class="card__apply">
                        <a class="card__link" href="#">Apply Now <i class="fas fa-arrow-right"></i></a>
                    </p>
                </div>

            </div>
        </div>
        <!-- Card -->
    </div>
</template>
<script>
import axios from "axios";
export default {
    name: "BlogCard",



    data() {
        return {
            searchbar: null,
            articles: []
        }


    },
    methods: {
        async artcilesdata() {
            let result = await axios.get(`https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=ca7b8b07f01647a2a20dc31780387d53`)
            console.log(result.data.articles)
            let home = result.data.articles
            this.articles = home
            console.log(home, "home")


            //console.log(this.artcile,"home")

        }

    },
    computed: {
        filteredarticles() {
            let articledata = this.articles
            console.log(articledata, "hyya")

            if (this.searchbar != '' && this.searchbar) {
                articledata = articledata.filter((item) => {
                    return item.title
                        .toUpperCase()
                        .includes(this.searchbar.toUpperCase())
                })
            }
            return articledata
        }
    }


}

</script>

<style scoped>
@import url(https://fonts.googleapis.com/css?family=Open+Sans);

.card__title[data-v-4fb4197e] {
    grid-row: 3/4;
    font-weight: 400;
    color: black;
}

body {
    background: #f2f2f2;
    font-family: 'Open Sans', sans-serif;
}

.search {
    width: 100%;
    position: relative;
    display: flex;
}

.searchTerm {
    width: 100%;
    border: 3px solid #00B4CC;
    border-right: none;
    padding: 5px;
    height: 20px;
    border-radius: 5px 0 0 5px;
    outline: none;
    color: #9DBFAF;
}

.searchTerm:focus {
    color: #00B4CC;
}

.searchButton {
    width: 40px;
    height: 36px;
    border: 1px solid #00B4CC;
    background: #00B4CC;
    text-align: center;
    color: #fff;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
    font-size: 20px;
}

/*Resize the wrap to see the search bar change!*/
.wrap {
    width: 30%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
        Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}

.main-container {
    padding: 30px;
}

/* HEADING */

.heading {
    text-align: center;
}

.heading__title {
    font-weight: 600;
}

.heading__credits {
    margin: 10px 0px;
    color: #888888;
    font-size: 25px;
    transition: all 0.5s;
}

.heading__link {
    text-decoration: none;
}

.heading__credits .heading__link {
    color: inherit;
}

/* CARDS */

.cards {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}

.card {
    margin: 20px;
    padding: 20px;
    width: 500px;
    min-height: 200px;

    grid-template-rows: 20px 50px 1fr 50px;
    border-radius: 10px;
    box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.25);
    transition: all 0.2s;
}

.card:hover {
    box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.4);
    transform: scale(1.01);
}

.card__link,
.card__exit,
.card__icon {
    position: relative;
    text-decoration: none;
    color: rgba(255, 255, 255, 0.9);
}

.card__link::after {
    position: absolute;
    top: 25px;
    left: 0;
    content: "";
    width: 0%;
    height: 3px;
    background-color: rgba(255, 255, 255, 0.6);
    transition: all 0.5s;
}

.card__link:hover::after {
    width: 100%;
}

.card__exit {
    grid-row: 1/2;
    justify-self: end;
}

.card__icon {
    grid-row: 2/3;
    font-size: 30px;
}

.card__title {
    grid-row: 3/4;
    font-weight: 400;
    color: #ffffff;
}

.card__apply {
    grid-row: 4/5;
    align-self: center;
}

/* CARD BACKGROUNDS */

.card-1 {
    background: radial-gradient(#1fe4f5, #3fbafe);
}

.card-2 {
    background: radial-gradient(#fbc1cc, #fa99b2);
}

.card-3 {
    background: radial-gradient(#76b2fe, #b69efe);
}

.card-4 {
    background: radial-gradient(#60efbc, #58d5c9);
}

.card-5 {
    background: radial-gradient(#f588d8, #c0a3e5);
}

/* RESPONSIVE */

@media (max-width: 1600px) {
    .cards {
        justify-content: center;
    }
}

.search[data-v-4fb4197e] {
    /* width: 100%; */
    position: relative;
    display: flex;
    margin-top: -50px;
    height: 40px;
    width: 488px;
    align-items: center;

}

.searchTerm[data-v-4fb4197e] {
    width: 100%;
    border: 3px solid #00B4CC;
    border-right: none;
    padding: 5px;
    height: 30px;
    border-radius: 5px 0 0 5px;
    outline: none;
    color: #9DBFAF;
}

img,
svg {
    /* vertical-align: middle; */
    width: 310px;
    margin: auto;
    margin: auto !important;
}
</style>