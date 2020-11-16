<template>
  <div class="signup">
    <div
      class="full-height relative p-y-30 v-center bg-img"
      style="background-image: url(../assets/images/map-pins.jpg)"
    >
      <div class="overlay-dark"></div>
      <div class="container p-y-70">
        <div
          class="row no-gutters promo-img-lg promo-img promo-box-img-left no-transform"
        >
          <div
            class="col-lg-6 bg-img box-bg-image"
            style="background-image: url(../assets/images/map-pins.jpg); min-height: 400px;"
          >
            &nbsp;
            <div class="section-title-area text-center">
              <br />
              <h1 class="text-white">
                <span class="d-block">Sign up with Traverse</span>
              </h1>
              <br />
            </div>
          </div>
          <!-- / column -->
          <div class="col-lg-6">
            <ul>
              <li class="text-danger" v-for="error in errors">{{ error }}</li>
            </ul>
            <div class="promo-box p-y-80 mb-0 bg-light">
              <span class="text-center">
                <h3 class="text-black">
                  Start building your personal travel universe today!
                </h3>
              </span>
              <div class="card card-w-bar mb-15">
                <div class="card-body">
                  <ul
                    class="nav nav-tabs text-center tab-w-bar bg-primary-gradient"
                    role="tablist"
                  >
                    <li class="nav-item">
                      <a
                        class="nav-link"
                        data-toggle="tab"
                        href="#tab-register"
                        role="tab"
                        ><i class="fas fa-user mr-5"></i>Sign up</a
                      >
                    </li>
                    <li class="nav-item">
                      <a
                        class="nav-link active"
                        data-toggle="tab"
                        href="#tab-sign-in"
                        role="tab"
                        ><i class="fas fa-sign-in-alt mr-5"></i> Login</a
                      >
                    </li>
                  </ul>
                  <!-- / nav tabs -->
                  <div class="tab-content">
                    <div
                      class="tab-pane fade show active mt-30 p-15"
                      id="tab-sign-in"
                      role="tabpanel"
                    >
                      <form
                        class="validation-inner"
                        id="login-form3"
                        novalidate="novalidate"
                      >
                        <div class="form-group">
                          <input
                            type="text"
                            class="form-control"
                            name="emailLogin3"
                            placeholder=" Email"
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                          />
                        </div>
                        <!-- / form-group -->

                        <div class="form-group">
                          <input
                            type="password"
                            class="form-control"
                            name="passwordLogin3"
                            placeholder=" Password"
                            required=""
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            aria-required="true"
                          />
                        </div>
                        <!-- / form-group -->

                        <div class="row v-center mt-15">
                          <div class="col-xl-5 tablet-xl-top">
                            <div class="checkbox checkbox-primary ml-10">
                              <label class="hidden"
                                ><input type="checkbox"
                              /></label>
                              <input id="checkbox-login2" type="checkbox" />
                              <label for="checkbox-login2">Remember Me</label>
                            </div>
                            <!-- / checkbox -->
                          </div>
                          <!-- / column -->
                          <div class="col-xl-7 text-right">
                            <button
                              type="submit"
                              class="btn btn-primary-gradient tablet-xl-fw"
                            >
                              <i class="fas fa-sign-in-alt mr-5"></i> Sign In
                            </button>
                          </div>
                          <!-- / column -->
                        </div>
                        <!-- / row -->
                      </form>
                      <!-- / login-form -->
                    </div>
                    <!-- / tab-pane -->
                    <div
                      class="tab-pane fade mt-30 p-15"
                      id="tab-register"
                      role="tabpanel"
                    >
                      <form
                        class="validation-inner"
                        id="register-form3"
                        novalidate="novalidate"
                      >
                        <div class="form-group">
                          <input
                            type="text"
                            class="form-control"
                            name="usernameRegister3"
                            placeholder=" First name"
                            required=""
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            aria-required="true"
                            v-model="first_name"
                          />
                        </div>
                        <div class="form-group">
                          <input
                            type="text"
                            class="form-control"
                            name="usernameRegister3"
                            placeholder=" Last name"
                            required=""
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            aria-required="true"
                            v-model="last_name"
                          />
                        </div>

                        <div class="form-group">
                          <input
                            type="text"
                            class="form-control"
                            name="usernameRegister3"
                            placeholder=" What languages do you speak?"
                            required=""
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            aria-required="true"
                            v-model="languages_spoken"
                          />
                        </div>

                        <div class="form-group">
                          <input
                            type="url"
                            class="form-control"
                            name="usernameRegister3"
                            placeholder=" Please enter a profile photo url"
                            required=""
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            aria-required="true"
                            v-model="image_url"
                          />
                        </div>
                        <div class="form-group">
                          <input
                            type="email"
                            class="form-control"
                            name="emailRegister3"
                            placeholder=" Email"
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            v-model="email"
                          />
                        </div>
                        <!-- / form-group -->

                        <!-- / form-group -->
                        <div class="form-group">
                          <input
                            type="password"
                            id="passwordRegister3"
                            class="form-control"
                            name="passwordRegister3"
                            placeholder=" Password"
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            v-model="password"
                          />
                        </div>
                        <!-- / form-group -->
                        <div class="form-group">
                          <input
                            type="password"
                            class="form-control"
                            name="passwordRegisterConfirm3"
                            placeholder=" Confirm Password"
                            required=""
                            style="font-family:'Font Awesome 5 Free', sans-serif !important; font-weight: 400"
                            aria-required="true"
                            v-model="passwordConfirmation"
                          />
                        </div>
                        <!-- / form-group -->

                        <div class="row v-center">
                          <!-- / column -->

                          <div class="col-xl-5 text-right">
                            <button
                              type="submit"
                              class="btn btn-primary-gradient tablet-xl-fw"
                            >
                              <i class="fas fa-sign-in-alt mr-5"></i> Sign up!
                            </button>
                          </div>
                          <!-- / column -->
                        </div>
                        <!-- / row -->
                      </form>
                      <!-- / register-form -->
                    </div>
                    <!-- / tab-pane -->
                  </div>
                  <!-- / tab-content -->
                </div>
                <!-- / card-body -->
              </div>
              <!-- / promo-box -->
            </div>
            <!-- promo-box -->
          </div>
          <!-- / column -->
        </div>
        <!-- / row -->
      </div>
      <!-- / container -->
      <p class="absolute bottom-30 x-0 text-center dark">
        <a href="../index.html" class="text-link fs-16 m-x-15">Home</a>
        <a href="../components.html" class="text-link fs-16 m-x-15"
          >Components</a
        >
        <a href="../sections.html" class="text-link fs-16 m-x-15">Sections</a>
        <a href="../templates.html" class="text-link fs-16 m-x-15">Templates</a>
      </p>
    </div>
    <!-- <form v-on:submit.prevent="submit()">
      <h1>Sign Up with Traverse</h1>
      <h3>Start building your personal travel universe today!</h3> -->

    <!-- <div class="form-group">
        <label>First name:</label>
        <input type="text" class="form-control" v-model="first_name" />
      </div>
      <div class="form-group">
        <label>Last name:</label>
        <input type="text" class="form-control" v-model="last_name" />
      </div>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email" />
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password" />
      </div>
      <div class="form-group">
        <label>Password confirmation:</label>
        <input
          type="password"
          class="form-control"
          v-model="passwordConfirmation"
        />
      </div>
      <div class="form-group">
        <label>What languages do you speak?</label>
        <input type="text" class="form-control" v-model="languages_spoken" />
      </div>
      <div class="form-group">
        <label>Please enter a profile picture url: </label>
        <input type="url" class="form-control" v-model="image_url" />
      </div>
      <input type="submit" class="btn btn-primary" value="Sign up!" /> -->
    <!-- </form> -->
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
