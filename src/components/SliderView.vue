<template>
  <div class="main">
    <h1>Happiness Slider</h1>
    <img v-bind:srcset="require('../assets/3-neutral@1x.png') + ' 1x,' + require('../assets/3-neutral@2x.png') + ' 2x' + require('../assets/3-neutral@3x.png') + ' 3x'" alt="smiley" />
    <h2 id="question">How you're doing?</h2>    
    <div class="toolTip">
        <p>I'm feeling...</p>
        <img v-bind:src="tool_picture" />
    </div>
    <div class="slider-wrapper">      
      <input type="range" v-model="mood_value" class="slider" id="slider" min="0" max="5">
      <input @click.stop.prevent="fetchMood" type="image" v-bind:src="button_picture" class="submit" id="submit">
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: 'SliderView',
    data () {
      return{
        button_picture: require('../assets/Submit@1x.png'),
        tool_picture: require('../assets/Tooltip arrow@1x.png'),
        mood_value: 0,
        mood_data: {},
      }
    },
    methods: {
      fetchMood(){
        axios.post('https://automation.uselab.com/api/fe-test/mood', {mood:this.mood_value})
          .then ((response)=> {
            this.mood_data = response.data.data;  
            console.log(this.mood_data);
            this.$router.push({name: 'Result', params: {data: this.mood_data}})          
          })   
          .catch(() => {
            this.$router.push({name: 'Result', params: {data: {}}})  
          })
             
      },
    }
  }
</script>

<style lang="scss">
  .main{
    position: relative;
    animation: 2s ease-out 0s 1 FadeIn;
  }
  h1{
    font-size: 4rem;
    color: white;
    font-weight: normal;
  }
   #question{
    font-size: 3rem;
    color: white;
    font-weight: normal;
    opacity: 1;
    transition: all 2s;
    position: absolute;
    left: 50%;
    transform: translate(-50%);
  }

  .slider-wrapper{
    height: 60px;
    border-radius: 30px;
    background-color: #fff;    
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    box-sizing: border-box;
    opacity: 0;
    transition: all 2s;
    position: absolute;
    left: 50%;
    transform: translate(-50%);
    top: 130%;
  }
  .slider{
    cursor: pointer;
    margin: 25px;
    height: 10px;
    -webkit-appearance: none;
    background-color: #39B8FF;
    border-radius: 5px;
  }
 
  .slider::-webkit-slider-thumb{
    -webkit-appearance: none;
    appearance: none;
    width: 30px;
    height: 30px;
    background-image: url("../assets/Slider handle@1x.png");
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }
  .slider::-moz-range-thumb{
    -webkit-appearance: none;
    appearance: none;
    width: 30px;
    height: 30px;
    background-image: url("../assets/Slider handle@1x.png");
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }
  .slider::-ms-thumb{
    -webkit-appearance: none;
    appearance: none;
    width: 30px;
    height: 30px;
    background-image: url("../assets/Slider handle@1x.png");
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }
  .submit{
    height: 80%;
    margin-top: 5px;
    margin-right: 12px;
  }
  .main:hover #question{
    opacity: 0;
  }
  .main:hover .slider-wrapper{
    opacity: 1;
  }
  .toolTip{
    position: absolute;
    left: 50%;
    transform: translate(-50%);
    top:95%;
    opacity: 0;
    transition: all 2s;
  }
  .toolTip p{
    font-size: 2rem;
  }

@media(max-width:570px){
    h1{
      font-size: 3rem;
    }
    #question{
      font-size: 2rem;
    }   
  }
  

@media(max-width:420px){
    h1{
      font-size: 2rem;
    }
    #question{
      font-size: 1rem;
    }  
    .toolTip p{
      font-size: 1.5rem;
    } 
  }
   
  
.main:hover .toolTip{
  opacity: 1;
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

