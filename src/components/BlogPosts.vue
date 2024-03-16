<script setup>
import { ref, onMounted, computed } from 'vue'
import 'animate.css'

const posts = ref([])
const selectedAuthor = ref('')

const fetchData = async () => {
  try {
    const response = await fetch('https://dummyapi.online/api/blogposts')
    if (!response.ok) {
      throw new Error(`API request failed with status ${response.status}`)
    }
    const data = await response.json()
    // Create a copy of the data (recommended)
    posts.value = [...data]
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

const filteredPosts = computed(() => {
  if (!selectedAuthor.value) return posts.value // Return all posts if no author selected
  return posts.value.filter((post) => post.author === selectedAuthor.value)
})

// Fetch data on component mount
onMounted(fetchData)

defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div>
    <h1 class="green">{{ msg }}</h1>
    <div v-if="posts.length">
      <h2>Fetched Posts:</h2>

      <div class="filter-buttons">
        <button @click="selectedAuthor = 'Tim Burton'">Tim Burton</button>
        <button @click="selectedAuthor = 'Sophia Carter'">Sophia Carter</button>
        <button @click="selectedAuthor = 'John Seele'">John Seele</button>
        <button @click="selectedAuthor = 'James Brown'">James Brown</button>
        <button @click="selectedAuthor = ''">Clear Filter</button>
      </div>

      <ul class="posts">
        <!-- <li v-for="post in filteredPosts" :key="post.id">
          <h3>{{ post.title }}</h3>
          <p>{{ post.author }}</p>
          <p>{{ post.content }}</p>
        </li> -->
        <!-- <transition-group name="list" tag="ul" class="posts"> -->
        <li
          v-for="post in filteredPosts"
          :key="post.id"
          class="animate__animated animate__fadeIn animate__faster"
        >
        <img src="../assets/pexels-blog.jpg" alt="Blog image" class="blog-img">
          <h3>{{ post.title }}</h3>
          <p class="author">{{ post.author }}</p>
          <p>{{ post.content }}</p>
        </li>
        <!-- </transition-group> -->
      </ul>
    </div>
    <p v-else>Loading data...</p>
  </div>
</template>

<style scoped>
button {
  padding: 12px 32px;
  font-size: 16px;
  border-radius: 8px;
}

.filter-buttons button {
  padding: 8px 16px;
  margin-right: 5px;
  border: 1px solid #ddd;
  border-radius: 4px;
  cursor: pointer;
  background-color: #f5f5f5;
}

.filter-buttons button.active {
  background-color: #eee;
}

/* .list-move {
  transition: transform 200ms;
} */
</style>
