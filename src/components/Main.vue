<template>
  <div id="nav" :style="{
    top: 1.5 * deviceHeight - nowHeight > 0.04 * deviceHeight ? (1.5 * deviceHeight - nowHeight) + 'px' : 0.04 * deviceHeight + 'px',
  }">
    <h1 :style="{
      left: 0.5 * deviceWidth - (nowHeight - deviceHeight) < 0.15 * deviceWidth ? '15%' : 0.5 * deviceWidth - (nowHeight - deviceHeight) + 'px'
    }">Title</h1>
    <ul :style="{
      left: 0.55 * deviceWidth - (nowHeight - deviceHeight) < 0.3 * deviceWidth ? '30%' : 0.55 * deviceWidth - (nowHeight - deviceHeight) + 'px',
      right: 0.55 * deviceWidth - (nowHeight - deviceHeight) < 0.1 * deviceWidth ? '10%' : 0.55 * deviceWidth - (nowHeight - deviceHeight) + 'px',
      opacity: (nowHeight - deviceHeight) * 0.001
    }">
      <li> Nav item</li>
      <li> Nam item</li>
      <li> Nav item</li>
    </ul>
  </div>
  <div id="masonry" class="masonry-grid" :style="{
    gap: (nowHeight - deviceHeight) - 0.7 * deviceHeight > masonryHeight ? '1vw' : Math.abs((nowHeight - deviceHeight) - (masonryHeight + 0.7 * deviceHeight)) * 0.6 + 15 + 'px',
    opacity: (nowHeight - deviceHeight) * 0.0015
  }">
    <div class="item item-1">
      <img src="https://picsum.photos/400/400?radom=1" alt="">
    </div>
    <div class="item item-2">
      <img src="https://picsum.photos/400/400?radom=2" alt="">
    </div>
    <div class="item item-3">
      <img src="https://picsum.photos/400/400?radom=3" alt="">
    </div>
    <div class="item item-4">
      <img src="https://picsum.photos/400/400?radom=4" alt="">
    </div>
    <div class="item item-5">
      <img src="https://picsum.photos/400/400?radom=5" alt="">
    </div>
    <div class="item item-6">
      <img src="https://picsum.photos/400/400?radom=6" alt="">
    </div>
    <div class="item item-7">
      <img src="https://picsum.photos/400/400?radom=7" alt="">
    </div>
    <div class="item item-8">
      <img src="https://picsum.photos/400/400?radom=8" alt="">
    </div>
    <div class="item item-9">
      <img src="https://picsum.photos/400/400?radom=9" alt="">
    </div>
    <div class="item item-10">
      <img src="https://picsum.photos/400/400?radom=10" alt="">
    </div>
  </div>

  <div id="introduction1" class="introduction">
    <div class="mask" :class="{ rightToLeftToRight: nowHeight - 1.2 * deviceHeight > introHeight1 }">
      <div class="text" :class="{ introductionText: nowHeight - 1.2 * deviceHeight > introHeight1 }">
        <h1 class="">Introduction</h1>
        <ul>
          <li>description</li>
          <li>description</li>
          <li>description</li>
        </ul>
      </div>
    </div>
    <div class="img img-1">
      <div class="border borderTop" :class="{ 'width0To100': nowHeight - 1.3 * deviceHeight > introHeight1 }">
      </div>
      <div class="border borderRight" :class="{ 'fromCenterToRight': nowHeight - 1.3 * deviceHeight > introHeight1 }">
      </div>
      <div class="border borderBottom" :class="{ 'width0To100': nowHeight - 1.3 * deviceHeight > introHeight1 }">
      </div>
      <div class="border borderLeft" :class="{ 'fromCenterToLeft': nowHeight - 1.3 * deviceHeight > introHeight1 }">
      </div>
    </div>
  </div>
  <div id="introduction2" class="introduction">
    <div class="mask" :class="{ rightToLeftToRight: nowHeight - 2.2 * deviceHeight > introHeight1 }">
      <div class="text" :class="{ introductionText: nowHeight - 2.2 * deviceHeight > introHeight1 }">
        <h1 class="">Introduction</h1>
        <ul>
          <li>description</li>
          <li>description</li>
          <li>description</li>
        </ul>
      </div>
    </div>
    <div class="img img-2">
      <div class="border borderTop" :class="{ 'width0To100': nowHeight - 2.3 * deviceHeight > introHeight1 }">
      </div>
      <div class="border borderRight" :class="{ 'fromCenterToRight': nowHeight - 2.3 * deviceHeight > introHeight1 }">
      </div>
      <div class="border borderBottom" :class="{ 'width0To100': nowHeight - 2.3 * deviceHeight > introHeight1 }">
      </div>
      <div class="border borderLeft" :class="{ 'fromCenterToLeft': nowHeight - 2.3 * deviceHeight > introHeight1 }">
      </div>
    </div>
  </div>
  <div class="footer">
    <transition name="chat">
      <div v-if="nowHeight >= 4.2 * deviceHeight " class="chat" @click.self="chatStart">
        <transition-group name="message" tag="div" class="messageBox">
          <div v-for="(message, index) in messages" :key="index" class="msg"
            :class="{ right: message.user === 'user', left: message.user === 'bot' }">
            <p class="messageContent">{{ message.content }}</p>
          </div>
        </transition-group>
        <div class="messageInput">
          <input :disabled="!canSendMessage" @keydown.enter="newMessage({ user: 'user', content: messageInput })" v-model="messageInput" type="text">
          <button v-if="!messages.length" @click="chatStart" class="messageSend">Knock</button>
          <button v-else :disabled="!canSendMessage" @click="newMessage({user: 'user', content: messageInput})" class="messageSend">Send</button>
        </div>
      </div>
    </transition>
    <footer>: )</footer>
  </div>


</template>

<script>
export default {
  name: "MainComp",
  data() {
    return {
      nowHeight: 0,
      deviceHeight: 0,
      deviceWidth: 0,
      masonryHeight: 0,
      introHeight1: 0,
      introHeight2: 0,
      messages: [],
      messageInput: '',
      canSendMessage: false
    }
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
    this.nowHeight =
      window.pageYOffset + document.documentElement.clientHeight ||
      document.documentElement.scrollTop + document.documentElement.clientHeight ||
      document.body.scrollTop + document.documentElement.clientHeight;
    this.masonryHeight = document.getElementById('masonry').offsetTop
    this.introHeight1 = document.getElementById('introduction1').offsetTop
    this.introHeight2 = document.getElementById('introduction2').offsetTop
    this.deviceHeight = document.documentElement.clientHeight
    this.deviceWidth = document.documentElement.clientWidth
  },
  methods: {
    handleScroll() {
      this.nowHeight =
        window.pageYOffset + document.documentElement.clientHeight ||
        document.documentElement.scrollTop + document.documentElement.clientHeight ||
        document.body.scrollTop + document.documentElement.clientHeight;
    },
    newMessage({ user, content }) {
      if (!content.trim()) {
        return
      }
      this.messages.push({
        user: user,
        content: content,
      })
      this.messageInput = ''
      if (this.messages.length === 4 ) {
        this.chatContinue()
      } else return
    },
    async chatStart() {
      console.log('start')
      this.newMessage({ user: 'user', content: 'Knock knock.' });
      await this.delay(1000)
      this.newMessage({ user: 'bot', content: 'Hi dear.' })
      await this.delay(1500)
      this.newMessage({ user: 'bot', content: 'How is going today?' })
      this.canSendMessage = true
    },
    delay(time) {
      return new Promise((resolve) => setTimeout(resolve, time))
    },
    async chatContinue() {
      console.log('continue')
      this.canSendMessage = false
      await this.delay(2000)
      this.newMessage({ user: 'bot', content: "Well" })
      await this.delay(2000)
      this.newMessage({ user: 'bot', content: "I hope you enjoy this website." })
      await this.delay(3000)
      this.newMessage({ user: 'bot', content: 'If you have any feedback or question to us, you can send messages here.' })
      await this.delay(3000)
      this.newMessage({ user: 'bot', content: "Don't worry, It's anonymous, you can say anything you want, we will reply you asap.(if you write your own email address in message)" })
      this.canSendMessage = true
    },

  },
}
</script>

<style scoped>
#nav {
  position: fixed;
  width: 100%;
  height: 8vh;
  top: 50vh;
  transform: translateY(-50%);
  line-height: 8vh;
  z-index: 10;
  background-color: rgba(255, 255, 255, 0.87);
}

#nav h1 {
  opacity: 1;
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  font-size: 5vh;
}

#nav ul {
  display: flex;
  justify-content: space-between;
  overflow: hidden;
  position: absolute;
  top: 0px;
  left: 55%;
  right: 30%;
  bottom: 0;
  opacity: 1;
  text-align: left;
}

.masonry-grid {
  padding: 5vh 10vw;
  overflow: hidden;
  justify-content: center;
  width: 100%;
  height: 100vh;
  margin: 0 auto;
  margin-top: 100vh;
  display: grid;
  grid-auto-columns: 1fr;
  grid-auto-rows: 1fr;
  gap: 20px;
  grid-template-areas:
    "item1 item1  item2 item2  item3 item3  item4 item4"
    "item1 item1  item2 item2  item3 item3  item4 item4"
    "item1 item1  item6 item6  item3 item3  item8 item8"
    "item5 item5  item7 item7  item7 item7  item8 item8"
    "item5 item5  item7 item7  item7 item7  item8 item8"
    "item9 item9  item9 item9  item10 item10 item8 item8"
    "item9 item9  item9 item9  item10 item10 item8 item8"
  ;
}

.item-1 {
  grid-area: item1;
}

.item-2 {
  grid-area: item2;
}

.item-3 {
  grid-area: item3;
}

.item-4 {
  grid-area: item4;
}

.item-5 {
  grid-area: item5;
}

.item-6 {
  grid-area: item6;
}

.item-7 {
  grid-area: item7;
}

.item-8 {
  grid-area: item8;
}

.item-9 {
  grid-area: item9;
}

.item-10 {
  grid-area: item10;
}

.item-11 {
  grid-area: item11;
}

.item-12 {
  grid-area: item12;
}


.masonry-grid .item {
  padding: 2px;
  position: relative;
  counter-increment: count;
}

.masonry-grid .item::after {
  transition: all .3s ease;
}

.masonry-grid .item:hover::after {
  opacity: 0.6;
}

.masonry-grid .item img {
  display: block;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  object-fit: cover;
  flex: 1;
}

.masonry-grid .item::after {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: gray;
  color: #fff;
  font-size: 50px;
  content: counter(count);
  opacity: 0;
}

.introduction {
  position: relative;
  width: 100%;
  height: 100vh;
  padding: 5vh 0;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.introduction .mask {
  border-right: 1px solid black;
  position: relative;
  left: 25%;
  width: 50%;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: center;
}

.introduction .text {
  width: 100%;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: center;
  opacity: 0;
  letter-spacing: 3px;
}

.introduction .text h1 {
  font-size: 30px;
  position: relative;
  overflow: hidden;
  left: 0%;
}

.introduction .text li {
  margin-top: 2vw;
}




.introduction .img-1 {
  background-image: url(https://picsum.photos/1920/1080?radom=11);
  opacity: 0.8;
}

.introduction .img-2 {
  background-image: url(https://picsum.photos/1920/1080?radom=12);
  opacity: 0.8;
}

.introduction .img {
  margin-top: 3vw;
  width: 100%;
  height: 70%;
  position: relative;
  left: 0;
  background-attachment: fixed;
  background-position: center 0;
  background-repeat: no-repeat;

}

.introduction .img img {
  width: 100%;
  height: 100%;
  opacity: .9;
  object-fit: cover;
}

.introduction .img .border {
  position: absolute;
}

.introduction .borderTop {
  background-color: rgba(211, 211, 211, 0.164);
  width: 0%;
  height: 5px;
  top: 0;
  right: 0;
  z-index: 5;
}

.introduction .borderLeft {
  background-color: white;
  width: 50%;
  height: 100%;
  top: 0;
  left: 0;
}

.introduction .borderBottom {
  background-color: rgba(211, 211, 211, 0.164);
  width: 0%;
  height: 5px;
  bottom: 0;
  left: 0;
  z-index: 5;
}

.introduction .borderRight {
  background-color: white;
  width: 50%;
  height: 100%;
  top: 0;
  right: 0;
}

.footer {
  width: 100%;
  height: 100vh;
  padding: 10%;
  position: relative;
}

.footer .chat {
  border-radius: 20px;
  width: 100%;
  height: 80%;
  overflow: hidden;
  position: relative;
}

.footer .chat .messageBox::-webkit-scrollbar {
  display: none;
}

.footer .chat .messageBox {
  padding: 3%;
  height: 90%;
  overflow-y: scroll;
  background-color: rgb(243, 243, 243);
}

.chat-enter-from {
  transform: translateY(300px);
  opacity: 0;
}

.chat-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.chat-enter-active {
  transition: all ease 1.5s;
}


.message-enter-from {
  transform: translateY(30px);
  opacity: 0;
}

.message-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.message-enter-active {
  transition: all ease .5s;
}

.footer .chat .messageBox .msg {
  margin-bottom: 20px;
  min-height: 40px;
  display: grid;
}

.footer .chat .messageBox .msg p {
  min-height: 40px;
  line-height: 40px;
  font-size: 20px;
  display: inline-block;
  border-radius: 20px;
  padding: 0 20px;
  transition: all ease .5s;
}

.footer .chat .messageBox .msg.left p {
  background-color: white;
  color: rgb(150, 150, 150);
  justify-self: start;
}

.footer .chat .messageBox .msg.right p {
  background-color: rgb(221, 221, 221);
  color: white;
  justify-self: end;
}

.footer .chat .messageInput {
  height: 10%;
  width: 100%;
  padding: 0 3%;
  position: absolute;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: rgb(245, 245, 245);
}

.footer .chat .messageInput input {
  height: 70%;
  width: 80%;
  padding: 0 5%;
  font-size: 20px;
  border-radius: 20px;
  border: 0;
  outline: 0;
  background-color: white;
  color: rgba(0, 0, 0, 0.5);
}

.footer .chat .messageInput button:hover {
  cursor: pointer;
}

.footer .chat .messageInput button {
  text-align: center;
  border: 0;
  border-radius: 20px;
  width: 80px;
  height: 70%;
  padding: 0 15px;
  font-size: 18px;
  background-color: rgb(143, 143, 143);
  color: #fff;
}

footer {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 15%;
  width: 100%;
  background-color: rgb(216, 216, 216);
  display: flex;
  justify-content: center;
  align-items: end;
  font-size: 30px;
  color: white;
}

/**  Animation */

.rightToLeftToRight {
  animation: rightToLeftToRight 1s ease-out both;
}

.introductionText {
  animation: introductionText 1s linear both;
}

.width0To100 {
  animation: width0To100 1s ease-in-out both;
}

.width0To100D3 {
  animation: width0To100 1s ease-in-out both;
  animation-delay: .2s;
}


.width0To40 {
  animation: width0To40 2s ease-in-out both;
  animation-delay: .8s;
}


.fromCenterToLeft {
  animation: fromCenterToLeft .5s ease-out both;
  animation-delay: 1s;

}

.fromCenterToRight {
  animation: fromCenterToRight .5s ease-out both;
  animation-delay: 1s;
}

@keyframes rightToLeftToRight {
  0% {
    width: 50%;
  }

  29% {
    border-right: 1px solid black;
  }

  30% {
    width: 0%;
    border-right: 2px solid black;
  }

  100% {
    width: 50%;
    border-right: 2px solid black;
  }
}

@keyframes introductionText {
  0% {
    opacity: 0;
  }

  29% {
    opacity: 0;
  }

  30% {
    opacity: 1;
  }

  100% {
    opacity: 1;
  }
}

@keyframes width0To100 {
  0% {
    width: 0%;
  }

  100% {
    width: 100%;
  }
}

@keyframes width0To40 {
  0% {
    width: 0%;
  }

  100% {
    width: 40%;
  }
}


@keyframes fromCenterToLeft {
  0% {
    width: 50%;
  }

  100% {
    width: 0px;
  }
}

@keyframes fromCenterToRight {
  0% {
    width: 50%;
  }

  100% {
    width: 0px;
  }
}
</style>