<template>
  <v-container>
    <v-layout
      text-xs-center
      wrap
    >

      <v-flex
        xs12
        mb-5
      >
      <div class="hello">
        <h1>{{ msg }}</h1>

        <div>
          <v-text-field type="text" v-model="username" />

          <v-btn @click="create">Create</v-btn>
        </div>

        <div>
          <User v-for="user in users" :user="user" :key="user.id" :updateList="refreshUserList" ></User>
        </div>

      </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios"
import User from "./User"

export default {
  name: 'HelloWorld',
  components: { User },
  data() {
    return {
      users: [],
      username: ""
    }
  },
  mounted() {
    this.refreshUserList();
  },
  methods: {
    refreshUserList() {
      axios.get("http://localhost:8080/users").then(response =>
      this.users = response.data)
    },
    create() {
      axios.post("http://localhost:8080/users", { username: this.username }).then(response =>
        this.refreshUserList()
      );
    }
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
