<template>
  <div>
    <b-card-title class="text-center fs-6">
      {{ activity.name }}
    </b-card-title>
    <b-card-text class="text-center">
      {{ activity.folderName ? activity.folderName : "sin carpeta" }}
    </b-card-text>
    <b-card-text class="d-flex text-center justify-content-center">
      <p class="my-auto">hecho:</p>
      <input
        class="checkBox"
        type="checkbox"
        v-model="activity.done"
        @change="completeTask(activity)"
      />
    </b-card-text>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["task"],
  data() {
    return {
      activity: {
        id: this.task.id,
        name: this.task.name,
        folder: this.task.folder,
        folderId: this.task.folderId,
        done: this.task.done,
      },
    };
  },
  methods: {
    completeTask(activity) {
      fetch("http://localhost:8080/api/manager/activity/complete", {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          id: activity.id,
          done: activity.done,
        }),
      }).catch((err) => console.log(err.message));
    },
  },
};
</script>

<style lang="scss" scoped>
.checkBox {
  margin-top: auto;
  margin-bottom: 4%;
  margin-left: 5%;
}
</style>
