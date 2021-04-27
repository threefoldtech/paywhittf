<template>
  <div id="app">
    <a class="btn" @click="payWithTf">
      <img src="./assets/TFN.svg" alt="Logo" />
      <span>TF Pay</span>
    </a>
    <transition name="fade">
      <div class="overlay" v-if="showQr">
        <div>
          <div class="qr">
            <qrcode :value="qrText"/>
          </div>
          <h1>Scan this QR from your tf-wallet</h1>
          <a class="btn" @click="cancelPayment">Cancel</a>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
    import qrcode from '@chenfengyuan/vue-qrcode';

export default {
  name: "App",
  components: {
    qrcode
  },
  props: {
    message: {
      type: String,
      default: ""
    },
    amount: {
      type: String,
      default: ""
    },
    receiver: {
      type: String,
      default: ""
    },
    asset: {
      type: String,
      default: "tft"
    }
  },
  data() {
    return {
      showQr: false,
    };
  },
  created() {
    const linkNode = document.createElement('link');
    linkNode.type = 'text/css';
    linkNode.rel = 'stylesheet';
    linkNode.href = '//fonts.googleapis.com/css2?family=Bebas+Neue&display=swap';
    document.head.appendChild(linkNode);
  },
  methods: {
    payWithTf() {
      this.showQr = true;
      // setTimeout(() => {
      //     this.showQr = false;
      // }, 3000);
    },
    cancelPayment () {
      this.showQr = false;
      
    }
  },
  computed: {
    qrText() {
      // return { tft: '01ed90bee1d6d50b730a1aacf2890ac6fc0f7718849fba5f7c5719e3cfcc4641be09c5607b0210', amount: 0 }
      return `tft:${
        this.receiver
      }?amount=${Number(this.amount).toFixed(7)}&message=${
        this.message
      }&sender=${this.sender}`;
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
* {
  font-family: "Bebas Neue", sans-serif;
}
a.btn {
  border: #4ec48f;
  border-radius: 6px;
  height: 50px;
  width: 100px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  place-items: center;
  background: #44a687;
  color: white;
  padding: 0 20px;
}
.btn img {
  height: 2em;
  margin-right: 1em;
}
.btn span {
  font-size: 1.5em;
}
.overlay {
  position: fixed;
  left: 0;
  top: 0;
  height: 100vh;
  width: 100vw;
  display: grid;
  place-items: center;
  background: white;
}

.overlay > div {
  display: grid;
  place-items: center;
}
.overlay .btn {
  width: auto;
  grid-template-columns: 1fr;
}
</style>
