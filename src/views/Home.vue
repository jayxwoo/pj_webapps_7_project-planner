<template>
  <NavFilter @filter="handleFilter" :currentBy="currentBy" />
  <div class="home">
    <div class="projects-cont" v-if="projects.length">
      <div class="projects-group" v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject";
import NavFilter from "../components/NavFilter";

export default {
  name: "Home",
  components: { SingleProject, NavFilter },
  data() {
    return {
      projects: [],
      currentBy: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        this.projects = data;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    handleComplete(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.complete = !p.complete;
    },
    handleFilter(by) {
      this.currentBy = by;
    },
  },
  computed: {
    filteredProjects() {
      if (this.currentBy === "all") {
        return this.projects;
      } else if (this.currentBy === "completed") {
        return this.projects.filter((project) => {
          return project.complete === true;
        });
      } else if (this.currentBy === "ongoing") {
        return this.projects.filter((project) => {
          return project.complete === false;
        });
      }
    },
  },
};
</script>
