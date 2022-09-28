<template>
  <div class="project" :class="{ isCompleted: project.isCompleted }">
    <div class="actions">
      <h3 @click="toggleSingleProject">{{ project.title }}</h3>
      <div class="styles">
        <router-link :to="{ name: 'Edit', params: { id: project.id } }">
          <span class="material-icons"> edit </span>
        </router-link>
        <span @click="deleteItem" class="material-icons"> delete </span>
        <span @click="toggleItem" class="material-icons tick"> done </span>
      </div>
    </div>
    <div class="details" v-show="isShow">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      isShow: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },

  methods: {
    toggleSingleProject() {
      this.isShow = !this.isShow;
    },
    deleteItem() {
      fetch(this.url, { method: "DELETE" }).then(
        this.$emit("delete", this.project.id)
      );
    },
    toggleItem() {
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ isCompleted: !this.project.isCompleted }),
      })
        .then(() => {
          this.$emit("isCompleted", this.project.id);
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background-color: #fff;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 4px 5px 3px rgba(0, 0, 0, 0.2);
  border-left: 4px solid #e90075;
}

.project.isCompleted {
  border-left: 4px solid #00ce89;
}
.project.project.isCompleted .tick {
  color: #00ce89;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.actions h3 {
  cursor: pointer;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  cursor: pointer;
  color: #e90075;
}
.material-icons:hover {
  color: #777;
}
/* .details {
} */
</style>