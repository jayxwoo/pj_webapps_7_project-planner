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
    <button class="form-submit-btn">Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
      created_at: null,
      uri: "http://localhost:3000/projects",
    };
  },
  methods: {
    handleSubmit() {
      // Create project object
      this.created_at = new Date().toLocaleString();
      let p = {
        title: this.title,
        details: this.details,
        complete: false,
        created_at: this.created_at,
      };

      // Save project object
      fetch(this.uri, {
        method: "POST",
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
.project-form {
  background-color: white;
  display: flex;
  flex-direction: column;
  padding: 2rem;
  border-radius: 10px;
}
.form-label {
  text-transform: uppercase;
  font-size: 0.8rem;
  margin-bottom: 0.5rem;
}
.form-input-title {
  border: none;
  border-bottom: 1px solid var(--lightgrey);
  padding: 0.6rem;
}
.form-input {
  margin-bottom: 2rem;
}
.form-textarea-details {
  resize: vertical;
  height: 200px;
  padding: 0.6rem;
  border: 1px solid var(--lightgrey);
  border-radius: 5px;
}
.form-submit-btn {
  align-self: center;
  border: none;
  background-color: var(--green);
  color: white;
  padding: 0.8rem;
  font-size: 0.8rem;
  font-weight: bold;
  border-radius: 5px;
  cursor: pointer;
  text-transform: uppercase;
}
.form-submit-btn:hover {
  background-color: forestgreen;
}
</style>