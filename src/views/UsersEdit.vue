<template>
  <div class="users-edit">
    <div class="container">
      <div class="section-title-area text-center mb-70">
        <br />

        <h2 class="section-title">
          {{ user.first_name }} {{ user.last_name }}
        </h2>
        <h5 class="section-title">Edit profile</h5>
      </div>
    </div>
    <div class="container">
      <form
        class="validation-inner"
        id="form-validation4"
        novalidate="novalidate"
        v-on:submit.prevent="updateUser()"
      >
        <div class="row">
          <div class="col-md-6 sub-col-left">
            <div class="input-group">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fas fa-envelope fs-20 text-primary"></i
                ></span>
              </div>
              <!--/ input-group-prepend -->
              <input
                type="text"
                class="form-control w-icon-left"
                id="contact-email4"
                name="inputEmail4"
                placeholder="Email"
                required=""
                v-model="user.email"
              />
            </div>
            <!-- / input-group -->
          </div>
          <!-- / column -->

          <div class="col-md-6 sub-col-right">
            <div class="input-group">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fas fa-portrait fs-22 text-primary"></i
                ></span>
              </div>
              <!--/ input-group-prepend -->
              <input
                type="email"
                class="form-control w-icon-left"
                id="contact-email4"
                name="inputEmail4"
                placeholder="Profile picture url"
                required=""
                v-model="user.image_url"
              />
            </div>
            <!-- / input-group -->
          </div>
          <!-- / column -->

          <div class="col-12">
            <div class="input-group">
              <div class="input-group-prepend">
                <span class="input-group-text"
                  ><i class="fas fa-language fs-22 text-primary"></i
                ></span>
              </div>
              <!--/ input-group-prepend -->
              <input
                type="text"
                class="form-control w-icon-left"
                id="contact-subject4"
                name="inputSubject4"
                placeholder="Languages spoken"
                v-model="user.languages_spoken"
              />
            </div>
            <!-- / form-group -->
          </div>
          <!-- / column -->
        </div>
        <!-- / row -->

        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>

        <div class="section-title">
          <section class="lg bg-secondary">
            <div class="container">
              <div class="section-title-area text-center mb-60">
                <h3 class="section-title">
                  Complete your profile
                </h3>

                <div>
                  <div class="container">
                    <h5 class="section-title">
                      Select the cities you have visited or lived in.
                    </h5>
                    <div class="col-md-12 tablet-top">
                      <multiselect
                        v-model="selectedCities"
                        :options="cityOptions"
                        :multiple="true"
                        :close-on-select="false"
                        :clear-on-select="false"
                        :preserve-search="true"
                        placeholder="Select your cities"
                        label="name"
                        track-by="name"
                        :preselect-first="true"
                      >
                        <template
                          slot="selection"
                          slot-scope="{ values, isOpen }"
                          ><span
                            class="multiselect__single"
                            v-if="values.length &amp;&amp; !isOpen"
                            >{{ values.length }} cities selected</span
                          ></template
                        >
                      </multiselect>
                    </div>
                  </div>
                  <!-- {{ selectedCities }} -->
                  <br />
                  <h5 class="section-title">
                    Check the box that indicates your knowledge of each city
                    you've chosen.
                  </h5>
                  <br />
                  <div class="col-md-12">
                    <div class="row">
                      <div
                        class="col-sm-6 col-md-3 tablet-top-30 text-center"
                        v-for="(city, index) in selectedCities"
                      >
                        <div class="card">
                          <div class="card-body radio radio-primary">
                            <br />

                            <h5 class="card-title fw-bold mb-10 text-primary">
                              {{ city.name }}
                            </h5>
                            <input
                              type="radio"
                              :id="city.id"
                              :value="{
                                city_id: city.id,
                                current_living: true,
                              }"
                              v-model="cityAssociations[index]"
                            />
                            <label class="mb-10" :for="city"
                              ><span>I live here now.</span></label
                            >

                            <input
                              type="radio"
                              :id="city.id"
                              :value="{ city_id: city.id, lived: true }"
                              v-model="cityAssociations[index]"
                            />
                            <label class="mb-10" :for="city"
                              ><span>I used to live here.</span></label
                            >

                            <input
                              type="radio"
                              :id="city.id"
                              :value="{ city_id: city.id, visited: true }"
                              v-model="cityAssociations[index]"
                            />
                            <label class="mb-10" :for="city"
                              ><span>I've visited here.</span></label
                            >

                            <input
                              type="radio"
                              :id="city.id"
                              :value="{
                                city_id: city.id,
                                current_visiting: true,
                              }"
                              v-model="cityAssociations[index]"
                            />
                            <label class="mb-10" :for="city"
                              ><span>I'm visiting here now.</span></label
                            >
                          </div>
                          <!-- / card-body -->
                        </div>
                        <!-- / card -->
                      </div>
                      <!-- / column -->
                    </div>
                  </div>
                  <!-- <div class="container">
                    <div class="btn-group m-y-5 ml-10 mr-20">
                      <div class="radio radio-primary">
                        <div v-for="(city, index) in selectedCities">
                          <h5>{{ city.name }}</h5>
                          <input
                            type="radio"
                            :id="city.id"
                            :value="{ city_id: city.id, current_living: true }"
                            v-model="cityAssociations[index]"
                          />
                          <label class="mb-10" :for="city"
                            ><span>I live here now.</span></label
                          >
                          <br />
                          <input
                            type="radio"
                            :id="city.id"
                            :value="{ city_id: city.id, lived: true }"
                            v-model="cityAssociations[index]"
                          />
                          <label class="mb-10" :for="city"
                            ><span>I used to live here.</span></label
                          >
                          <br />
                          <input
                            type="radio"
                            :id="city.id"
                            :value="{ city_id: city.id, visited: true }"
                            v-model="cityAssociations[index]"
                          />
                          <label class="mb-10" :for="city"
                            ><span>I've visited here.</span></label
                          >
                          <br />
                          <input
                            type="radio"
                            :id="city.id"
                            :value="{
                              city_id: city.id,
                              current_visiting: true,
                            }"
                            v-model="cityAssociations[index]"
                          />
                          <label class="mb-10" :for="city"
                            ><span>I'm visiting here now.</span></label
                          >
                          <br />
                        </div>
                        
                      </div>
                    </div>
                  </div>
                  <br /> -->
                  <!-- <span>Associated cities: {{ cityAssociations }}</span> -->
                </div>
                <br />
                <input
                  type="submit"
                  class="btn btn-primary-gradient"
                  value="Update my profile"
                />
                <br />
                <br />
                <span v-if="user.id == $parent.getUserId()">
                  <button
                    class="btn btn-xs btn-info m-5 pill"
                    v-on:click="destroyUser(user)"
                  >
                    <span class="fas fa-user-alt-slash mr-5"></span>
                    <span>Delete my profile</span>
                  </button>
                </span>
                <p class="mb-0">
                  <router-link
                    class="btn btn-xs btn-info m-5 pill"
                    :to="`/users/${user.id}`"
                    ><span class="fas fa-window-close mr-5"></span
                    ><span>Cancel</span></router-link
                  >
                </p>
              </div>
            </div>
          </section>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Multiselect from "vue-multiselect";

export default {
  components: { Multiselect },
  data: function() {
    return {
      user: {},
      errors: [],
      selectedCities: [],
      cityOptions: [],
      cityAssociations: [],
    };
  },

  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
      this.selectedCities = this.user.associated_cities.map((city) => {
        return { id: city.city_id, name: city.city_name };
      });
      this.user.associated_cities.forEach((city) => {
        if (city.current_living) {
          this.cityAssociations.push({
            city_id: city.city_id,
            current_living: true,
          });
        }
        if (city.current_visiting) {
          this.cityAssociations.push({
            city_id: city.city_id,
            current_visiting: true,
          });
        }
        if (city.visited) {
          this.cityAssociations.push({
            city_id: city.city_id,
            visited: true,
          });
        }
        if (city.lived) {
          this.cityAssociations.push({
            city_id: city.city_id,
            lived: true,
          });
        }
      });
    });
    axios.get("/api/cities").then((response) => {
      this.cityOptions = response.data;
      console.log(response.data);
    });
  },
  methods: {
    updateUser: function() {
      var params = {
        email: this.user.email,
        languages_spoken: this.user.languages_spoken,
        image_url: this.user.image_url,
        city_associations: this.cityAssociations,
      };
      axios
        .patch(`/api/users/${this.user.id}`, params)
        .then((response) => {
          this.$router.push(`/users/${this.user.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyUser: function(user) {
      if (
        confirm(
          "Are you sure you want to delete your profile? You will delete your entire Traverse account and will lose all data."
        )
      ) {
        axios.delete(`/api/users/${user.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/logout");
        });
      }
    },
  },
};
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

// Need to finish city association issues
