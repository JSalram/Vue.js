<template>
  <img v-if="image" :src="image" alt="background" />
  <div class="bg-dark"></div>

  <div class="indecision-container">
    <input v-model="question" type="text" placeholder="Hazme una pregunta" autofocus />
    <p>Recuerda terminar con un signo de interrogación</p>

    <div v-if="isValidQuestion">
      <h2>{{ oldQuestion }}</h2>
      <h1>{{ answer }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: "",
      oldQuestion: "",
      isValidQuestion: false,
      answer: null,
      image: null,
    };
  },
  methods: {
    async getAnswer() {
      this.answer = "Pensando...";

      const { answer, image } = await fetch("https://yesno.wtf/api").then((r) =>
        r.json()
      );

      this.answer = this.getSiNo(answer);
      this.image = image;
    },
    getSiNo(val) {
      return val === "yes" ? "SI" : "NO";
    },
  },
  watch: {
    question(val, oldVal) {
      this.isValidQuestion = false;
      if (!val.includes("?")) {
        return;
      }

      this.isValidQuestion = true;
      this.oldQuestion = val.charAt(0).toUpperCase() + val.slice(1);
      this.getAnswer();
    },
  },
};
</script>

<style scoped>
img,
.bg-dark {
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

h1,
h2 {
  color: white;
}

h2 {
  margin-top: 150px;
}
</style>