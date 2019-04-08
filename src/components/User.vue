<template>
  <v-card>
    <v-text-field v-model="user.username" />
    <v-btn @click="updateUser">Update</v-btn>
    <v-btn v-if="user.username !== 'Simon'" color="error" @click="deleteUser">Delete</v-btn>
  </v-card>
</template>
<script>
import axios from "axios"

export default {
  name: "User",
  props: ["user", "updateList"],
  methods: {
    deleteUser() {
      axios.delete("http://localhost:8080/users/" + this.user.id)
        .then(response => this.updateList());
    },
    updateUser() {
      axios.put("http://localhost:8080/users/" + this.user.id, {
        username: this.user.username
      }).then(response => alert(response.data));
    }
  }
}

</script>
