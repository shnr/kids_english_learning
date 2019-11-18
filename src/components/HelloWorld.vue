<template>
  <div class="hello">
    <div class="inner">
      <h1>{{ msg }}</h1>
      <router-link to="/q">はじめる</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      numOfquestions: 10,    
      values: [],
      msg: 'English Practice!!'
    }
  },
  created: function() {
    this.getquestion()
  },
  methods: {
    getquestion: function() {
      for(var i = 0; i < this.numOfquestions; i++) {
        let arr = {}
        arr.prob = [this.getRandomInt(9, 0), this.getRandomInt(9, 0)]
        this.values.push(arr)
      }
    },
    getRandomInt: function(max, min) {
      return Math.floor(Math.random() * (max - min) + min);
    },
    submit: function(){      
      for(var i = 0; i < this.values.length; i++) {
        let ans = this.values[i].prob.reduce(function (accumulator, currentValue, currentIndex, array) {
          return accumulator + currentValue;
        })
        let n = this.values[i].answer

        // set results
        let r = (Number(ans) === Number(n))? true : false
        this.$set(this.values[i], "result", r)
      }
    },
    reload: function(){
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  margin: 0;
  padding: 0;
}
p{
  margin: 0;
  padding: 0;
}
h1{
  margin-bottom: .8em;
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
.hello{
  height: 100%;
  position: relative;

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

   text-align: center;
}

</style>
