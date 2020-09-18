<template>
  <main role="main">
    <section class="jumbotron text-center">
      <div class="container">
        <h1 class="jumbotron-heading">My Album</h1>
        <p class="lead text-muted">{{message}}</p>
      </div>
    </section>
  </main>
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