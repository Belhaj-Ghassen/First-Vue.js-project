<template>
  <div class="main-container">
    <div class="h1-container">
      <h1>Hello Vue.js project</h1>
    </div>
    <div class="msg-container">
      <span>Message: {{ msg }}</span>
    </div>
    <div :id="dynamicId" class="dynamic-div">This is a dynamic div with ID: {{ dynamicId }}</div>
    <button @click="changeId">Change ID</button>
    <p class="v-html-container">Using v-html directive: <span v-html="rawHtml" style="color: royalblue;"></span></p>
    <div><button @click="increment">{{ count }}</button></div>
    <div :class="classObject">HELLO</div>
    <div :style="styleObject">BINDING INLINE STYLES USING OBJECTS</div>
    <button @click="awesome = !awesome">click here !</button>
    <h1 v-if="awesome">Vue is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>
    <div v-if="type === 'A'">v-if</div>
    <div v-else-if="type === 'B'">B</div>
    <div v-else-if="type === 'C'">C</div>
    <div v-else>Not A/B/C</div>
    <h1 v-show="ok">v-show</h1>
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ parentMessage }} - {{ index }} - {{ item.message }}
      </li>
    </ul>
    <ul>
      <li v-for="(value, key, index) in myObject" :key="index">
        {{ index }} / {{ key }}: {{ value }}
      </li>
    </ul>
    <span v-for="n in 4" :key="n">{{ n }}</span>
    <ul>
      <li v-for="n in evenNumbers" :key="n">{{ n }}</li>
    </ul>
    <ul v-for="numbers in sets">
      <li v-for="n in even(numbers)">{{ n }}</li>
    </ul>
    <button @click="greet">Greet</button>
    <p>le message est :{{message}}</p>
    <input v-model="message" placeholder="edit me !"/>
    <div>Selected: {{ selected }}</div>
    <select v-model="selected">
      <option disabled value="">Please select one</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <h1>Here are many child components!</h1>
    <ButtonCounter />
    <ButtonCounter />
    <ButtonCounter />
    <div :style="{ fontSize: postFontSize + 'em' }">
    <BlogPost
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      @enlarge-text="postFontSize += 0.1"></BlogPost>
    </div>
    <AlertBox>
      Something bad happened 
    </AlertBox>
    <CustomInput v-model="texte" /> {{ texte }}
    <br>
    <MouseTracker v-slot="{ x, y }">
      Mouse is at: {{ x }}, {{ y }}
    </MouseTracker>
    <a href="#/">Home</a> |
  <a href="#/about">About</a> |
  <a href="#/non-existent-path">Broken Link</a>
  <component :is="currentView" />
  </div>
</template>

<script>
import ButtonCounter from './components/ButtonCounter.vue';
import BlogPost from './components/BlogPost.vue';
import AlertBox from './components/AlertBox.vue';
import CustomInput from './components/CustomInput.vue';
import MouseTracker from './components/MouseTracker.vue';
import Home from './components/Home.vue';
import About from './components/About.vue';
import NotFound from './components/NotFound.vue';
const routes = {
  '/': Home,
  '/about': About
}


export default {
  components: {
    ButtonCounter,
    BlogPost,
    AlertBox,
    CustomInput,
    MouseTracker,
    Home,
    About,
    NotFound,
  },
  data() {
    return {
      msg: 'we are building a new project!',
      rawHtml: '1234',
      dynamicId: 'initialId',
      idList: ['initialId', 'newId1', 'newId2', 'newId3'],
      currentIndex: 0,
      count: 0,
      isActive: true,
      awesome: true,
      ok: true,
      type: 'A',
      parentMessage: 'NeoLedge',
      items: [{ message: 'Vue.js' }, { message: '.Net' }],
      numbers: [1, 2, 3, 4, 5],
      sets: [[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]],
      name: 'Vue.js',
      message: '',
      selected: '',
      texte:'hello Vue.js',
      currentPath:window.location.hash,
      myObject: {
        title: 'How to do lists in Vue',
        author: 'Jane Doe',
        publishedAt: '2016-04-10',
      },
      styleObject: {
        color: 'red',
        fontSize: '13px',
        border: '5px solid #fafad2',
      },
      posts: [
        { id: 1, title: 'My journey with Vue' },
        { id: 2, title: 'Blogging with Vue' },
        { id: 3, title: 'Why Vue is so fun' }
      ],
      postFontSize: 1,
    };
  },
  computed: {
    classObject() {
      return {
        active: this.isActive,
      };
    },
    evenNumbers() {
      return this.numbers.filter((n) => n % 2 === 0);
    },
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    },
  },
  methods: {
    changeId() {
      this.currentIndex = (this.currentIndex + 1) % this.idList.length;
      this.dynamicId = this.idList[this.currentIndex];
    },
    increment() {
      this.count++;
    },
    even(numbers) {
      return numbers.filter((number) => number % 2 === 0);
    },
    greet(event) {
      alert(`Hello ${this.name}!`);
      if (event) {
        alert(event.target.tagName);
      }
    },
  },
  mounted() {
    this.increment();
    window.addEventListener('hashchange', () => {
		  this.currentPath = window.location.hash
		});
  },
};
</script>

<style scoped>
.main-container {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

.h1-container {
  width: 100%;
  color: black;
  background-color: rgb(55, 184, 104); /* Background color only for h1 */
  text-align: center;
  padding: 20px;
}

.msg-container {
  margin-top: 20px; /* Adjust spacing between h1 and msg */
}

.dynamic-div {
  margin-top: 20px; /* Adjust spacing */
  padding: 10px;
  border: 1px solid black;
}

button {
  margin-top: 20px; /* Adjust spacing */
  padding: 10px 20px;
  background-color: darkblue;
  color: white;
  border: none;
  cursor: pointer;
}

#initialId {
  background-color: lightcyan;
  color: black;
}

#newId1 {
  background-color: lightgreen;
  color: black;
}

#newId2 {
  background-color: lightcoral;
  color: black;
}

#newId3 {
  background-color: #fafad2;
  color: black;
}

.v-html-container {
  position: absolute;
  top: 125px;
  right: 50px;
}

.active {
  color: aliceblue;
  border: 5px solid #1f8041;
  padding: 10px;
}

</style>
