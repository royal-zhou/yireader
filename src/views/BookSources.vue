<template>
  <div class="bookSource">
    <BookSourceInfo v-for="(booksource, index) in bookSources" :key="index"
      :name="booksource.name" :url="booksource.url" />
  </div>
</template>

<script>
import BookSourceInfo from "@/components/BookSourceInfo"
import {booksources} from "@/api.js"

export default {
  name: "BookSources",
  components: {
    BookSourceInfo
  },
  data() {
    return {
      bookSources: [],
      fetching: true,
    };
  },
  created() {
    this.fetchBookSources();
  },
  watch: {
    $route() {
      this.fetchBookSources();
    }
  },
  methods: {
    fetchBookSources() {
      console.log("fetchBookSources");
      booksources().then(res => {
        console.log("fetchBookSources result:", res.data);
        this.bookSources = res.data;
        this.fetching = false;
      }).catch(res => {
        console.error(res);
      });
    }
  },
  title: "书源 - 易读"
}
</script>
