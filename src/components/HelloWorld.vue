<template>
  <div class="container-fluid">
    <img src="../assets/logoredsismicabordeblanco.png" class="shamar-logo" alt="logo" width="200px" height="200px">
    <div class="login-form container">
        <div class="login-title">
          <span>Login</span>
        </div>
        <div class="form-group row">
          <i class="fas fa-user col-sm-1"></i>
          <div class="col-sm-11">
            <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email or Username" v-model="email">
          </div>
        </div>
        <div class="form-group row">
          <i class="fas fa-lock col-sm-1"></i>
          <div class="col-sm-11">
            <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password" v-model="password">
          </div>
        </div>
        <button @click="loginUser" class="btn btn-primary">Login</button>
    </div>
  </div>
</template>

<script>
  import Parse from "parse";
  export default {
    name: 'HelloWorld',
    data() {
      return {
        email: null,
        password: null
      }
    },
    methods: {
      loginUser() {
        Parse.User.logIn(this.email, this.password).then((user) => {
          console.log(user);
          console.log(user)
          if (user.get("isAdmin") == true) {
            this.$router.push("/Posts");
          } else {
            Parse.User.logOut().then(() => {
              var currentUser = Parse.User.current();
              alert("This user is not an admin.");
            });
          }
        }).catch(error => {
          console.error(error);
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container-fluid {
    padding-top: 100px;
    padding-bottom: 100px;
    background: #1f205a;
    height: 100vh;
  }
  
  .shamar-logo {
    border-radius: 50%;
  }
  
  .login-form {
    /* width: 700px; */
    height: auto;
    background: rgb(255, 255, 255);
    margin-top: 50px;
    padding: 50px;
    border-radius: 50px;
  }
  
  #exampleInputEmail1 {
    border-style: none;
    border-radius: 0;
    border-bottom: 1px solid;
    margin-top: 40px;
    margin-bottom: 30px;
  }
  
  #exampleInputPassword1 {
    border-style: none;
    border-radius: 0;
    border-bottom: 1px solid;
  }
  
  .btn-primary {
    background: #1f205a;
    width: 100px;
    border-style: none;
    margin-bottom: 20px;
    float: right;
    -webkit-box-shadow: 0px 10px 13px -7px #000000, 5px 5px 15px 5px rgba(0, 0, 0, 0);
    box-shadow: 0px 10px 13px -7px #000000, 5px 5px 15px 5px rgba(0, 0, 0, 0);
  }
  
  .fa-user {
    padding-left: 0;
    padding-right: 0;
    padding-top: 60px;
    font-size: 20px;
  }
  
  .fa-lock {
    padding-left: 0;
    padding-right: 0;
    padding-top: 10px;
    font-size: 20px;
  }
  
  .login-title {
    width: 100%;
    height: auto;
    font-size: 40px;
    color: black;
  }
</style>
