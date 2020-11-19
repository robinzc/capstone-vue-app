<template>
  <div class="login">
    <section class="lg bg-secondary">
      <div class="container">
        <div class="section-title-area text-center mb-70">
          <h1 class="section-title">Traverse Login</h1>
          <h4 class="section-title">
            Expand your travel universe
          </h4>
        </div>
        <section
          class="sm bg-img bg-fixed"
          style="background-image: url(/assets/images/main-header.jpg)"
        >
          <div class="overlay"></div>
          <div class="container">
            <div class="row">
              <div class="container">
                <form
                  class="validation-inner"
                  id="form-validation4"
                  novalidate="novalidate"
                  v-on:submit.prevent="submit()"
                >
                  <div class="row">
                    <div class="col-12">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-envelope text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="text"
                          class="form-control w-icon-left"
                          id="contact-subject4"
                          name="inputSubject4"
                          placeholder="Email"
                          equired=""
                          aria-required="true"
                          v-model="email"
                        />
                      </div>
                      <!-- / form-group -->
                    </div>
                    <!-- / column -->
                    <div class="col-12">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-unlock-alt text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="text"
                          class="form-control w-icon-left"
                          id="contact-name4"
                          name="inputName4"
                          placeholder="Password"
                          required=""
                          aria-required="true"
                          v-model="password"
                        />
                      </div>
                      <!-- / input-group -->
                    </div>
                    <!-- / column -->
                  </div>
                  <!-- / row -->

                  <button
                    type="submit"
                    class="btn btn-primary-gradient btn-submit"
                  >
                    <i class="fas fa-sign-in-alt mr-5"></i> Log in
                  </button>
                </form>
              </div>
            </div>
            <!-- / row -->
          </div>
          <!-- / container -->
        </section>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      email: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/api/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("user_id", response.data.user_id);
          this.$router.push(`/users/${response.data.user_id}`);
        })
        .catch((error) => {
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>
