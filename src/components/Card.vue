<template>
    <div class="col">
        <div class="item-card">
            <div class="img-container m-3">
                <img v-if="poster" :src="image" :alt="title">
                <img v-else src="https://cdn.download.it/ms/static/images/poster-placeholder.png" :alt="title">
            </div>
            <div class="hover">
                <div class="text d-flex justify-content-between align-items-center">
                    <div class="first-title">
                        <span class="title mb-2">{{title}}</span>
                    </div>
                    <div v-show="title !== original" class="original-title mb-2">
                        <span>Titolo originale</span>
                        <span class="subtitle">{{original}}</span>
                    </div>
                    <div v-if="!clickMore" class="plot">
                        <p>{{plot}}</p>
                    </div>
                    <div v-if="clickMore" class="cast mt-2">
                        <span>Cast:</span>
                        <span v-for="(actor, index) in getCast(id)" :key="index">{{actor}}</span>
                    </div>
                    <span class="mb-2">Language: <i :class="'flag flag-' + getFlags(lang)"></i></span>
                    <div class="vote">
                        <span class="d-block">Vote {{getVote(vote)}}</span>
                        <div class="d-flex justify-content-center">
                            <i v-for="(star, index) in getVote(vote)" :key="index+'piene'" class="bi-star-fill"></i>
                            <i v-for="(star, index) in (5 - getVote(vote))" :key="index+'vuote'" class="bi-star"></i>
                        </div>
                    </div>
                    <div class="cast-title mt-2" @click="clickMore = !clickMore">
                        <span>Clicca qui per vedere più info</span>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios';


export default {
    name: "Card",
    props: [
        'title',
        'image',
        'original',
        'lang',
        'vote',
        'poster',
        'plot',
        'id',
        'type',
    ],
    data(){
        return {
            cast: [],
            api_key: '4148b7accd7bd65952002b841924594e',
            query: 'https://api.themoviedb.org/3/',
            clickMore: false,
        }
    },
    methods: {
        getFlags(lang){
            switch (lang){
                case 'en':
                    return 'us';
                case 'ko':
                    return 'kr';
                case 'ja':
                    return 'jp';
                case 'ur':
                    return 'pk';
                case 'zh':
                    return 'cn';
                case 'hi':
                    return 'in';
                default:
                    return lang;
            }
        },
        getVote(vote){
            let finalVote = parseFloat(vote) / 2;
            return Math.round(finalVote);
        },
        getCast(id){
			const parameters = {
				api_key: this.api_key,
			};
            axios.get(`${this.query}${this.type}/${id}/credits`, { params: parameters })
            .then((result) => {
                const castList = result.data.cast;
                this.cast = [];
                if (castList.length > 0){
                    for(let i = 0; i < 5; i++) {
                    this.cast.push(castList[i].name);
                    }
                } else {
                    console.log('nessun cast');
                }
            })
            .catch((error) => {
                console.log(error);
            })
            
            return this.cast;
        }
    }
}

</script>

<style lang="scss">
@import "../assets/scss/style.scss";
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.7.2/font/bootstrap-icons.css");

.col {
    padding: 0.5em 1em;
    .item-card {
        position: relative;
        color: white;
        text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		height: 100%;
        border: 1px solid white;
        .img-container {
            height: 300px;
            overflow: hidden;
            img {
            height: 100%;
            width: 100%;
            }
        }
        .hover {
            display: none;
            position: absolute;
            background-color: $hoverBackground;
            opacity: 0.9;
            height: 100%;
            width: 100%;
            cursor: pointer;
            .text {
                overflow: auto;
                height: 100%;
                padding: 0.5em;
                opacity: 1;
                flex-direction: column;
                .cast-title {
                    color: #54d1ff;
                    cursor: pointer;
                }
                .plot, .cast {
                    font-size: 0.8em;
                }
                span {
                    font-size: 0.9em;
                    display: block;
                }
                .title {
                    font-size: 1.1em;
                    }
                .subtitle {
                    font-size: 1em;
                }
            }
        }
    }
    .item-card:hover .hover {
        display: block;
    }
}

</style>