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
                    <div class="plot">
                        <p>{{plot}}</p>
                    </div>
                    <span class="mb-2">Language: <i :class="'flag flag-' + getFlags(lang)"></i></span>
                    <span>Vote: {{getVote(vote)}}</span>
                    <div class="d-flex justify-content-center">
                        <i v-for="(star, index) in getVote(vote)" :key="index+'piene'" class="fas fa-star"></i>
                        <i v-for="(star, index) in (5 - getVote(vote))" :key="index+'vuote'" class="far fa-star"></i>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import '@fortawesome/fontawesome-free/css/all.css';

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
    ],
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
        }
    }
}

</script>

<style lang="scss">
@import "../assets/scss/style.scss";
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
            }
        }
        .hover {
            display: none;
            position: absolute;
            background-color: $hoverBackground;
            opacity: 0.9;
            height: 100%;
            width: 100%;
            .text {
                overflow: auto;
                height: 100%;
                padding: 0.5em;
                opacity: 1;
                flex-direction: column;
                .plot {
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