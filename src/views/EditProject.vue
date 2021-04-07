<template>
  <form class="project-form" @submit.prevent="handleSubmit">
    <label class="form-label-title form-label" for="title">Title:</label>
    <input
      class="form-input-title form-input"
      type="text"
      name="title"
      id="title"
      v-model="title"
      required
    />
    <label class="form-label-details form-label" for="details">Details:</label>
    <textarea
      class="form-textarea-details form-input"
      name="details"
      id="details"
      v-model="details"
      required
    ></textarea>
    <button class="form-submit-btn">Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      completed: null,
      uri: `http://localhost:3000/projects/${this.id}`,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
        this.completed = data.completed;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    handleSubmit() {
      let p = {
        title: this.title,
        details: this.details,
        completed: this.completed,
        created_at: new Date().toLocaleString(),
      };
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(p),
      })
        .then(() => {
          this.$router.push({ name: "Home" });
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
</style>