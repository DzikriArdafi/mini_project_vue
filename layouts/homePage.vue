<template>
<div>
    <v-app class="dark">
      
  <v-container fluid class="jangancontainer" style="height: 420px">
    
    <v-row>
      <v-col cols="12">
        <NavbarHome />
      </v-col> 
    </v-row>
    <!-- Left Row -->
    <v-row>
      <v-col cols="6">
        <div style="margin-top: 75px">
          <h1 class="text-center font-weight-bold">Happy <span class="font-weight-regular">Watching</span> </h1>
            <v-btn
            to="/All-Movies"
            color="#BF360C"
            elevation="2"
            small
            style="margin-left:210px">All Movies</v-btn>
        </div>
      </v-col>

      <!-- Right Row -->
  
      <v-col cols="6">
  <ApolloQuery 
    :query="require('../gql/queries/HomeImage.gql')"> 
  <template v-slot="{ result: { loading, error, data } }">
  <!-- Loading -->
        <div v-if="loading" class="loading apollo">Loading...</div>
  <!-- Error -->
        <div v-else-if="error" class="error apollo">An error occurred</div>
  <!-- Result -->
      <div v-else-if="data" class="result apollo">
        <v-carousel 
        height="290"
        cycle
        hide-delimiter-background
        
        >
    <v-carousel-item
      v-for="newItem in data.Home_by_pk.Movies"
      :key="newItem.Title" 
      @click="goTo(newItem.Title)"
      class="mx-auto"
      
      reverse-transition="fade-transition"
      transition="fade-transition"
      style="border-radius: 20px"
    >
    <v-img style="border-radius: 10px; margin-bottom: auto"
      :src="newItem.Path_image"
      class="mx-auto"
      max-height="290px"
      max-width="500px" 
    ></v-img>
    </v-carousel-item>
  </v-carousel>
      </div>
    <div v-else class="no-result apollo text-center">
            
            <v-icon>mdi-spin mdi-loading</v-icon> 
        </div>
  </template>

  </ApolloQuery>
</v-col>
    
    </v-row>
  </v-container>     
    

  <Nuxt />
   
    </v-app>
</div>
</template>

<script>


export default {
    name: 'HomeLayout',
    data: () => ({
      model: null,
      }),
    methods: {
    goTo(Title) {
      this.$router.push(`/detail/${Title}`);
    },
    }
}
</script>

<style>
    .jangancontainer{
      background-image: url("../static/h.jpg"); 
      
    };
    #container1{
      background-color: rgb(0, 1, 51);
      height: 100%;
      
    }
    

</style>