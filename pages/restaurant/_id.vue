<template>
    <div>
        <img :src="restaurant.thumbnail">
        <p class="title">
          {{ restaurant.name }}
        </p>
        <p class="content">
          {{ restaurant.description }}
        </p>
    </div>
</template>

<script>
import axios from "axios";

export default {

async asyncData({ params }) {
  const response = await axios.get(
    `https://www.master-7rqtwti-mq325chc5wubq.us-2.platformsh.site/Restaurant-Khs`
  );
  const restaurantData = response.data.map(item => {
    return {
      id: item.id,
      name: item.Name,
      description: item.description,
      thumbnail: item.photo.length
        ? `https://www.master-7rqtwti-mq325chc5wubq.us-2.platformsh.site${item.photo[0].url}`
        : "http://placehold.jp/400x300.png?text=No Image"
    };
  }).find(item => item.id == params.id);

  return {
    restaurant: restaurantData
  };
}

}
</script>

<style scoped>

</style>
