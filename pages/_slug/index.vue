<template>
  <div>
    <div v-for="item in items" v-bind:key="item.id">
      <nuxt-link :to="'blog/' + item.id">
        <h2>
          {{ item.name }}
        </h2>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      items: []
    };
  },
  async asyncData() {
    const { data } = await axios.get(
      "https://your.microcms.io/api/v1/blog",
      {
        headers: { "X-MICROCMS-API-KEY": process.env.API_KEY }
      }
    );
    return {
      items: data.contents
    };
  }
};
</script>