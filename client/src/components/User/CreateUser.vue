<template>
  <div>
    <h1>Create item</h1>
    <form v-on:submit.prevent = "createUser">
      <p>เตียง: <input type="text" v-model="user.name"></p>
      <p>ราคา: <input type="text" v-model="user.lastname"></p>
      <p>วัสดุ: <input type="text" v-model="user.email"></p>
      <p>ขนาด:<input type="text" v-model="user.status"></p>
      <p>คุณสมบัติ: <input type="text" v-model="user.type"></p>
      <p>ประกันสินค้า: <input type="text" v-model="user.password"></p>
      <p><button type="submit">create item</button></p>
    </form>
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
        status: "",
        type: ""
      }
    };
  },
  methods: {
    async createUser(){
      try{
        await UsersService.post(this.user)
        this.$router.push('/users')
      }catch(err){
        console.log(err)
      }
    }
  }
};
</script>

<style></style>
