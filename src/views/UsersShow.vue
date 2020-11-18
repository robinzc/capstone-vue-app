<template>
  <div class="users-show">
   
      <div class="container">
        <div class="section-title-area text-center mb-70">
          <br />
          <p class="mb-0">
            <router-link
              class="btn btn-primary-gradient m-5 ml-0"
              :to="`/map_connections`"
            >
              <span>See your connections map</span></router-link
            >
          </p>
          <br />
          <h2 class="section-title">{{ user.first_name }} {{ user.last_name }}</h2>
          <h5 class="section-title">My languages: {{ user.languages_spoken }}</h5>
          <h6 class="section-title">
            {{ user.email }}
          </h6>
        </div>
      <br />
        <!-- / section-title-area -->
            <div class="col-md-12">
            
                <div class="card card-w-raised-img-top">
                  <div class="card-body text-center">
                    <img
                      class="card-raised-img-top mb-30 rounded w-60 raised"
                      :src="user.image_url"
                      alt=""
                    />
                    
                    <h3 class="card-title fw-bold mb-10 text-primary">
                      My cities
                    </h3>
                    <br />
                    
                    <div class="row">
                    <div class="col-sm-6 col-md-3 tablet-top-30 text-center">
                        <div class="card">
                            <div class="card-body">
                                <i class="fas fa-house-user fs-36 text-primary d-block mb-15"></i>
                                <h3 class="timer" id="count-one" data-to="123" data-speed="1000">123</h3>
                                <p>Visitors</p>
                            </div><!-- / card-body -->
                        </div><!-- / card -->
                    </div><!-- / column -->

                    <div class="col-sm-6 col-md-3 tablet-top-30 text-center">
                        <div class="card">
                            <div class="card-body">
                                <i class="fas fa-suitcase fs-36 text-success d-block mb-15"></i>
                                <h3 class="timer" id="count-two" data-to="456" data-speed="2000">456</h3>
                                <p>Hours</p>
                            </div><!-- / card-body -->
                        </div><!-- / card -->
                    </div><!-- / column -->

                    <div class="col-sm-6 col-md-3 tablet-top-30 text-center">
                        <div class="card">
                            <div class="card-body">
                                <i class="fas fa-plane-arrival fs-36 text-info d-block mb-15"></i>
                                <h3 class="timer" id="count-three" data-to="789" data-speed="3000">789</h3>
                                <p>Views</p>
                            </div><!-- / card-body -->
                        </div><!-- / card -->
                    </div><!-- / column -->

                    <div class="col-sm-6 col-md-3 tablet-top-30 text-center">
                        <div class="card">
                            <div class="card-body">
                                <i class="fas fa-map-marker-alt fs-36 text-warning d-block mb-15"></i>
                                <h3 class="timer" id="count-four" data-to="997" data-speed="4000">997</h3>
                                <p>Comments</p>
                            </div><!-- / card-body -->
                        </div><!-- / card -->
                    </div><!-- / column -->
                </div>
                <p class="card-text mb-0">
                      <span v-if="user.id == $parent.getUserId()">
                  <router-link class="btn btn-xs btn-primary m-5 pill" :to="`/users/${this.user.id}/edit`"><span class="fas fa-edit mr-5" ></span>
                   <span>Update your profile</span></router-link
                   >
                   </span>
                   <br />
                    </p>
                  </div>
                  <!-- / card-body -->
                </div>
                <!-- / card -->
              </div>
        </div>
      </div>
      <!-- / container -->
  

    <!-- <h3>My Cities</h3>

    <div v-for="associated_city in user.associated_cities">
      <h4>{{ associated_city.city_name }}</h4>
      <p v-if="associated_city.current_living">I'm living here</p>
      <p v-if="associated_city.current_visiting">I'm visiting here</p>
      <p v-if="associated_city.lived">I've lived here</p>
      <p v-if="associated_city.visited">I've visited here</p>
    </div>
      --> 
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
      associated_cities: [],
      user_cities: [],
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      this.user = response.data;
      console.log(response.data);
    });
  },
  methods: {},
};
</script>

// Needs friend validation // this.associated_cities =
this.user.associated_cities.map((city) => { // return { id: city.city_id, name:
city.city_name }; // }); // this.user.associated_cities.forEach((city) => { //
if (city.current_living) { // this.associated_cities.push({ // city_id:
city.city_id, // current_living: true, // }); // } // if (city.current_visiting)
{ // this.associated_cities.push({ // city_id: city.city_id, //
current_visiting: true, // }); // } // if (city.visited) { //
this.associated_cities.push({ // city_id: city.city_id, // visited: true, // });
// } // if (city.lived) { // this.associated_cities.push({ // city_id:
city.city_id, // lived: true, // }); // } // });n
