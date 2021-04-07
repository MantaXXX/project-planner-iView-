<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons"> edit </span>
        </router-link>
        <span class="material-icons" @click="projectDelete"> delete </span>
        <span class="material-icons tick" @click="toggleComplete"> done </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/project/" + this.project.id,
    };
  },
  methods: {
    projectDelete() {
      // request server to delete => method: 'DELETE'
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project.id))
        .catch((err) => console.log(err.message));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        // request header, means sending data with request and it's JSON type
        headers: { "Content-Type": "application/json" },
        // updated data in body property, have to be JSON data, hence, have to use JSON.stringify()
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => this.$emit("complete", this.project.id))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
.project.complete {
  border-left: 4px solid #00ce89;
  text-decoration: line-through;
}
.project.complete .tick {
  color: #00ce89;
}
</style>