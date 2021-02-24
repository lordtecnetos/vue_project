<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>{{ ttt }}</p>
    <button @click="toggleAudio()">
      <template v-if="!playing">Play</template>
      <template v-else>Pause</template>
    </button>
  </div>
</template>

<script>
import SockJS from "sockjs-client";
import Stomp from "webstomp-client";
import audio3 from "@/assets/audio.mp3";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
    ttt: String,
  },
  data() {
    return {
      audio: new Audio(audio3),
      playing: false,
    };
  },
  methods: {
    connect() {
      this.socket = new SockJS(process.env.VUE_APP_WS_URL);
      this.stompClient = Stomp.over(this.socket);
      this.stompClient.connect(
        {},
        (frame) => {
          this.connected = true;
          console.log(frame);
          this.stompClient.subscribe("/topic/greetings", (tick) => {
            console.log(tick);
            this.received_messages.push(JSON.parse(tick.body).content);
            this.audio.play();
          });
        },
        (error) => {
          console.log(error);
          this.connected = false;
        }
      );
    },

    toggleAudio() {
      if (this.audio.paused) {
        this.playing = true;
        this.audio.play();
      } else {
        this.playing = false;
        this.audio.pause();
      }
    },
  },
  mounted() {
    this.audio.loop = true;
    this.connect();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
</style>
