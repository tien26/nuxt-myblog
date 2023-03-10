<template>
  <div>
    <v-row class="my-5">
      <v-col xs12 sm8 md6>
        <h1 class="text-center">Home</h1>
      </v-col>
    </v-row>
    <v-row class="my-5">
      <v-col xs12 sm8 md6 v-for="post in $store.state.posts" :key="post.id">
        <v-card class="mx-auto" max-height="100%" width="300" rounded="xl">
          <v-card-text>
            <p class="text--primary text-center mb-3 text-h5">
              {{ post.title }}
            </p>
            <p class="text--primary text-justify">{{ post.body }}</p>
          </v-card-text>
          <v-card-actions>
            <template>
              <v-btn
                text
                color="primary"
                block
                :to="`/post/${post.id}`"
                rounded
              >
                <span> Detail </span>
              </v-btn>
            </template>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "Home",
  fetch({ $axios, store }) {
    return $axios.$get("http://localhost:3001/posts").then((res) => {
      store.commit("updatePosts", res);
    });
  },
};
</script>
