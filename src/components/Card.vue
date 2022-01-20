<template>
    <div class="col">
        <div class="item-card p-3">
            <img :src="image" :alt="title">
            <span>Title: {{title}}</span>
            <span>Original title: {{original}}</span>
            <span>Language: <i :class="'flag flag-' + getFlags(lang)"></i></span>
            <span>Vote: {{vote}}</span>
        </div>
        
    </div>
</template>

<script>
export default {
    name: "Card",
    props: [
        'title',
        'image',
        'original',
        'lang',
        'vote',
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
                default:
                    return lang;
            }

        }
    }
}

</script>

<style lang="scss">
@import "../assets/scss/style.scss";
.col {
    padding: 0.5em 1em;
    .item-card {
		display: flex;
		flex-direction: column;
		align-items: center;
		height: 100%;
        border: 1px solid black;
        img {
            width: 100%;
        }
        span {
            text-align: center;
        }
}
}

</style>