<template>
  <div>
    <div class="modal-add">
      <div class="form-modal">
        <form @submit="signIn">
          <div class="login-img">
            <img src="../assets/image/chatMee1.png" alt="" width="150px">
          </div>
            <h1>Login</h1>
            <div class="form-group row email">
              <div class="col-md-11">
                <input type="text" class="form-control" id="inputUsername" placeholder="Enter Your Email" v-model="email"><img src="../assets/image/email.svg" alt="">
              </div>
            </div>
              <div class="form-group row password">
                <div class="col-md-11">
                  <input type="password" class="form-control" id="inputPassword" placeholder="Enter Your Password"  v-model="password">
                  <img src="../assets/image/password.svg" alt="">
                </div>
              </div>
              <!-- <div class="alert alert-danger alert-dismissible col-md-11" role="alert">
                  <strong>hello</strong>
                  <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                      <span aria-hidden="true">&times;</span>
                  </button>
              </div> -->
              <div class="button">
                  <button type="submit" class="btn btn-outline-light">Login</button>
              </div>
              <div class="col-md-12 col-sm-12 col-xs-12 last-part">
                  <p>Not registered?<router-link to="/register"> Create an account</router-link></p>
              </div>
          </form>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase'
export default {
  name: 'login',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    signIn (e) {
      e.preventDefault()
      firebase.auth().signInWithEmailAndPassword(this.email, this.password)
        .then(user => {
          firebase.firestore().collection('users').doc(firebase.auth().currentUser.uid)
            .update({
              status: true
            })
          alert(`Success Login With email ${this.email}`)
          this.$router.push('/')
        },
        err => {
          alert(err.message)
        }
        )
    }
  }
}
</script>

<style scoped>
  *{
      font-family: "Tahoma", "Lucida Grande", "Lucida Sans Unicode", Arial, Helvetica, Verdana, sans-serif;
    }
    .modal-add{
        position: fixed;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background: #ffffff;
    }
    .login-img img{
      /* width: 150px;
      height: 150px; */
      position: absolute;
      top: -90px;
      left: 135px;
    }
    .form-modal{
        width: 430px;
        height: 470px;
        background-color: #5580a3;
        margin: 120px auto;
        border-radius: 5px;
        position: relative;
    }
    .form-modal h1{
        text-align: center;
        margin-top: 30px;
        margin-bottom: 80px;
        margin-left: -20px;
        color: #ffffff;
    }
    .form-modal form{
        padding-top: 10px;
        margin-left: 40px;
    }
    .button button{
        width: 350px;
        height: 45px;
        margin-top: 40px;
        margin-bottom: 15px;
        font-size: 20px;
        font-weight: bold;
        line-height: 30px;
        /* background: #0095f6;
        border: 1px solid #0095f6; */
    }
    .email, .password{
      position: relative;
    }
    .email img {
      position: absolute;
      top: 7px;
      left: 330px;
    }
    .password img {
       position: absolute;
      top: 7px;
      left: 330px;
    }
    .alert strong{
      font-size: 14px;
    }
    .col-md-12 p{
      text-align: center;
      margin-left: -30px;
    }
    .hide{
        display: none;
    }
    .alert{
        height: 50px;
        padding-left: 15px;
    }
    .alert .close{
        line-height: 25px;
    }
    .last-part p, .last-part a{
      color: #ffffff;
      font-size: 14px;
      padding-bottom: 10px;
    }
    @media screen and (max-width: 414px) {
      .modal-add{
        position: fixed;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background: #ffffff;
      }
      .login-img img{
        top: -90px;
        left: 100px;
      }
      input {
        width: 300px;
        height: 50px;
      }
      .form-modal{
        width: 350px;
        height: auto;
      }
      .form-modal h1{
        text-align: center;
     }
      .form-modal form{
        padding-top: 10px;
        margin-left: 25px;
      }
      .button button{
        width: 300px;
        height: 45px;
        margin-top: 40px;
        margin-bottom: 15px;
        font-size: 20px;
        font-weight: bold;
        line-height: 30px;
        /* background: #0095f6;
        border: 1px solid #0095f6; */
      }
      .email, .password{
      position: relative;
      }
      .email img {
        position: absolute;
        top: 15px;
        left: 280px;
      }
      .password img {
        position: absolute;
        top: 15px;
        left: 280px;
      }
    }
</style>
