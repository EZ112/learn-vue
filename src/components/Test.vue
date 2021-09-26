<template>
  <h1>Hello, Vue :)</h1>
  <!-- <div v-if="showBooks">
    <p>{{ title }} = {{ author }} = {{ age }}</p>

    <button v-on:click="age++">Increase age</button>
    <button v-on:click="age--">Decrease age</button>
    <div @click="changeTitle('Oathbringer')">Change book title</div>
  </div> -->
  <div v-if="showBooks">
    <ul>
      <li v-for="book in books" :key="book.author">
        <img :src="book.img" :alt="book.title" />
        <h3>{{ book.title }}</h3>
        <p>{{ book.author }}</p>
      </li>
    </ul>
  </div>
  <button @click="toggleShowBooks">
    <span v-if="showBooks">Hide Books</span>
    <span v-else>Show Books</span>
  </button>
  <div v-show="showBooks">currently showBooks</div>

  <!-- mouse events -->
  <div class="box" @mouseover="handleEvent($event, 5)">mouseover (enter)</div>
  <div class="box" @mouseleave="handleEvent">mouseleave</div>
  <div class="box" @dblclick="handleEvent">double click</div>
  <div class="box" @mousemove="handleMouseMove">position - {{ x }} {{ y }}</div>

  <!-- attribute binding -->
  <div>
    <a v-bind:href="url">net ninja website</a>
  </div>
  <div>
    <a :href="url">net ninja website</a>
  </div>
  <!-- dynamic class -->
  <div v-if="showBooks">
    <ul>
      <li
        v-for="book in books"
        :key="book.author"
        :class="{ fav: book.isFav }"
        @click="toggleFav(book)"
      >
        <img :src="book.img" :alt="book.title" />
        <h3>{{ book.title }}</h3>
        <p>{{ book.author }}</p>
      </li>
    </ul>
  </div>

  <!-- computed properties -->
  <div v-if="showBooks">
    <ul>
      <li
        v-for="book in filteredBooks"
        :key="book.author"
        :class="{ fav: book.isFav }"
        @click="toggleFav(book)"
      >
        <img :src="book.img" :alt="book.title" />
        <h3>{{ book.title }}</h3>
        <p>{{ book.author }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "https://www.thenetninja.co.uk",
      showBooks: true,
      books: [
        {
          title: "name of the wind",
          author: "patrick rothfuss",
          img: "./src/assets/logo.png",
          isFav: true,
        },
        {
          title: "the way of kings",
          author: "brandon sanderson",
          img: "./src/assets/logo.png",
          isFav: false,
        },
        {
          title: "the final empire",
          author: "brandon rothfuss",
          img: "./src/assets/logo.png",
          isFav: true,
        },
      ],
      x: 0,
      y: 0,
    };
  },
  methods: {
    changeTitle(title) {
      this.title = title;
    },
    toggleShowBooks() {
      this.showBooks = !this.showBooks;
    },
    handleEvent(e, num) {
      console.log(e, e.type);
      if (num) {
        console.log(num);
      }
    },
    handleMouseMove(e) {
      this.x = e.offsetX;
      this.y = e.offsetY;
    },
    toggleFav(book) {
      book.isFav = !book.isFav;
    },
  },
  computed: {
    filteredBooks() {
      return this.books.filter((book) => book.isFav);
    },
  },
};
</script>

<style>
.box {
  padding: 100px 0;
  width: 400px;
  text-align: center;
  background: #ddd;
  margin: 20px;
  display: inline-block;
}
li {
  list-style-type: none;
  background: #fff;
  margin: 20px auto;
  padding: 10px 20px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
li.fav {
  background: #ff93d2;
  color: white;
}
</style>