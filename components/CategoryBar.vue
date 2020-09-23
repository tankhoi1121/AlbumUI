<template>
  <section class="jumbotron text-center">
    <div class="container d-flex justify-content-between">
      <h1 class="jumbotron-heading">My Album</h1>
      <p class="lead text-muted">{{message}}</p>
      <div class="row">
        <div class="col-md-3 card mb-4 box-shadow">
          <nuxt-link to="/">All</nuxt-link>
        </div>
        <div class="col-md-3 card mb-4 box-shadow">
          <nuxt-link to="/people">People</nuxt-link>
        </div>
        <div class="col-md-3 card mb-4 box-shadow">
          <nuxt-link to="/landscape">Landscape</nuxt-link>
        </div>
        <div class="col-md-3 card mb-4 box-shadow">
          <nuxt-link to="/tech">Tech</nuxt-link>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      message: "Welcome to the world of atractive magic",
    };
  },
};
</script>