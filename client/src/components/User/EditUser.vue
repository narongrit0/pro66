<template>
  <div>
    <h1>Edit User</h1>
    <form v-on:submit.prevent="editUser">
      <p>เตียง: <input type="text" v-model="user.name" /></p>
      <p>ราคา: <input type="text" v-model="user.lastname" /></p>
      <p>วัสดุ: <input type="text" v-model="user.email" /></p>
      <p>ประกันสินค้า: <input type="text" v-model="user.password" /></p>
      <p><button type="submit">edit</button></p>
    </form>
    <hr />
    <div>
      <p>เตียง: {{ user.name }}</p>
      <p>ราคา: {{ user.lastname }}</p>
      <p>วัสดุ: {{ user.email }}</p>
      <p>ประกันสินค้า: {{ user.password }}</p>
      <p></p>
    </div>
  </div>
</template>

<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      user: {
        name: "",
        lastname: "",
        email: "",
        password: "",
        status: "active"
      }
    };
  },
  methods: {
    async editUser() {
      try {
        console.log(this.user)
        await UsersService.put(this.user)
        this.$router.push("/users")
      } catch (err) {
        console.log(err)
      }
    }
  },
  async created() {
    try {
      let userId = this.$route.params.userId
      this.user = (await UsersService.show(userId)).data
    } catch (err) {
      console.log(err)
    }
  }
};
</script>

<style></style>
