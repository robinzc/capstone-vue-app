<template>
  <div class="users-index">
    <div class="right col-md-3 text-right">
      <div class="nav-item m-0 p-0">
        <div class="input-group mb-0">
          <input
            type="text"
            class="form-control pill"
            placeholder="Search by name"
            v-model="nameFilter"
            list="names"
          />
          <datalist id="names">
            <option v-for="user in users"
              >{{ user.first_name }} {{ user.last_name }}</option
            >
          </datalist>
          <span class="input-group-btn">
            <button
              class="btn btn-xs btn-icon btn-circle btn-dark overlapping-btn"
              type="button"
            >
              <i class="fas fa-search"></i>
            </button>
          </span>
        </div>
        <!-- / input-group -->
      </div>
      <!-- / nav-item -->
    </div>
    <section class="lg bg-secondary">
      <div class="container">
        <div class="section-title-area text-center mb-70">
          <h1 class="section-title">THE TRAVEL UNIVERSE</h1>
          <h4 class="section-title">Find your travel network.</h4>
          <h5 class="section-title">
            Connect to your friends. Build your universe. Inform your travels
            with trusted advice.
          </h5>
        </div>
        <!-- / section-title-area -->
        <div
          v-for="user in orderBy(
            filterBy(users, nameFilter, 'last_name', 'first_name'),
            'last_name'
          )"
        >
          <div class="row">
            <div class="col-md-12">
              <router-link :to="`/users/${user.id}`"></router-link>
              <div v-if="!user.accepted_friend">
                <div class="card card-w-raised-img-top">
                  <div class="card-body text-center">
                    <img
                      class="card-raised-img-top mb-30 rounded w-60 raised"
                      :src="user.image_url"
                      alt=""
                    />
                    <h6
                      class="mb-5 fs-10 secondary-font text-black"
                      v-if="user.pending_friend"
                    >
                      Connection pending
                    </h6>
                    <h4 class="card-title fw-bold mb-10 text-primary">
                      {{ user.first_name }} {{ user.last_name }}
                    </h4>
                    <p class="card-text mb-30">
                      My languages: {{ user.languages_spoken }}
                    </p>
                    <p class="mb-0">
                      <router-link
                        class="btn btn-xs btn-info m-5 pill"
                        :to="`/users/${user.id}`"
                        ><span class="fas fa-id-card mr-5"></span>
                        <span>Profile</span></router-link
                      >
                      <span
                        v-if="
                          user.accepted_friend != true &&
                            user.pending_friend != true
                        "
                      >
                        <button
                          class="btn btn-xs btn-primary m-5 pill"
                          v-on:click="createConnection(user)"
                        >
                          <span class="fas fa-people-arrows mr-5"></span>
                          <span>Request to connect</span>
                        </button>
                      </span>
                    </p>
                  </div>
                  <!-- / card-body -->
                </div>
                <!-- / card -->
              </div>
            </div>
            <!-- / column -->
          </div>
          <!-- / row -->
        </div>
      </div>
      <!-- / container -->
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      users: [],
      nameFilter: "",
    };
  },
  created: function() {
    axios.get("/api/users").then((response) => {
      console.log(response.data);
      this.users = response.data;
    });
  },
  methods: {
    createConnection: function(user) {
      var params = {
        recipient_id: user.id,
      };
      axios
        .post("/api/connections", params)
        .then((response) => {
          this.$router.push("/connections");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>

// "user.id !== $parent.getUserId()" is not working to exclude current user from
index
