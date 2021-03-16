<template>
        <input class="input" type="text" v-model="search" placeholder="search beers"/>
        <div v-for="beer in Beers" :key="beer.id" id="beer-compo" >
            <div id="each-beer">
                <h3><label>Beer No : </label>{{beer.id}} </h3>
                <h3><label>Name : </label>{{beer.name}} </h3>
                <h3><label>Tag : </label>{{beer.tagline}} </h3>
                <h3><label>ABV : </label>{{beer.abv}} </h3>
                <h3><label>Attenuation Level : </label>{{beer.attenuation_level}} </h3>
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
.input{
    position: absolute;
}
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
#each-beer > h3 > label{
    color: rgb(53, 54, 48);
}
.beer-img{
    height:220px;
    margin-top:15px;
    position: relative;
    left:50%;
    transform: translateX(-50%);
}

</style>