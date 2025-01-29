<script setup>
import { ref, reactive, computed } from 'vue';


// Reactive state
const age = ref(20);
const title = ref('Default Title');
const showBooks = ref(true)
const books = reactive([{ title: 'Book1', scope: 'SF', price: '200', lastRead: '11/01/2022', isFav: true }, { title: 'Book2', scope: 'SF', price: '200', lastRead: '11/01/2022' }])
const filteredBooks = computed(() => books.filter((book) => book.isFav))

// Function to increase age
const increaseAge = () => {
  age.value++;
};

const changeTitle = (newTitle) => {
  title = newTitle.target.value
}

const toggleFav = (book) => {
  book.isFav = !book.isFav
}

const toggleShowBooks = () => {
  showBooks.value = !showBooks.value
}

const handleEvent = () => {
  console.log("event")
}
</script>

<template>
  <main>
    <div>{{ age }}</div>
    <div v-if="showBooks">
      <div>
        <ul>
          <li v-for="book in filteredBooks" :class="{ fav: book.isFav }" @click="toggleFav(book)">
            <h1>{{ book.title }}</h1>
            <h3>{{ book.scope }}</h3>
            <label for="title">Change Title:</label>
            <input id="title" v-model="book.title" type="text" />
          </li>
        </ul>
      </div>
    </div>
    <div v-show="showBooks">
      <h1>{{ title }}</h1>
    </div>
    <button @click="increaseAge">Increase Age</button>

    <button @click="toggleShowBooks">
      <span v-if="!showBooks">ShowBooks</span>
      <span v-else>HideBooks</span>
    </button>

    <br>

    <div class="box" @mouseover="handleEvent($event, 5)">mouse over</div>
    <div class="box" @mouseleave="handleEvent">mouse leave</div>
    <div class="box" @dblclick="handleEvent">double click</div>
    <div class="box"></div>
    <!-- <input @change="changeTitle"></input> -->
  </main>
</template>

<style>
.box {
  padding: 100px 0;
  width: 400px;
  text-align: center;
  background: #ddd;
  margin: 20px;
  display: inline-block;
}

.fav {
  background: red;
}
</style>