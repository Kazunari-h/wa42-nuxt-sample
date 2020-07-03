<template>
  <div class="container">
    <div class="columns is-multiline">
      <div v-for="restaurant in restaurants" :key="restaurant.id" class="column is-4">
        <nuxt-link :to="`/restaurant/${restaurant.id}`">
          <div class="card">
            <div class="card-image">
              <figure class="image is-4by3">
                <img :src="restaurant.thumbnail" />
              </figure>
            </div>
            <div class="card-content">
              <h1 class="title is-5">{{ restaurant.name }}</h1>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  components: {},
  async asyncData({ app }) {
    const response = await axios.get(
      `https://www.master-7rqtwti-mq325chc5wubq.us-2.platformsh.site/Restaurant-Khs`
    );

    const restaurantsData = response.data.map(item => {
      return {
        id: item.id,
        name: item.Name,
        description: item.description,
        thumbnail: item.photo.length
          ? `https://www.master-7rqtwti-mq325chc5wubq.us-2.platformsh.site${item.photo[0].url}`
          : "http://placehold.jp/400x300.png?text=No Image"
      };
    });

    return {
      restaurants: restaurantsData
    };
  }
};
</script>

<style scoped>
</style>