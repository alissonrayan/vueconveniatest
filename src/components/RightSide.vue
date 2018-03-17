<template>
    <div class="rightside-content">
    </div>
</template>
<script>
export default {
  name: 'RightSide'
}
</script>
<style lang="scss">
    @import '../assets/css/util.scss';

    .rightside-content{
        width: 100%;
        height: 100%;
        background-image: url('../assets/images/ConveniaIcon.png');
        background-repeat: no-repeat;
        background-position: 20% 80%;
        background-attachment: fixed;
        background-repeat: no-repeat;
        background-size: 50%;

        @include sm{
        background-attachment: scroll;
        background-size: 40%;
        }
    }
</style>
