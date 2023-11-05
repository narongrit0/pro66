<template>
  <div>
    <h1>Get All item</h1>
    <div>
      <h2>จำนวนเตียง {{ users.length }}</h2>
    </div>
    <div v-for="i in users" v-bind:key="i.id">
      <div>เตียง: {{ i.name }}</div>
      <div>ราคา: {{ i.lastname }}</div>
      <div>ขนาด: {{ i.status }}</div>
      <div>คุณสมบัติ: {{ i.type }}</div>

      <div>
        <button v-on:click="navigateTo('/user/' + i.id)">ดูข้อมูล</button>
      </div>
      <div>
        <button @click="navigateTo('/user/edit/' + i.id)">edit</button>
      </div>
      <div><button @click="deleteUser(i)">delete</button></div>
      <hr />
    </div>
  </div>
</template>

<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: []
    };
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user) {
      let result = confirm("Want of delete?");
      if (result) {
        try {
          await UsersService.delete(user);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.users = (await UsersService.index()).data;
    }
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style></style>
