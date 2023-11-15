<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const posts = ref([]);
    onMounted(() => {
      const apiUrl = 'https://maqison.com/wp-json/wp/v2/posts?categories=1,10';
      axios.get(apiUrl)
        .then(response => {
          posts.value = response.data;
        })
        .catch(error => {
          console.error('Error fetching WordPress data:', error);
        });
    });
    return {
      posts,
    };
  },
};

</script>

<template>
  <div>
    <h1>WordPress Posts</h1>
    <ul class="wd-post-container">
      <li v-for="post in posts" :key="post.id">
        <div v-html="post.content.rendered"></div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
