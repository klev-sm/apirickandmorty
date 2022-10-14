<template>
  <div id="card" class="card is-mobile">
    <br />
    <div class="card-image">
      <nav class="level">
        <div class="level-item has-text-centered">
          <figure class="image is-128x128">
            <img :src="image" />
          </figure>
        </div>
      </nav>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ name }}</p>
          <p class="subtitle is-6">Gênero: {{ gender }}</p>
        </div>
      </div>
      <div class="content">
        
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    gender: String,
    image: String,
  },
};
</script>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css";

#card {
  padding-top: 1%;
  margin-bottom: 1%;
}
</style>