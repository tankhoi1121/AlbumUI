<template>
  <section class="jumbotron text-center">
    <div class="container justify-content-between">
      <h1 class="jumbotron-heading">My Album</h1>
      <p class="lead text-muted">{{ message }}</p>
      <div class="row h-35px">
        <div class="col-md-2 mr-2 box-shadow btn-dark rounded">
          <nuxt-link to="/"
            ><p class="text-sm-center h5">All &nbsp;</p></nuxt-link
          >
        </div>
        <div class="col-md-2 mr-2 box-shadow btn-dark rounded">
          <nuxt-link to="/people"
            ><p class="text-sm-center h5">People &nbsp;</p></nuxt-link
          >
        </div>
        <div class="col-md-2 mr-2 box-shadow btn-dark rounded">
          <nuxt-link to="/landscape"
            ><p class="text-sm-center h5">Landscape &nbsp;</p></nuxt-link
          >
        </div>
        <div class="col-md-2 mr-2 box-shadow btn-dark rounded">
          <nuxt-link to="/tech"
            ><p class="text-sm-center h5">Tech &nbsp;</p></nuxt-link
          >
        </div>
      </div>
    </div>
  </section>
</template>
<style>
.h-35px {
  height: 35px;
}
</style>
<script>
export default {
  data() {
    return {
      message: "Welcome to the world of atractive magic",
    };
  },
};
</script>