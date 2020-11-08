<template>
 <div class="image-flip">
    <div class="mainflip">
        <div class="frontside">
            <div class="card">
                <div class="card-body text-center">
                    <p v-if="persona.picture !== null">
                        <img class="img-fluid" :src="persona.picture" alt="card image">
                    </p>
                    <p v-else>
                        <img class="img-fluid" src="https://lh3.googleusercontent.com/proxy/KcngInzQbFBvFcGfJWnlg9PHPG0Yc3fZGzEiJeIXFbb3LRsEwYCRrr9y1MyO0KiQldv8GoPn6Z5oRfZTB2uaT32vqtkxw6U" alt="card image">
                    </p>
                    <h4 class="card-title">{{persona.name}}<br/><small>@{{persona.username}}</small></h4>                    
                    <p class="card-text">{{persona.professionalHeadline}}</p>
                    <p class="card-text">{{persona.locationName}}</p>
                    <a :href="`https://bio.torre.co/es/${persona.username}`" class="btn btn-primary mb-4" target="_blank">Ver perfil</a>
                </div>
            </div>
        </div>
        
    </div>
</div>
</template>

<script>

export default {
  name: 'Card',
  props: {
    datos: Object
  },
  data() {
    return {
        persona:this.datos
    };
  },
  methods:{
   
  },
  created: function() {
    console.log(this.datos)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.btn-primary:hover,
.btn-primary:focus {
    background-color: #108d6f;
    border-color: #108d6f;
    box-shadow: none;
    outline: none;
}

.btn-primary {
    color: #fff;
    background-color: #007b5e;
    border-color: #007b5e;
}


.mainflip {
    -webkit-transition: 1s;
    -webkit-transform-style: preserve-3d;
    -ms-transition: 1s;
    -moz-transition: 1s;
    -moz-transform: perspective(1000px);
    -moz-transform-style: preserve-3d;
    -ms-transform-style: preserve-3d;
    transition: 1s;
    transform-style: preserve-3d;
    position: relative;
    height: 54vh;
    min-height: 50vh;
    overflow: hidden;
    font-size: 14px;
}

.frontside {
    position: relative;
    -webkit-transform: rotateY(0deg);
    -ms-transform: rotateY(0deg);
    z-index: 2;
    margin-bottom: 30px;
}

.frontside,
.backside {
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    -ms-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-transition: 1s;
    -webkit-transform-style: preserve-3d;
    -moz-transition: 1s;
    -moz-transform-style: preserve-3d;
    -o-transition: 1s;
    -o-transform-style: preserve-3d;
    -ms-transition: 1s;
    -ms-transform-style: preserve-3d;
    transition: 1s;
    transform-style: preserve-3d;
}

.frontside .card,
.backside .card {
    min-height: 312px;
}

.backside .card a {
    font-size: 18px;
    color: #007b5e !important;
}

.frontside .card .card-title,
.backside .card .card-title {
    color: #007b5e !important;
}

.frontside .card .card-body img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
}

h4{
    small{
        font-size: 12px;
    }
}

ul{ 
    &.skills{
        font-size: 12px;
        display: flex;
        flex-wrap: wrap;   
        li{
            list-style: none;
            padding: 0;
        }     
    }

}

</style>
