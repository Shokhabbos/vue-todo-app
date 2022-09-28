<template>
  <div class="home">
    <a
      href="https://github.com/Shokhabbos/vue-todo-app"
      target="_blank"
      class="source-code"
    >
      Source Code</a
    >
    <FilterNav @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredToDo" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @isCompleted="handleComplete"
        />
      </div>
    </div>
    <div v-else>Loading ...</div>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue";
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: "HomeView",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((item) => item.id !== id);
    },
    handleComplete(id) {
      let p = this.projects.find((item) => {
        return item.id === id;
      });
      p.isCompleted = !p.isCompleted;
    },
  },
  computed: {
    filteredToDo() {
      if (this.current === "completed") {
        return this.projects.filter((todo) => todo.isCompleted);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((todo) => !todo.isCompleted);
      }
      return this.projects;
    },
  },
};
</script>

<style scoped>
.source-code {
  color: #bbb;
  text-decoration: none;
  font-weight: 500;
  transition: all ease 0.3s;
}
.source-code:hover {
  color: rgb(36, 35, 35);

}
</style>
