<template>
  <h2>{{ customTitle }}</h2>
  <p>{{ counter }} <sup>2</sup> = {{ squareCounter }}</p>

  <div>
    <button @click="increaseCounter">+1</button>
    <button @click="decreaseCounter">-1</button>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: {
      title: String,
      start: {
          type: Number,
          default: 5,
        //   required: true,
        validator(value) {
            return value >= 0
        }
      }
  },
  data() {
    return {
      counter: this.start,
    };
  },
  methods: {
    // getSquareValue() {
    //     return 'HOLA';
    // }
    increaseCounter() {
      this.counter++;
    },
    decreaseCounter() {
      this.counter--;
    },
  },
  computed: {
    squareCounter() {
      return this.counter * this.counter;
    },
    customTitle() {
        // return this.title ?? 'Counter'
        return this.title || 'Counter'
    }
  },
};
</script>

<style>
button {
  background-color: #64b687;
  border-radius: 5px;
  border: 1px solid white;
  color: white;
  cursor: pointer;
  margin: 0 5px;
  padding: 5px 15px;
  transition: 0.3s ease-in-out;
}
button:hover {
  background-color: #5aa67b;
  transition: 0.3s ease-in-out;
}
</style>