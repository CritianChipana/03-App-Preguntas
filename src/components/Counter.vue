<template>
  <h2>{{customTitle }}</h2>
  <p>{{counter}} <sup>2</sup> = {{counterSquared}} </p>

  <div class="btn">
    <button
    @click="increase"
    >+1</button>
    <button
    @click="decrease"
    >-1</button>
  </div>
</template>

<script>
export default {
  // name: 'miguel'
  props: {
    title: {
      type: String,
      // required: true
    },
    start: {
      type: Number,
      required: true,
      default: 100,
      validator: (value) => {
        return value > 100;
      }
    } 
  },
  data() {
    return {
      counter: this.start
    }
  }, 
  methods: {
    getSquarValue() {
      return this.counter * this.counter
    },
    increase () {
      this.counter++
    },
    decrease () {
      this.counter--
    }
  },
  computed: {
    counterSquared() {
      return this.counter * this.counter
    },
    customTitle() {
      return this.title || 'Counter'
    }
  }

}
</script>

<style>
button {
  background-color: #64bb87;
  border-radius: 3px;
  margin: 0 5px;
  border: 1px solid #ccc;
  padding: 5px 10px;
}
</style>