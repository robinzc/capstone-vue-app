<template>
  <div class="connections-index">
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
            <option v-for="connection in connections"
              >{{ connection.user.first_name }}
              {{ connection.user.last_name }}</option
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
          <h1 class="section-title">YOUR UNIVERSE</h1>
          <h4 class="section-title">
            Explore the universe of your personal travel network.
          </h4>
          <h5 class="section-title">
            Browse connections. Confirm pending requests. Access your friends'
            profiles from one place.
          </h5>
          <h5 class="section-title">
            Get inspiration for your next adventure!
          </h5>
          <br />
          <p class="mb-0">
            <router-link
              class="btn btn-primary-gradient m-5 ml-0"
              :to="`/map_connections`"
            >
              <span>See your connections map</span></router-link
            >
          </p>
        </div>
        <!-- / section-title-area -->
        <div
          v-for="connection in orderBy(
            filterBy(
              connections,
              nameFilter,
              'user.last_name',
              'user.first_name'
            ),
            'accepted'
          )"
        >
          <div class="row">
            <div class="col-md-12">
              <!-- <router-link :to="`/connections/${user.id}`"></router-link> -->
              <!-- <div v-if="!user.accepted_friend"> -->
              <div class="card card-w-raised-img-top">
                <div class="card-body text-center">
                  <img
                    class="card-raised-img-top mb-30 rounded w-60 raised"
                    :src="connection.user.image_url"
                    alt=""
                  />
                  <!-- <h6
                    class="mb-5 fs-10 secondary-font text-black"
                    v-if="user.pending_friend"
                  >
                    Connection pending
                  </h6> -->
                  <h4 class="card-title fw-bold mb-10 text-primary">
                    {{ connection.user.first_name }}
                    {{ connection.user.last_name }}
                  </h4>
                  <p class="card-text mb-30">
                    Email: {{ connection.user.email }}
                    <br />
                    My languages: {{ connection.user.languages_spoken }}
                  </p>
                  <h6
                    class="card-title fw-bold mb-10 text-primary"
                    v-if="connection.accepted"
                  >
                    Connected
                  </h6>
                  <h6
                    class="card-title fw-bold mb-10 text-primary"
                    v-if="!connection.accepted"
                  >
                    Connection request pending
                  </h6>
                  <p class="mb-0">
                    <router-link
                      class="btn btn-xs btn-info m-5 pill"
                      :to="`/users/${connection.user.id}`"
                      ><span class="fas fa-id-card mr-5"></span>
                      <span>Profile</span></router-link
                    >
                    <span v-if="connection.accepted != true">
                      <button
                        class="btn btn-xs btn-primary m-5 pill"
                        v-if="connection.recipient_id == $parent.getUserId()"
                        v-on:click="updateConnection(connection)"
                      >
                        <span class="fas fa-people-arrows mr-5"></span>
                        <span>Accept connection request</span>
                      </button>
                    </span>
                    <span v-if="connection.accepted">
                      <button
                        class="btn btn-xs btn-primary m-5 pill"
                        v-on:click="destroyConnection(connection)"
                      >
                        <span class="fas fa-user-alt-slash mr-5"></span>
                        <span> Delete this connection </span>
                      </button>
                    </span>
                  </p>
                </div>
                <!-- / card-body -->
              </div>
              <!-- / card -->
              <!-- </div> -->
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
      connections: [],
      nameFilter: "",
    };
  },
  created: function() {
    axios.get("/api/connections").then((response) => {
      console.log(response.data);
      this.connections = response.data;
    });
  },
  methods: {
    updateConnection: function(connection) {
      axios
        .patch(`/api/connections/${connection.id}`)
        .then((response) => {
          this.$router.push(`/users/${connection.sender_id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyConnection: function(connection) {
      if (confirm("Are you sure you want to delete this connection?"));
      {
        axios.delete(`/api/connections/${connection.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/users");
        });
      }
    },
  },
};
</script>
