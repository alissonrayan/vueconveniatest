<template>
  
  <div class="bottom-bar">
    
    <div class="bottom-bar__carrousel">
      <div class="bottom-bar__carrousel__text">
        <p>Parceiros</p>
      </div>
      <div class="bottom-bar__carrousel__slider">
       <carousel :perPageCustom = "[[576, 2], [768, 3], [992, 4], [1200, 5]]" :navigationEnabled="true" :paginationEnabled="false" navigationNextLabel="<div class='arrow arrow--next'></div>" navigationPrevLabel="<div class='arrow arrow--prev'></div>">
            <slide v-for="pic in pics">
              <img :src="pic.image" :alt="pic.name" class="bottom-bar__carrousel__slider__custom">
            </slide>
        </carousel>
      </div>
    </div>
    <div class="bottom-bar__copyright">
      <div class="bottom-bar__copyright__text">
        <p>desenvolvido por</p>
      </div>
      <div class="bottom-bar__copyright__image">

      </div>
    </div>
  </div>
</template>
<script>

import { Carousel, Slide } from 'vue-carousel';

var data = { counter: 0}

export default {
  name: 'BottomBar',
  components: {
    Carousel,
    Slide
  },
  data (){
    return{
      pics: []
    }
  },
  mounted() {
    fetch("https://convenia-front-end-test.firebaseio.com/partners.json")
    .then(response => response.json())
    .then((data) => {
      this.pics = data;
    })
  }
}

</script>
<style lang="scss">


 
  @import '../assets/css/util.scss';
  @import '../assets/css/carousel.scss';


  .bottom-bar{
    width: 100%;
    background-color: #f3f3f4; 
    display: flex;
    flex-direction: column;

    @include sm{
      flex-direction: row;
    }

    &__carrousel{
      width: 100%;
      height: 50%;
      display: flex;

      @include sm{
        height: 100%;
        width: 60%;
      }
      @include md{
        width: 60%;
      }

      &__text{
        width: 10%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #ababab;
        padding-left: 15px;
        font-size: 14px;

        @include xl{
          width: 30%;
        }
      }
      &__slider{
        width: 90%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;

       @include xl {
         justify-content: flex-start;
         width: 70%;
       }
        
        &__custom{
          margin: 0 auto;
          width: 60px;
          opacity: 0.6;
        }
      }
    }

    &__copyright{
      width: 100%;
      height: 50%;
      display: flex;

      @include sm{
        width: 40%;
        height: 100%;
      }
      @include md{
        width: 40%;
        height: 100%;
      }

      &__text{
        width: 45%;
        display: flex;
        align-items: center;
        justify-content: center;

        @include sm{
          justify-content: flex-end;
        }

        p{
          color: #ababab;
          font-size: 14px;
        }
      }
      &__image{
        height: 100%;
        width: 55%;
        background-image: url('../assets/images/ConveniaLogo.png');
        background-repeat: no-repeat;
        background-position: center;
        background-size: 60%;

        @include sm{
          background-size: 80%;
        }
      }
    }
  }

  @include arrows;
</style>
