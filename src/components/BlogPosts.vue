<script setup>
import { ref, onMounted, computed } from "vue";
import "animate.css";

import BlogCard from "./BlogCard.vue";

const posts = ref([]);
const selectedAuthor = ref("");
const activeAuthor = ref("");

const fetchData = async () => {
  try {
    const response = await fetch("https://dummyapi.online/api/blogposts");
    if (!response.ok) {
      throw new Error(`API request failed with status ${response.status}`);
    }
    const data = await response.json();
    // Create a copy of the data (recommended)
    posts.value = [...data];
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

const filteredPosts = computed(() => {
  if (!selectedAuthor.value) return posts.value; // Return all posts if no author selected
  return posts.value.filter((post) => post.author === selectedAuthor.value);
});

const truncateContent = (content) => {
  return content.split(" ").slice(0, 10).join(" ") + " ...";
}

// Fetch data on component mount
onMounted(fetchData);

defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div>
    <div v-if="posts.length">
      <div class="filter-area">
        <p>Filter posts by author:</p>

        <div class="filter-area__buttons">
          <div class="filter-area__buttons__authors">
            <button
              @click="
                selectedAuthor = 'Tim Burton';
                activeAuthor = 'Tim Burton';
              "
              :class="{ active: activeAuthor === 'Tim Burton' }"
              class="filter-area__buttons--default"
            >
              Tim Burton
            </button>
            <button
              @click="
                selectedAuthor = 'Sophia Carter';
                activeAuthor = 'Sophia Carter';
              "
              :class="{ active: activeAuthor === 'Sophia Carter' }"
              class="filter-area__buttons--default"
            >
              Sophia Carter
            </button>
            <button
              @click="
                selectedAuthor = 'John Seele';
                activeAuthor = 'John Seele';
              "
              :class="{ active: activeAuthor === 'John Seele' }"
              class="filter-area__buttons--default"
            >
              John Seele
            </button>
            <button
              @click="
                selectedAuthor = 'Alex Johnson';
                activeAuthor = 'Alex Johnson';
              "
              :class="{ active: activeAuthor === 'Alex Johnson' }"
              class="filter-area__buttons--default"
            >
              Alex Johnson
            </button>
            <button
              @click="
                selectedAuthor = 'James Brown';
                activeAuthor = 'James Brown';
              "
              :class="{ active: activeAuthor === 'James Brown' }"
              class="filter-area__buttons--default"
            >
              James Brown
            </button>
            <button
              @click="
                selectedAuthor = 'Michael Brown';
                activeAuthor = 'Michael Brown';
              "
              :class="{ active: activeAuthor === 'Michael Brown' }"
              class="filter-area__buttons--default"
            >
              Michael Brown
            </button>
            <button
              @click="
                selectedAuthor = 'Lois Lane';
                activeAuthor = 'Lois Lane';
              "
              :class="{ active: activeAuthor === 'Lois Lane' }"
              class="filter-area__buttons--default"
            >
              Lois Lane
            </button>
          </div>
          <button
            @click="
              selectedAuthor = '';
              activeAuthor = '';
            "
            class="clear-btn"
          >
            Clear Filter
          </button>
        </div>
      </div>

      <ul class="posts">
        <li
          v-for="post in filteredPosts"
          :key="post.id"
          class="animate__animated animate__fadeIn animate__faster"
        >
          <BlogCard>
            <template #blog-title>{{ post.title }}</template>
            <template #blog-author>{{ post.author }}</template>
            <template #blog-date>{{ post.date_published }}</template>
            <template #blog-content>{{ truncateContent(post.content) }}</template>
          </BlogCard>
        </li>
      </ul>
    </div>
    <p v-else>Loading data...</p>
  </div>
</template>

<style scoped></style>
