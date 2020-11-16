<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>Inform your travels through your own trusted network</h2>
    <br />
    <h2>Visualize your personal travel universe</h2>
    <button>
      <router-link :to="`/signup`"> Sign up</router-link>
    </button>
    <button>
      <router-link :to="`/login`"> Login</router-link>
    </button>
    <h3>Signup is free and easy!</h3>
  </div>
</template>

<style></style>

<script>
export default {
  data: function() {
    return {
      message: "Traverse",
    };
  },
  created: function() {},
  methods: {},
};
</script>
