<template>
  <div class="hello">
    <router-link class="btn-back-home" to="/"><span class="ic"></span></router-link>
    <template v-if="!ifFinish">
      <div class="target-word-wrap">
        <div class="fig-box">
          <img :src="currentImage" alt="">
        </div>    
        <div class="audio-box">
          <div class="btn-play" @click="playsound(currentSound)">
            <img src="../assets/play-button_3.svg" alt="">
          </div>
        </div>
        <div class="name-box">
          <p class="word-ttl" v-bind:class="{hidden: isHidden}">{{currenterm.title}}</p>
        </div>
        <div class="btn-foot-bar">          
          <div class="btn-next-pProblem" @click="goNext()">つぎへ</div>
        </div>        
      </div>
    </template>

    <template v-if="ifFinish">
      <div class="reload-wrap">
        <div class="btn-reload" v-on:click="reload()">もう一度！</div>
      </div>      
    </template>

    <!-- <button v-on:click="submit()">submit</button>
    <button v-on:click="reload()">reload</button> -->

    <!-- <div class="footers">
      <router-link to="/">HOME</router-link>
    </div> -->

  </div>
</template>

<script>

const terms = [
  {
    title: 'APPLE',
    soundName: 'apple.mp3',
    imageName: 'apple.png',
  },
  {
    title: 'FISH',
    soundName: 'fish.mp3',
    imageName: 'fish.png',
  },
  {
    title: 'DOG',
    soundName: 'dog.wav',
    imageName: 'dog.png',
  },
  {
    title: 'BIRD',
    soundName: 'bird.wav',
    imageName: 'bird.png',
  },
  {
    title: 'CAR',
    soundName: 'car.mp3',
    imageName: 'car.png',
  },
  {
    title: 'CAT',
    soundName: 'cat.wav',
    imageName: 'cat.png',
  },
  {
    title: 'DINOSAUR',
    soundName: 'dinosaur.mp3',
    imageName: 'dinosaur.png',
  },
  {
    title: 'DUCK',
    soundName: 'duck.wav',
    imageName: 'duck.png',
  },
  {
    title: 'ELEPHANT',
    soundName: 'elephant.wav',
    imageName: 'elephant.png',
  },
  {
    title: 'LION',
    soundName: 'lion.mp3',
    imageName: 'lion.png',
  },
  {
    title: 'TIGER',
    soundName: 'tiger.mp3',
    imageName: 'tiger.png',
  },
  {
    title: 'ORANGE',
    soundName: 'orange.mp3',
    imageName: 'orange.png',
  }
]

export default {
  name: 'Question',
  data () {
    return {
      terms : terms,
      currenterm: {},
      currentImage: '',
      currentSound: '',
      numOfquestions: 5,    
      values: [],
      currentQuestion: 0,
      ifFinish: false,
      correctQuestionNum: 0,
      isHidden: true
    }
  },
  created: function() {
    this.getquestion()
  },
  methods: {
    getquestion: function() {
      console.log(this.terms)
      this.isHidden = true
      let n = this.getRandomInt(this.terms.length, 0)
      this.currenterm = this.terms[n]
      this.terms.splice(n,1);
      this.currentImage = require('../assets/targets/' + this.currenterm.imageName)
      this.currentSound = require('../assets/pronouces/' + this.currenterm.soundName)
      console.log(this.currenterm)
    },
    getRandomInt: function(max, min) {
      return Math.floor(Math.random() * (max - min) + min);
    },

    submit: function(){  
      // console.log(this.values)    
      this.ifFinish = true
      for(var i = 0; i < this.values.length; i++) {
        let ans = this.values[i].prob.reduce(function (accumulator, currentValue, currentIndex, array) {
          return accumulator + currentValue;
        })
        let n = this.values[i].answer

        // set results
        let r = (Number(ans) === Number(n))? true : false
        this.$set(this.values[i], "result", r)

        if(r){
          this.correctQuestionNum++
        }
      }
    },

    playsound:function(playsound){
      var audio = new Audio(playsound);
      audio.play();
      this.isHidden = false;
    },

    reload: function(){
      this.$router.go({path: this.$router.currentRoute.path, force: true})
    },

    goNext: function(){
      let self = this
      if (this.terms.length > 0) {
        this.getquestion()  
      } else {
        self.ifFinish = true
      }      
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.reload-wrap{
  height: 100vh;
  display: -ms-flexbox;
  display: flex;  
  justify-content: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  align-content: center;
  -webkit-align-content: center;
  -ms-flex-line-pack: center;
  align-items: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
}
.btn-reload{
  font-size: 6.4vmin;
  line-height: 1;
  width: 60%;
  color: #fff;
  display: block;
  margin: 0 auto;
  border: 1px solid #2196f3;
  background-color: #2196f3;
  padding: .8em 0;  
}
.target-word-wrap{
  
}
.target-word-wrap .fig-box{
  padding: 32px 0;
  height: 48vh;
  display: -ms-flexbox;
  display: flex;  
  justify-content: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  align-content: center;
  -webkit-align-content: center;
  -ms-flex-line-pack: center;
  align-items: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
}
.target-word-wrap .fig-box img{
  max-width: 240px;
  height: auto;
}
.name-box{
  margin: 4.27vmin auto;
}
.name-box .word-ttl{
  font-size: 12.8vmin;
  line-height: 1.6;
  color: #607d8b;
  letter-spacing: .1em;
  font-weight: bold;
  transition: all .7s cubic-bezier(0.190, 1.000, 0.220, 1.000);
}
.name-box .word-ttl.hidden{
  color: #fff;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
p{
  margin: 0;
  padding: 0;
}
.btn-next-pProblem{
  font-size: 6.4vmin;
  line-height: 1;
  max-width: 40%;
  color: #fff;
  display: block;
  margin: 0 auto;
  border: 1px solid #2196f3;
  background-color: #2196f3;
  padding: .8em 0;
}
.btn-play {
  max-width: 40%;
  font-size: 6.4vmin;
  margin: 0 auto;
  background-color: #4CAF50;
  /*border: 0px solid rgba(0,0,0,1);*/
  padding: .8em 0;
}
.btn-play img{
  max-height: 6.4vmin;
  width: auto;
  display: block;
  margin: 0 auto;
}
.result-text{
  font-size: 24px;
  line-height: 1.6;
  color: #000;
  display: block;
  text-align: center;
  margin-top: 2em;
}
.result-box{
  width: 53.3vmin;
  text-align: left;
  margin: 0 auto 0;
}
.is-false{
  font-size: 16px;
  line-height: 1.6;  
}
.is-true{
  font-size: 16px;
  
}
.is-box-true{
  color: #2196f3;
}
.is-box-false{
  color: #9e9e9e;
}
.hello{
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
  height: 100%;
  position: relative;
}
.footers{
  position: absolute;
  bottom: 0;
  text-align: center;
  width: 100%;
  padding: 20px 0;

}
.btn-foot-bar{
}
.btn-back-home{
  position: absolute;
  top: 0;
  left: 0;
  width: 4.27vmin;
  height: 4.27vmin;
  padding: 3.2vmin;
}
.btn-back-home .ic{
  display: block;
  background-color: #000;
  border: 1px solid #000;
  border-radius: 50%;
  width: 4.27vmin;
  height: 4.27vmin;
}
</style>
