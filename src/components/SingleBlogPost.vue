<template>
  <div>
    <h1>{{ post.title }}</h1>
    <p>{{ post.author }}</p>
    <p>{{ post.date_published }}</p>
    <p>{{ post.content }}</p>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  props: {
    id: {
      type: String,
      required: true,
    },
  },
  setup(props) {
    const post = ref(null);

    const fetchPost = async () => {
      try {
        const response = await fetch(
          `https://dummyapi.online/api/blogposts/${props.id}`
        );
        if (!response.ok) {
          throw new Error(`API request failed with status ${response.status}`);
        }
        const data = await response.json();
        post.value = data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    };

    onMounted(fetchPost);

    return { post };
  },
};
</script>
