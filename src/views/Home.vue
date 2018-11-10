<style>
.message,
.controls {
  clear: both;
  overflow-y: auto;
}
.bot {
  float: left;
}
.user {
  float: right;
}
</style>

<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <div class="message" v-for="(message, i) in messages" :key="i">
      <p :class="message.className">{{ message.text }}</p>
    </div>
    <div class="controls">
      <input type="text" v-model="userInput" />
      <button @click="sendUserInput">Send</button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import { Interactions } from "aws-amplify";

export default {
  name: "home",
  // components: {
  //   HelloWorld
  // },
  data() {
    return {
      messages: [],
      userInput: ""
    };
  },
  mounted() {
    // let userInput = 'I would like to pick up flowers';
    // Provide a bot name and user input
    // Interactions.send("OrderFlowers", userInput)
    //   .then((response) => {
    //     const { message:text } = response;
    //     // Log chatbot response
    //     console.log (response);
    //     this.messages.push({
    //       text,
    //       className: 'bot',
    //     });
    //   });
  },
  methods: {
    sendUserInput() {
      const { userInput: text } = this;
      this.messages.push({
        text,
        className: "user"
      });
      Interactions.send("OrderFlowers", text).then(response => {
        const { message: text } = response;
        this.messages.push({
          text,
          className: "bot"
        });
        // Log chatbot response
        console.log(response);
      });
    }
  }
};
</script>
