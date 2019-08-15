<template>
  <div>
    <h1>Dashboard</h1>
    <p>Welcome to your dashboard {{ user.name }}</p>
    <p>Your login email is: {{ user.email }}</p>
    <form @submit.prevent="submitForm">
      <label for="name">Edit your name:</label>
      <input type="text" id="name" v-model="userForm.name" />
      <br />
      <div>
        <label for="age">Edit your Age</label>
        <input type="text" v-model="userForm.age" id="age" requried />
      </div>
      <div>
        <label for="city">Edit your City</label>
        <input type="text" v-model="userForm.city" id="city" requried />
      </div>
      <div>
        <label for="job">Edit your Job</label>
        <input type="text" v-model="userForm.job" id="job" requried />
      </div>
      
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
<script>
import { mapActions, mapGetters } from "vuex";
export default {

  data() {
    return {
     userForm: {
      name: "",
      age: "",
      city: "",
      job: ""
      
    }
    };
  },
  
  computed: {
    ...mapGetters({
      userData: "getUser"
    }),
    user() {
      return !this.userData ? false : this.userData;
    }
  },

  created() {
    this.getUserData();
  },
  methods: {
    ...mapActions(["fetchUser", "updateUser"]),
    getUserData() {
      let userEmail = localStorage.getItem("userEmail");
      this.fetchUser(userEmail);
    },
    submitForm() {
      const formData = {
        name: this.userForm.name,
        age: this.userForm.age,
        city: this.userForm.city,
        job: this.userForm.job,
      
      };
      this.updateUser(formData);
    }
  }
};
</script>
