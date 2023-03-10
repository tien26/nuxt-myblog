<template>
  <v-row class="my-5">
    <v-col xs12 sm8 md6>
      <v-card class="mx-auto" max-height="600" width="800" rounded="xl">
        <v-card-text>
          <p class="text--primary text-center mb-3 text-h5">
            {{ $store.state.selectedPost.title }}
          </p>
          <p class="text--primary text-justify">
            {{ $store.state.selectedPost.title }}
          </p>
        </v-card-text>
        <v-card-actions>
          <template>
            <v-btn text color="deep-purple accent-4" block to="/" rounded>
              <span> Back </span>
            </v-btn>
          </template>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  fetch({ $axios, store, params }) {
    if (store.state.selectedPost && store.state.selectedPost.id == params.id)
      return true;
    return $axios
      .$get(`https://jsonplaceholder.typicode.com/posts/${params.id}`)
      .then((res) => {
        store.commit("updateSelectedPost", res);
      });
  },
};
</script>