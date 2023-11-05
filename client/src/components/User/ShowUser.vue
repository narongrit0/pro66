<template>
  <div>
    <h1>Get User By Id</h1>
    <div>id: {{ user.id }}</div>
    <div>เตียง: {{ user.name }}</div>
    <div>ราคา: {{ user.lastname }}</div>
    <div>วัสดุ: {{ user.email }}</div>
    <div>ประกันสินค้า: {{ user.password }}</div>
    <div>ขนาด: {{ user.status }}</div>
    <div>คุณสมบัติ: {{ user.type }}</div>
    <div><button @click="navigateTo('/user/edit/'+user.id)">edit user</button></div>
    <div><button @click="navigateTo('/users')">กลับ</button></div>
  </div>
</template>

<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      user: null
    };
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    }
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
      console.log(this.user);
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style></style>
