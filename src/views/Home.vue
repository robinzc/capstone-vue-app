<template>
  <div class="home">
    <header
      class="fh bg-img bg-fixed img-bottom text-center dark"
      style="background-image: url(/assets/images/main-header.jpg)"
    >
      <div class="container">
        <h1 class="page-title fixed-title mt-50">
          <span class="d-block">TRAVERSE</span>
          <span class="d-block fs-24 opc-75"
            >Inform your travels through your own trusted network</span
          >
        </h1>
      </div>
      <!-- / container -->
      <img
        src="/assets/images/angles.svg"
        alt=""
        class="header-image-bottom absolute bottom-0 left-0 right-0"
      />
    </header>
    <a
      href="#top"
      class="scroll-to-top is-hidden smooth-scroll"
      data-nav-status="toggle"
      ><i class="fas fa-chevron-up"></i
    ></a>
    <!-- <h1>{{ message }}</h1>
    <h2>Inform your travels through your own trusted network</h2>
    <br />
    <h2>Visualize your personal travel universe</h2> -->
    <!-- <button>
      <router-link :to="`/signup`"> Sign up</router-link>
    </button>
    <button>
      <router-link :to="`/login`"> Login</router-link>
    </button> -->
    <!-- <h3>Signup is free and easy!</h3> -->
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
