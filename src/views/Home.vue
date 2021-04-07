<template>
  <div class="home">
    <Tabs value="all" @on-click="filteredProjects">
      <TabPane label="View All" name="all">
        <div v-for="project in filters" :key="project.id">
          <SingleProject
            :project="project"
            @delete="handleDelete"
            @complete="handleComplete"
          />
        </div>
      </TabPane>
      <TabPane label="COMPLETED" name="completed">
        <div v-if="projects.length">
          <div v-for="project in filters" :key="project.id">
            <SingleProject
              :project="project"
              @delete="handleDelete"
              @complete="handleComplete"
            />
          </div>
        </div>
      </TabPane>
      <TabPane label="ONGOING" name="ongoing">
        <div v-if="projects.length">
          <div v-for="project in filters" :key="project.id">
            <SingleProject
              :project="project"
              @delete="handleDelete"
              @complete="handleComplete"
            />
          </div>
        </div>
      </TabPane>
    </Tabs>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject";

export default {
  name: "Home",

  components: { SingleProject },
  data() {
    return {
      projects: [],
      current: "",
      filter: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/project")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
    handleComplete(id) {
      let target = this.projects.find((project) => {
        return project.id === id;
      });
      target.complete = !target.complete;
    },
    filteredProjects(status) {
      this.current = status;
    },
  },
  computed: {
    filters(name) {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.complete);
      } else if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.complete);
      }
      return this.projects;
    },
  },
};
</script>
