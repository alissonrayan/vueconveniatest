<template>
  <div id="app" class="app">
    <div class="app__content"> 
      <left-side class="app__content__leftside" />
      <right-side class="app__content__rightside" />
    </div>
    <bottom-bar class="app__bottombar" />
  </div>
</template>

<script>
import RightSide from './components/RightSide'
import LeftSide from './components/LeftSide'
import BottomBar from './components/BottomBar'

export default {
  name: 'app',
  components: {
    RightSide,
    LeftSide,
    BottomBar
  }
}
</script>

<style lang="scss">
  @import './assets/css/general.css';
  @import './assets/css/util.scss';
  
  .app{
    margin: 0;
    width: 100%;
    height: auto;
    display: flex;
    flex-direction: column;

    @include sm{
      height: 100vh;
    }

    @include md{
      height: 100vh;
    }

    &__content{
      width: 100%;
      display: flex;
      flex-direction: column;
      
      @include sm{
        flex-direction: row;
        height: 88vh;
      }

      &__leftside{
        min-width: 50%;
        height: 100%;
        background-color: #fff;

        @include sm{
        }
      }
      &__rightside{
        min-width: 50%;
        min-height: 50vh;
        background-color: #868686;

        @include sm{
        }
      }
    }

    &__bottombar{
      width: 100%;
      height: 30vh;
      background-color: #999;

      @include sm{
        height: 12vh;
      }
    }
  }
</style>
