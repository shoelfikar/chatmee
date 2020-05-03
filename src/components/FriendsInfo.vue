<template>
  <div>
    <div class="profil hide">
      <div class="main-profil">
        <div class="close">
          <a href="#" @click="closeModal">X</a>
        </div>
        <div class="head-profil">
          <div class="photo" v-if="picture == null">
            <img :src="whois[0].imageProfil" alt="">
            <progress id="progress" :value="uploadValue" max="100" v-if="uploadValue !== 0"></progress>
          </div>
          <div class="photo" v-else>
            <img :src="picture" alt="">
          </div>
          <div class="nama">
            <h5>{{whois[0].displayName}}</h5>
            <p>{{whois[0].email}}</p>
          </div>
        </div>
        <div class="body-profil">
          <div class="phone">
            <img src="../assets/image/phone.png" alt="">
            <input type="text" :value="whois[0].phoneNumber">
            <!-- <p>+6282386927889</p> -->
          </div>
          <div class="location">
            <img src="../assets/image/location.png" alt="">
            <input type="text" value="このはがくれ">
          </div>
        </div>
        <div class="upload-image">
          <div class="upload-btn-wrapper">
            <button class="btn"><img src="../assets/image/upload.png" alt="" width="35"></button>
            <input type="file" name="myfile"  @change="onUpload()"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import firebase from 'firebase'
// import db from '../firebaseInit'

export default {
  name: 'FriendsInfo',
  // props: ['myName'],
  data () {
    return {
      uploadValue: 0,
      picture: null,
      imageData: null,
      coordinates: {
        lat: 0,
        lng: 0
      }
    }
  },
  methods: {
    closeModal () {
      const closeMdl = document.querySelector('.profil')
      closeMdl.classList.add('hide')
    }
  },
  created () {
    this.$getLocation({})
      .then(coordinates => {
        this.coordinates = coordinates
      })
      .catch(error => alert(error))
    this.cariProfil()
  }

}
</script>

<style scoped>
  .profil{
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background-color: rgba(0, 0, 0, .50);
    /* display: none; */
  }
  .main-profil{
    width: 370px;
    height: 420px;
    background: #fff;
    margin: 80px auto;
    position: relative;
  }
  .hide{
    display: none;
  }
  .head-profil{
    height: 150px;
    background-color: #5580a3;
    display: flex;
    align-items: flex-end;
    box-sizing: border-box;
  }
  .close{
    position: absolute;
    left: 345px;
  }
  .close a{
    text-decoration: none;
    color: #fff;
  }
  #progress{
    width: 80px;
    height: 10px;
    position: absolute;
    top: 40px;
    left: 7px;
    /* border-radius: 1px; */
  }
  .photo{
    margin-left: 20px;
    margin-bottom: 10px;
    position: relative;
  }
  .photo img{
    width: 95px;
    height: 95px;
    border-radius: 50%;
    object-fit: cover;
  }
  .nama{
    margin-left: 10px;
  }
  /* .upload-profil{
    display: none;
  } */
  .upload-btn-wrapper {
  position: relative;
  overflow: hidden;
  display: inline-block;
}
.upload-image{
  position: absolute;
  top: 120px;
  left: 295px;
}
.phone, .location{
  width: 310px;
  margin-top: 40px;
  margin-left: 30px;
  display: flex;
  align-items: center;
  /* background-color: blueviolet; */
  border-bottom: 1px solid #ccc;
}
.phone img, .location img{
  width: 70px;
  margin-left: 20px;
  margin-bottom: 5px;
}
.phone input, .location input{
  margin-left: 20px;
  margin-top: 5px;
  font-size: 17px;
  border: none;
}
.btn {
  border: 2px solid gray;
  color: gray;
  background-color: white;
  border-radius: 50%;
  font-size: 20px;
  font-weight: bold;
  width: 60px;
  height: 60px;
}
.upload-btn-wrapper input[type=file] {
  font-size: 100px;
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0;
}
</style>
