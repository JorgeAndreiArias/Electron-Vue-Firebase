<template>
  <div class="home">
     <table class="table">
       <thead class="thead-dark">
          <tr>
            <th scope="col">Name</th>
            <th scope="col">LastName</th>
            <th scope="col">Nick</th>
            <th scope="col">Password</th>
          </tr>
       </thead>
       <tbody>
          <tr v-for="user in users" v-bind:key="user">
            <td>{{ user.Name }}</td>
            <td>{{ user.Paternal + " " + user.Maternal}}</td>
            <td>{{ user.Nick }}</td>
            <td> {{ user.Password }}</td>
          </tr>
       </tbody>
     </table>
     <download-excel
          class   = "btn btn-default"
          :data   = "users"
          :fields = "json_fields"
          title = "Users List"
          worksheet = "Users"
          name    = "Data">      
      </download-excel>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Firebase from 'firebase'
import Vue from 'vue'
import JsonExcel from 'vue-json-excel'
Vue.component('downloadExcel', JsonExcel)

var firebaseConfig = {
    apiKey: "AIzaSyDkMt7i3CPlQe865mj2akiWN2Wu5k4OWkk",
    authDomain: "users-7bba9.firebaseapp.com",
    databaseURL: "https://users-7bba9.firebaseio.com",
    projectId: "users-7bba9",
    storageBucket: "users-7bba9.appspot.com",
    messagingSenderId: "79834152064",
    appId: "1:79834152064:web:bc5e9af11ad72af3"
};

let app = Firebase.initializeApp(firebaseConfig);
let db = app.database();

let userRef = db.ref('users');

export default {
  name: 'home',
  firebase: {
    users: userRef
  },
  data:{
    json_fields: {
      "Maternal" : "Maternal",
      "Name" : "Name",
      "Nick" : "Nick",
      "Password" : "Password",
      "Paternal" : "Paternal"
    } 
  },
  components: {
    HelloWorld
  },
  methods:{
    GenerateExcel(){

    },
  },
}
</script>
