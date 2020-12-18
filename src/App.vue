<template>
  <div>
    <div class="main">
      <button @click="myAnimation = 'slide'">slide</button>
      <button @click="myAnimation = 'fade'">Fade</button>
      <p>{{ myAnimation }}</p>
      <br>
      <button @click="add">追加</button>
      <ul style="width: 200px; margin: auto;">
        <transition-group nume="fade">
          <li
            style="cursor: pointer;"
            v-for="(number, index) in numbers"
            :key="number"
            @click="remove(index)"
          >{{number}}</li>
        </transition-group>

      </ul>
      <br>
      <button @click="show = !show">切り替え</button>
      <br /><br />
      <transition
        :css="false"
        @before-enter="beforeEnter"
        @enter="enter"
        @leave="Leave"
      >
        <div class="circle" v-if="show"></div>
      </transition>
      <br />
      <button @click="myComponent = 'ComponentA'">ComponentA</button>
      <button @click="myComponent = 'ComponentB'">ComponentB</button>
      <transition name="fade" mode="out-in">
        <component :is="myComponent"></component>
      </transition>
      <transition name="fade" mode="out-in">
        <p v-if="show" key="bye">さようなら</p>
        <p v-if="!show" key="hello">こんにちは</p>
      </transition>

      <transition
        enter-class=""
        enter-to-class=""
        enter-active-class="animate__animated animate__bounce"
        leave-class=""
        leave-active-class="animate__animated animate__rubberBand"
        leave-to-class=""
        appear
      >
        <p v-if="show">hello</p>
      </transition>

      <transition name="myAnimation" appear>
        <p v-if="show">bye</p>
      </transition>
    </div>
    <LikeHeader>
      <template>
        <h1>トータルのいいね数</h1>
      </template>

      <template v-slot:num>
        <h2>{{ number }}</h2>
      </template>
    </LikeHeader>

    <LikeNumber
      :total-number="number"
      v-on:my-click="number = $event"
    ></LikeNumber>
    <LikeNumber
      :total-number="number"
      v-on:my-click="number = $event"
    ></LikeNumber>
    <button @click="currentComponent = 'Home'">Home</button>
    <button @click="currentComponent = 'About'">About</button>
    <keep-alive>
      <component :is="currentComponent"></component>
    </keep-alive>
    <div style="padding: 10rem;">
      <h2>イベントのフォーム</h2>
      <EventTitle v-model="eventData.title"></EventTitle>
      <MaxNumber v-model="eventData.maxnumber"></MaxNumber>

      <label for="host">主催者</label>
      <input id="host" type="text" v-model.trim="eventData.host" />
      <p>{{ eventData.host }}</p>
      <label for="detail">イベントの内容</label>
      <textarea
        id="detail"
        cols="30"
        rows="10"
        v-model="eventData.detail"
      ></textarea>
      <pre>{{ eventData.detail }}</pre>
      <input type="checkbox" id="isPrivate" v-model="eventData.isPrivate" />
      <label for="isPrivate">非公開</label>
      <p>{{ eventData.isPrivate }}</p>
      <p>参加条件</p>
      <input type="checkbox" id="10" value="10代" v-model="eventData.target" />
      <label for="10">10代</label>
      <input type="checkbox" id="20" value="20代" v-model="eventData.target" />
      <label for="20">20代</label>
      <input type="checkbox" id="30" value="30代" v-model="eventData.target" />
      <label for="30">30代</label>
      <p>{{ eventData.target }}</p>
      <p>参加費</p>
      <input type="radio" id="free" value="無料" v-model="eventData.price" />
      <label for="free">無料</label>
      <input type="radio" id="paid" value="有料" v-model="eventData.price" />
      <label for="paid">有料</label>
      <p>開催場所</p>
      <select v-model="eventData.location">
        <option v-for="location in locations" :key="location">{{
          location
        }}</option>
      </select>
      <p>{{ eventData.location }}</p>
    </div>
  </div>
</template>

<script>
import LikeHeader from "./components/LikeHeader.vue";
import About from "./components/About.vue";
import Home from "./components/Home.vue";
import EventTitle from "./components/EventTitle.vue";
import MaxNumber from "./components/MaxNumber.vue";
import ComponentA from "./components/ComponentA.vue";
import ComponentB from "./components/ComponentB.vue";

export default {
  data() {
    return {
      numbers: [0,1,2],
      nextNumber: 3,
      show: true,
      myAnimation: "slide",
      myComponent: "ComponentA",
      number: 14,
      currentComponent: "Home",
      locations: ["東京", "大阪", "名古屋"],
      eventData: {
        title: "タイトル",
        maxNumber: 0,
        host: "",
        detail: "",
        isPrivate: false,
        target: [],
        price: "無料",
        location: [],
      },
    };
  },
  components: {
    LikeHeader,
    About,
    Home,
    EventTitle,
    MaxNumber,
    ComponentA,
    ComponentB,
  },
  methods: {
    randomIndex(){
      return Math.floor(Math.random() * this.numbers.length);
    },
    add(){
      this.numbers.splice(this.randomIndex(), 0, this.nextNumber);
      this.nextNumber += 1;
    },
    remove(index) {
      this.numbers.splice(index, 1);
    },
    beforeEnter(el) {
      el.style.transform = "scale(0)";
    },
    enter(el, done) {
      let scale = 0;
      const interval = setInterval(() => {
        el.style.transform = `scale(${scale})`;
        scale += 0.1;
        if (scale > 1) {
          clearInterval(interval);
          done();
        }
      }, 20);
    },
    leave(el, done) {
      let scale = 1;
      const interval = setInterval(() => {
        el.style.transform = `scale(${scale})`;
        scale -= 0.1;
        if (scale < 0) {
          clearInterval(interval);
          done();
        }
      }, 20);
    },
  },
};
</script>

<style scoped>
.circle {
  width: 200px;
  height: 200px;
  margin: auto;
  border-radius: 100px;
  background-color: cadetblue;
}
.fade-move{
  transition: transform 1s;
}
.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  transform: opacity 1s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave {
  opacity: 1;
}
.fade-leave-active {
  transform: opacity 1s;
  position: absolute;
  width: 200px;
}
.fade-leave-to {
  opacity: 0;
}

.slide-enter,
.slide-leave-to {
  opacity: 0;
}
.slide-enter-active {
  animation: slide-in 0.5s;
  transition: opactiy 1s;
}
.slide-leave-active {
  animation: slide-in 0.5s reverse;
  transition: opactiy 1s;
}

@keyframes slide-in {
  from {
    transform: translateX(100px);
  }
  to {
    transform: translateX(0);
  }
}

.main {
  width: 70%;
  margin: auto;
  padding-top: 5rem;
  text-align: center;
}
</style>
