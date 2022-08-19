<template>
  <img v-if="img" :src="img" alt="bg">
  <div class="bg-dark"></div>

  <h1>App de preguntas (chipaneitor ;)</h1>


  <div class="indecision-container">
    <input v-model="question" type="text" placeholder="Hazme una pregunta">
    <p>Recuerda terminar con  un signo de interrogacion(?)</p>
      <dir v-if="isValidQuestion">
        <h1>{{question}}</h1> 
        <h1>{{(answer === 'yes') ? 'si' : 'no'}}</h1>
      </dir>
  </div>

</template>

<script>
export default {
  data () {
    return {
      question: '',
      answer: null,
      img: null,
      isValidQuestion: false
    }
  },
  watch: {
    question(value, oldValue){

      this.isValidQuestion = false

      if(!value.includes('?')) return
      //realizamos la peticion http

      this.isValidQuestion = true
      this.getAnswer()
    }
  },
  methods: {
    async getAnswer () {  
      this.answer = 'pensando...'

      const {answer, image} = await fetch('https://yesno.wtf/api').then(r => r.json())
      this.answer = answer
      this.img = image
      console.log(answer)
    }
  }

}
</script>

<style scoped>

    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>