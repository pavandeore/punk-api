<template>
        <div v-for="beer in Beers" :key="beer.id" id="beer-compo" >
            <div id="each-beer">
                <h3>Beer No : {{beer.id}} </h3>
                <h3>Name : {{beer.name}} </h3>
                <h3>Tag : {{beer.tagline}} </h3>
                <h3>ABV : {{beer.abv}} </h3>
                <h3>Attenuation Level : {{beer.attenuation_level}} </h3>
                <img class="beer-img" :src="beer.image_url" />
            </div>
        </div>    
</template>

<script>
import axios from 'axios';

export default {
    name: 'BeerComponent',
    created(){
        this.getBeers()
    },
    data(){
        return{
            Beers : [],
            errorMsg: ''
        }
    },
    methods: {
        async getBeers(){
            const response  = await axios.get('https://api.punkapi.com/v2/beers')
            const data = await response;
            
            this.Beers = data.data; 
        }
    }
}
</script>

<style scoped>
#beer-compo{
    width:290px;
    background-color: darkcyan;
    color: #fff;
    margin:10px;
    padding:13px;
}
#each-beer > h3{
    margin-top:15px;
}
.beer-img{
    height:220px;
    margin-top:15px;
    position: relative;
    left:50%;
    transform: translateX(-50%);
}

</style>