<template>
  <div class="signup">
    <section class="lg bg-secondary">
      <div class="container">
        <div class="section-title-area text-center mb-70">
          <h1 class="section-title">Sign up with Traverse</h1>
          <h4 class="section-title">
            Start building your personal travel universe today!
          </h4>
        </div>
        <section
          class="xl bg-img bg-fixed"
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
                    <div class="col-md-6 sub-col-left">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-user text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="text"
                          class="form-control w-icon-left"
                          id="contact-name4"
                          name="inputName4"
                          placeholder="First name"
                          required=""
                          aria-required="true"
                          v-model="first_name"
                        />
                      </div>
                      <!-- / input-group -->
                    </div>
                    <!-- / column -->

                    <div class="col-md-6 sub-col-right">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-user text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="email"
                          class="form-control w-icon-left"
                          id="contact-email4"
                          name="inputEmail4"
                          placeholder="Last name"
                          required=""
                          aria-required="true"
                          v-model="last_name"
                        />
                      </div>
                      <!-- / input-group -->
                    </div>
                    <!-- / column -->

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
                    <div class="col-md-6 sub-col-left">
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

                    <div class="col-md-6 sub-col-right">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-lock text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="email"
                          class="form-control w-icon-left"
                          id="contact-email4"
                          name="inputEmail4"
                          placeholder="Password confirmation"
                          required=""
                          aria-required="true"
                          v-model="passwordConfirmation"
                        />
                      </div>
                      <!-- / input-group -->
                    </div>
                    <!-- / column -->

                    <div class="col-12">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-language text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="text"
                          class="form-control w-icon-left"
                          id="contact-subject4"
                          name="inputSubject4"
                          placeholder="What languages do you speak?"
                          v-model="languages_spoken"
                        />
                      </div>
                      <!-- / form-group -->
                    </div>
                    <div class="col-12">
                      <div class="input-group">
                        <div class="input-group-prepend">
                          <span class="input-group-text"
                            ><i class="fas fa-portrait text-primary"></i
                          ></span>
                        </div>
                        <!--/ input-group-prepend -->
                        <input
                          type="text"
                          class="form-control w-icon-left"
                          id="contact-subject4"
                          name="inputSubject4"
                          placeholder="Please enter a profile picture url"
                          v-model="image_url"
                        />
                      </div>
                      <!-- / form-group -->
                    </div>
                  </div>
                  <!-- / row -->

                  <button
                    type="submit"
                    class="btn btn-primary-gradient btn-submit"
                  >
                    <i class="fas fa-user-plus mr-5"></i> Sign up!
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
      first_name: "",
      last_name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      languages_spoken: "",
      image_url: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        first_name: this.first_name,
        last_name: this.last_name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
        languages_spoken: this.languages_spoken,
        image_url: this.image_url,
      };

      axios
        .post("/api/users", params)
        .then((response) => {
          axios.post("/api/sessions", params).then((response) => {
            axios.defaults.headers.common["Authorization"] =
              "Bearer " + response.data.jwt;
            localStorage.setItem("jwt", response.data.jwt);
            localStorage.setItem("user_id", response.data.user_id);
            this.$router.push(`/users/${response.data.user_id}/edit`);
          });
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
