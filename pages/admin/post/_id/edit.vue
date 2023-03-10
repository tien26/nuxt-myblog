<template>
  <div>
    <v-row>
      <v-col>
        <h1 class="text-center mb-3">Page Edit</h1>
        <v-card class="mx-auto" max-width="800" outlined>
          <v-container grid-list-md>
            <v-form ref="form" v-model="valid" @submit.prevent="submit">
              <v-text-field
                v-model="form.title"
                :counter="10"
                :rules="rules.title"
                label="Title"
                required
              ></v-text-field>
              <v-textarea
                v-model="form.body"
                label="Body"
                :rules="rules.body"
                required
              ></v-textarea>
              <v-btn type="submit" :disabled="!valid" color="success"
                >Update</v-btn
              >
              <v-btn to="/admin" color="warning">Back</v-btn>
            </v-form>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>
  
<script>
export default {
  mounted() {
    this.postId && this.getPost();
  },
  computed: {
    postId() {
      return +this.$route.params.id;
    },
  },
  data: () => ({
    valid: false,
    form: {
      title: "",
      body: "",
    },
    rules: {
      title: [
        (v) => !!v || "Title is required",
        (v) => v.length >= 10 || "Title must be at least than 10 characters",
      ],
      body: [(v) => !!v || "Body is required"],
    },
  }),
  methods: {
    submit() {
      this.$store
        .dispatch("editPost", { ...this.form, id: this.postId })
        .then(() => {
          this.$router.push("/admin");
        });
    },
    getPost() {
      this.$store.dispatch("getPost", this.postId).then((post) => {
        this.form.title = post.title;
        this.form.body = post.body;
      });
    },
  },
};
</script>