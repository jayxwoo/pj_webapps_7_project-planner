<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="project-main-cont">
      <h3 class="project-title" @click="toggleDetails">{{ project.title }}</h3>
      <div class="project-actions">
        <router-link :to="{ name: 'EditProject', params: {id: project.id} }">
          <span class="material-icons"> edit </span>
        </router-link>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons tick" @click="toggleComplete"> done </span>
      </div>
    </div>
    <div class="project-details-cont" v-if="showDetails">
      <p class="project-createdAt">{{ project.created_at }}</p>
      <p class="project-details">{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: `http://localhost:3000/projects/${this.project.id}`,
    };
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },
    deleteProject(e) {
      fetch(this.uri, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
.project {
  width: 100%;
  background-color: rgba(255, 255, 255, 1);
  padding: 20px;
  margin: 20px auto;
  border-radius: 5px;
  border-left: 5px solid crimson;
  box-shadow: 2px 2px 4px lightgrey;
}
.project:first-of-type {
  margin-top: 0;
}
.project.complete {
  border-left: 5px solid var(--green);
}
.project-main-cont {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.project-actions {
  display: flex;
}
.material-icons {
  margin-left: 0.7rem;
  cursor: pointer;
  color: var(--lightgrey);
}
.material-icons:hover {
  color: var(--grey);
}
.project.complete .tick {
  color: var(--green);
}
.project-details-cont {
  margin-top: 1rem;
}
.project-title {
  cursor: pointer;
}
.project-createdAt {
  font-size: 0.7rem;
  margin-bottom: 0.5rem;
}
</style>