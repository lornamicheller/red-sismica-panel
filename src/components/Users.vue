<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <img src="../assets/logoredsismicabordeblanco.png" width="50px" height="50px">
      <a class="navbar-brand" href="#">RED SISMICA</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                  <span class="navbar-toggler-icon"></span>
                </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item right">
            <router-link class="nav-link" to="/Posts">VIDEOS<span class="sr-only">(current)</span></router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/Photos">PHOTOS</router-link>
          </li>
          <li class="nav-item">
            <a class="nav-link" @click="logoutUser" href="#">LOGOUT</a>
          </li>
        </ul>
      </div>
    </nav>
  
    <div class="container mt-3">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">PHOTO</th>
            <th scope="col">USERNAME</th>
            <th scope="col">DATE ADDED</th>
            <th scope="col">ACTIONS</th>
          </tr>
        </thead>
        <tbody>
          <UserList v-for="item in postsList" :post="item" :key="item.id" />
        </tbody>
      </table>
  
      <div class="modal" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Modal title</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <p>Modal body text goes here.</p>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
              <button type="button" class="btn btn-primary">Save changes</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  
  
  </div>
</template>

<script>
  import {
    Parse,
    Query
  } from 'parse';
  import UserList from '@/components/UserList'
  export default {
    components: {
      UserList
    },
    data() {
      return {
        postsList: []
      }
    },
  
    mounted: function() {
      this.getPosts();
    },
    methods: {
      logoutUser: function() {
        Parse.User.logOut().then((user) => {
          console.log(user);
          this.$router.push('/')
        }).catch(error => {
          console.error(error);
        })
      },
      getPosts: function() {
        var self = this;
        var list = Parse.Object.extend('Pictures');
        var query = new Parse.Query(list);
        query.equalTo('typeOfMedia','picture')
        query.find().then((results) => {
          for (let i = 0; i < results.length; i++) {
            results[i] = results[i].toJSON();
          }
          self.postsList = results;
          console.log()
        }, (error) => {
          console.log(error)
        })
      }
    }
  }
</script>

<style scoped>
  .navbar-nav {
    font-weight: bold;
    color: rgb(255, 255, 255);
  }
  
  .navbar {
    background: #1f205a !important;
  }
  
  .navbar img {
    margin-left: 20px;
    border-radius: 50%;
  }
  
  .navbar-brand {
    margin-left: 20px;
  }
  
  .nav-item .nav-link {
    color: white;
  }

</style>