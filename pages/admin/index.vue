<template>
  <div>
    <v-row class="my-5">
      <v-col xs12 sm8 md6>
        <h1 class="text-center">Page Admin</h1>
      </v-col>
    </v-row>
    <v-row class="ml-6">
      <v-col xs12 sm8 md6>
        <v-btn color="primary" to="/admin/post/add">Add Post</v-btn>
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
                color="warning"
                rounded
                :to="`/admin/post/${post.id}/edit`"
              >
                <span> Edit </span>
              </v-btn>
              <app-modal
                button-label="Delete"
                button-color="error"
                :button-text-style="true"
              >
                <template slot-scope="{ close }">
                  <v-card>
                    <v-card-title class="headline">
                      Are you sure?
                    </v-card-title>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn
                        color="error"
                        text
                        @click="deletePost(post.id, close)"
                      >
                        Yes
                      </v-btn>
                      <v-btn color="grey" text @click="close"> Cancle </v-btn>
                    </v-card-actions>
                  </v-card>
                </template>
              </app-modal>
            </template>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
  
<script>
import AppModal from "@/components/Modal.vue";
export default {
  components: {
    AppModal,
  },
  name: "Admin",
  fetch({ $axios, store }) {
    return $axios.$get("http://localhost:3001/posts").then((res) => {
      store.commit("updatePosts", res);
    });
  },
  methods: {
    deletePost(postId, callback) {
      this.$store
        .dispatch("deletePost", postId)
        .then(callback)
        .finally(() => {});
    },
  },
};
</script>
  