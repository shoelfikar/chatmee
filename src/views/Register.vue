<template>
    <div>
        <div class="modal-add">
          <div class="form-modal">
            <form @submit="signUp">
              <div class="login-img">
                <img src="../assets/image/chatMee1.png" alt="" width="150px">
              </div>
                <h1>Register</h1>
                <div class="form-group row">
                  <div class="col-md-11">
                    <input type="text" class="form-control" id="username" placeholder="Username" v-model="displayName">
                  </div>
                </div>
                <div class="form-group row">
                  <div class="col-md-11">
                    <input type="email" class="form-control" id="email" placeholder="Email"  v-model="email">
                  </div>
                </div>
                  <div class="form-group row">
                    <div class="col-md-11">
                      <input type="password" class="form-control" id="inputPassword" placeholder="Password" v-model="password">
                    </div>
                  </div>
                  <!-- <div class="form-group row">
                    <div class="col-md-11">
                      <input type="password" class="form-control" id="inputrePassword" placeholder="Retype Password">
                    </div>
                  </div> -->
                  <!-- <div class="alert alert-danger alert-dismissible col-md-11" role="alert" v-if="myMsg !== ''">
                      <strong>{{myMsg}}</strong>
                      <button type="button" class="close" data-dismiss="alert" aria-label="Close" @click="alert1">
                          <span aria-hidden="true">&times;</span>
                      </button>
                  </div> -->
                  <div class="button">
                      <button type="submit" class="btn btn-outline-primary">Register</button>
                  </div>
                  <div class="col-md-12 col-sm-12 col-xs-12 last-part">
                      <p>Back to<router-link to="/login"> Login</router-link></p>
                  </div>
              </form>
          </div>
        </div>
    </div>
</template>
<script>
import firebase from 'firebase'

export default {
  name: 'Register',
  data () {
    return {
      email: '',
      password: '',
      displayName: '',
      imageProfil: 'https://firebasestorage.googleapis.com/v0/b/chatmee-3a979.appspot.com/o/profil%2Fuser-profile.png?alt=media&token=54d73fa0-5b19-499f-9032-b659df1d10d1'
    }
  },
  methods: {
    signUp (e) {
      e.preventDefault()
      firebase.auth().createUserWithEmailAndPassword(this.email, this.password)
        .then(user => {
          firebase.firestore().collection('users').doc(firebase.auth().currentUser.uid)
            .set({
              // id: firebase.auth().currentUser.uid,
              email: this.email,
              displayName: this.displayName,
              imageProfil: this.imageProfil,
              phoneNumber: '+6200-000-000-00',
              status: true
            })
            // ensure we catch any errors at this stage to advise us if something does go wrong
            .catch(error => {
              console.log('Something went wrong with added user to firestore: ', error)
            })
          alert(`Register user ${this.email} Success!`)
          this.$router.push('/login')
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
            background: #5580a3;
        }
        .login-img img{
          position: absolute;
          top: 20px;
          left: 150px;
        }
        .form-modal{
            width: 430px;
            height: 550px;
            background-color: #fff;
            margin: 50px auto;
            border-radius: 10px;
            position: relative;
        }
        .form-modal h1{
           text-align: center;
           margin-top: 120px;
           margin-bottom: 30px;
           margin-left: -20px;
        }
        .form-modal form{
            padding-top: 10px;
            margin-left: 40px;
        }
        .button button{
            width: 350px;
            height: 45px;
            margin-top: 30px;
            margin-bottom: 10px;
            /* background: #57CAD5;
            border: 1px solid #57CAD5; */
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
        @media screen and (max-width: 414px) {
        .form-modal{
          width: 350px;
          height: auto;
          margin-bottom: 50px;
          margin: 30px auto;
          border-radius: 5px;
        }
        .modal-add{
            position: fixed;
            top: 0;
            bottom: 0;
            right: 0;
            left: 0;
            background: #5580a3;
        }
        .login-img img{
          left: 110px;
        }
        input {
          width: 300px;
          height: 45px;
          margin-left: -15px;
        }
        .button button{
          width: 300px;
          height: 45px;
          margin-top: 20px;
          margin-left: -15px;
          margin-bottom: 15px;
          font-size: 20px;
          font-weight: bold;
          line-height: 30px;
      }
      }
</style>
