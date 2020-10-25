<template>
  <div class="about">
    <h2>Repo Details</h2>
    <div class="cont">
    <div class="row text-left">
      <div class="col-sm-6 font-weight-bold">Repo Name: </div>
      <div class="col-sm-6">{{ repos[0].name }}</div>
    </div>
    <div class="row text-left">
      <div class="col-sm-6 font-weight-bold">FullName: </div>
      <div class="col-sm-6">{{ repos[0].full_name }}</div>
    </div>
    </div>
    
   <h5 class="float-left">    User {{ UserData.login }} with {{ UserData.followers }} followers is following {{ UserData.following }}.
     One repo for this user is {{ repos[0].full_name }} and it is {{ repos[0].private ? "it is private" : " it is not private" }}.
   </h5>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import APISERVICE from "@/services/apiService";

export default {
  data() {
    return {
      repos: "",
      privateMsg: ""
    }
  },
  methods: {
    checkPrivate(bool) {
      return bool ? "it is private" : " it is not private"
    },
    getRepos(name) {
      APISERVICE.getRepos(name)
        .then(res => {
          this.repos = res.data
          console.log(res);
        })
        .catch(error => console.dir(error));
    }
  },
  mounted () {
    this.getRepos(this.UserData.login)
  },
  computed: {
    ...mapGetters(["UserData"]),  
  }
}
</script>
<style scoped>
.cont {
  width: 30%;
    margin-left: auto;
    margin-right: auto;
    text-align: left; border: 1px solid #f6f6f6; border-radius: 5px; padding: 10px; margin-bottom: 40px; box-shadow: 10px 17px 42px -15px rgba(0,0,0,0.75); 
}
</style>
