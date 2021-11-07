<template>
    <div v-if="this.$route.params.data.mood==1 && isLoaded===true" class="mood">
      <img v-bind:srcset="require('../assets/0-not-happy-at-all@1x.png') + ' 1x,' + require('../assets/0-not-happy-at-all@2x.png') + ' 2x' + require('../assets/0-not-happy-at-all@3x.png') + ' 3x'" alt="smiley" @load="onImgLoad" />
      <p>{{this.$route.params.data.text}}</p>
    </div>
    <div v-else-if="this.$route.params.data.mood==2 && isLoaded===true" class="mood">
      <img v-bind:srcset="require('../assets/1-not-happy@1x.png') + ' 1x,' + require('../assets/1-not-happy@2x.png') + ' 2x' + require('../assets/1-not-happy@3x.png') + ' 3x'" alt="smiley" @load="onImgLoad" />
      <p>{{this.$route.params.data.text}}</p>
    </div>
    <div v-else-if="this.$route.params.data.mood==3 && isLoaded===true" class="mood">
      <img v-bind:srcset="require('../assets/3-neutral@1x.png') + ' 1x,' + require('../assets/3-neutral@2x.png') + ' 2x' + require('../assets/3-neutral@3x.png') + ' 3x'" alt="smiley" @load="onImgLoad" />
      <p>{{this.$route.params.data.text}}</p>
    </div>
    <div v-else-if="this.$route.params.data.mood==4 && isLoaded===true" class="mood">
      <img v-bind:srcset="require('../assets/4-pretty-happy@1x.png') + ' 1x,' + require('../assets/4-pretty-happy@2x.png') + ' 2x' + require('../assets/4-pretty-happy@3x.png') + ' 3x'" alt="smiley" @load="onImgLoad" />
      <p>{{this.$route.params.data.text}}</p>
    </div>
    <div v-else-if="this.$route.params.data.mood==5 && isLoaded===true" class="mood">
      <img v-bind:srcset="require('../assets/5-super-happy@1x.png') + ' 1x,' + require('../assets/5-super-happy@2x.png') + ' 2x' + require('../assets/5-super-happy@3x.png') + ' 3x'" alt="smiley" @load="onImgLoad"/>
      <p>{{this.$route.params.data.text}}</p>
    </div>
    <div v-else class="spinner">
      <img v-bind:srcset="require('../assets/Spinner@1x.png') + ' 1x,' + require('../assets/Spinner@2x.png') + ' 2x' + require('../assets/Spinner@3x.png') + ' 3x'" alt="smiley" @load="onImgLoad" />
    </div>
</template>

<script>
export default {
  name: 'ResultView',
  data () {
    return{
      isLoaded: false,
    }
  },
  methods: {
    onImgLoad() {
      this.isLoaded = true;
      console.log(this.isLoaded)
    }
  } 
}
</script>

<style lang="scss">
  p{
    color:white;
    font-size: 30px;
    font-weight: bold;
  }
  .mood{
    margin-top: 5%;
    animation: 3s ease-out 0s 1 FadeIn;
  }
  .spinner{
    margin-top: 5%;
    animation: rotation 4s infinite linear;
  }
  @keyframes rotation{
    from{
      transform: rotate(0deg);
    }
    to{
      transform: rotate(359deg)
    }
  }
  @keyframes FadeIn {
    0% {
      opacity:0;
    }
    100% {
      opacity:1;
    }
  }

</style>