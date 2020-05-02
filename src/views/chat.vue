<template>
  <div>
    <div class="luar">
    <div class="container">
      <!-- <img src="../assets/image/chatMee1.png" alt="" width="130" class="chatmee"> -->
      <h1 class="title">chatMee</h1>
      <div class="messaging">
      <div class="inbox_msg">
        <div class="inbox_people">
          <div class="headind_srch">
            <div class="recent_heading">
              <div class="dropdown">
               <button class="btn" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"><img src="../assets/image/menu.svg" alt="" width="25"></button>
                <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                  <a class="dropdown-item" href="#">Profil</a>
                  <a class="dropdown-item" href="#">About</a>
                  <a class="dropdown-item" href="#" @click="logout">Logout</a>
                </div>
              </div>
            </div>
            <div class="srch_bar">
              <div class="stylish-input-group">
                <input type="text" class="search-bar"  placeholder="Search" >
                <span class="input-group-addon">
                <button type="button"> <i class="fa fa-search" aria-hidden="true"></i> </button>
                </span> </div>
            </div>
          </div>
          <div class="chat-contact">
            <div class="list-friends" v-for="contact in this.profil" :key="contact.id">
              <div class="private" @click="cobaCoba" v-if="contact.email !== authUser.email">
                <div class="private-image">
                  <img :src="contact.imageProfil" alt="">
                </div>
                <div class="firends-name">
                  <h5>{{contact.displayName}}</h5>
                    <p>{{contact.email}}</p>
                 </div>
              </div>
            </div>
          </div>
        </div>
        <div class="messages">
          <div class="contact-name">
            <div class="listimage">
              <img :src="bannerName.imageProfil" alt="" >
            </div>
            <div class="listname">
              <h3>{{bannerName.displayName}}</h3>
            </div>
          </div>
          <div class="chat-empty full">
            <h1>Please select a chat to start messaging</h1>
          </div>
          <div class="mesgs">
            <div class="msg_history">
              <div class="incoming_msg" >
                <div class="received_msg" v-for="chat in messages" :key="chat.id">
                <div :class="[chat.sender === authUser.email? 'received_msg': 'sent_msg']" >
                  <p>{{chat.message}}</p>
                  </div>
              </div>
            </div>
            </div>
              <div class="type_msg">
              <div class="input_msg_write">
                <input type="text" class="write_msg" placeholder="Type a message" v-model="message"/>
                <button class="msg_send_btn" type="button" @click="sendMessage"><i class="fa fa-paper-plane-o" aria-hidden="true"></i></button>
              </div>
          </div>
          <!-- <div class="mesgs">
            <div class="msg_history">
              <div class="incoming_msg" >
                <div class="received_msg" v-for="chat in personalChat" :key="chat.id">
                <div :class="[chat.sender === authUser.email? 'received_msg': 'sent_msg']" >
                  <p>{{chat.message}}</p>
                  </div>
              </div>
            </div>
            </div>
              <div class="type_msg">
              <div class="input_msg_write">
                <input type="text" class="write_msg" placeholder="Type a message" v-model="message"/>
                <button class="msg_send_btn" type="button" @click="sendMessage"><i class="fa fa-paper-plane-o" aria-hidden="true"></i></button>
              </div>
          </div> -->
          </div>
        </div>
      </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase'
import db from '../firebaseInit'
export default {
  name: 'chat',
  data () {
    return {
      message: null,
      messages: [],
      authUser: {},
      profil: [],
      myContact: '',
      bannerName: [],
      personalChat: []
    }
  },
  methods: {
    sendMessage () {
      db.collection('chat').add({
        message: this.message,
        sender: this.authUser.email,
        received: this.bannerName.email,
        createdAt: new Date()
      })
      this.message = null
    },
    showMessage () {
      db.collection('chat').where('received', '==', this.authUser.email).where('sender', '==', this.bannerName.email).orderBy('createdAt').onSnapshot((querySnapshot) => {
        var allMessage = []
        querySnapshot.forEach(doc => {
          allMessage.push(doc.data())
        })
        this.messages = allMessage
      })
    },
    logout () {
      firebase.auth().signOut()
        .then(() => {
          this.$router.go({ path: this.$router.path })
        })
    },
    getUser () {
      db.collection('users').onSnapshot((querySnapshot) => {
        querySnapshot.forEach(doc => {
          this.profil.push(doc.data())
        })
      })
    },
    cobaCoba (e) {
      const empty = document.querySelector('.chat-empty')
      const chat = document.querySelector('.mesgs')
      empty.classList.add('full')
      chat.classList.toggle('full')
      this.myContact = e.target.textContent
      this.bannerContact()
      this.showMessage()
    },
    bannerContact () {
      for (let i = 0; i < this.profil.length; i++) {
        if (this.profil[i].displayName === this.myContact) {
          this.bannerName = this.profil[i]
        }
      }
      // this.chatPersonal()
    },
    chatPersonal () {
      for (let i = 0; i < this.messages.length; i++) {
        if (this.messages[i].sender === this.authUser.email && this.messages[i].received === this.bannerName.email) {
          this.personalChat.push(this.messages[i])
          console.log(this.personalChat)
        }
      }
    }
  },
  created () {
    if (firebase.auth().currentUser) {
      this.authUser = firebase.auth().currentUser
    }
    // this.showMessage()
    this.getUser()
  }
}
</script>

<style scoped>
.luar{
  background-color: #5580a3;
}
    .container{max-width:1170px; margin:auto;}
    img{ max-width:100%;}
    .title{
      padding-top: 10px;
      padding-bottom: 10px;
      color: #fff;
    }
    .inbox_people {
      background: #f8f8f8 none repeat scroll 0 0;
      float: left;
      /* overflow: hidden; */
      width: 40%; border-right:1px solid #c4c4c4;
    }
    .chat-contact{
      height: 600px;
      background-color: #fff;
      overflow-y: scroll;
    }
    /* .list-friends{
      overflow-y: scroll;
    } */
    .private{
      height: 85px;
      background-color:#fff;
      display: flex;
      margin-top: 10px;
      cursor: pointer;
    }
    .private:hover{
      background-color: #c4c4c4;
    }
    .full{
      display: none;
    }
    .private-image img{
      width: 70px;
      margin-top: 6px;
      margin-left: 10px;
    }
    .firends-name{
      margin-left: 30px;
      margin-top: 19px;
    }
    .messages{
      display: flex;
      flex-direction: column;
    }
    .contact-name{
      display: flex;
      align-items: center;
      width: 100%;
      /* height: 20px; */
      padding-top: 5px;
      padding-bottom: 5px;
      background-color: #fff;
    }
    .contact-name img{
      width: 50px;
      margin-left: 30px;
      /* padding-bottom: 10px; */
    }
    .listname h3{
      margin-left: 50px;
    }
    .chat-empty{
      position: absolute;
      top: 45%;
      left: 60%;
      width: 210px;
    }
    .chat-empty h1{
      font-size: 20px;
      text-align: center;
      color: #ccc;
    }
    .inbox_msg {
      border: 1px solid #c4c4c4;
      clear: both;
      overflow: hidden;
      position: relative;
    }
    .top_spac{ margin: 20px 0 0;}
    .recent_heading {float: left; width:40%;}
    .srch_bar {
      display: inline-block;
      text-align: right;
      width: 60%;
    }
    .headind_srch{
      padding:10px 29px 10px 20px;
      margin-bottom: 5px;
      /* overflow:hidden; */
      border-bottom:1px solid #c4c4c4;
    }
    .recent_heading h4 {
      color: #05728f;
      font-size: 21px;
      margin: auto;
    }
    .srch_bar input{
      border:1px solid #cdcdcd;
      border-width:0 0 1px 0; width:80%;
      padding:2px 0 4px 6px;
      background:none;
    }
    .srch_bar .input-group-addon button {
      background: rgba(0, 0, 0, 0) none repeat scroll 0 0;
      border: medium none;
      padding: 0;
      color: #707070;
      font-size: 18px;
    }
    .srch_bar .input-group-addon { margin: 0 0 0 -27px;}

    .chat_ib h5{ font-size:15px; color:#464646; margin:0 0 8px 0;}
    .chat_ib h5 span{ font-size:13px; float:right;}
    .chat_ib p{ font-size:14px; color:#989898; margin:auto}
    .chat_img {
      float: left;
      width: 11%;
    }
    .chat_ib {
      float: left;
      padding: 0 0 0 15px;
      width: 88%;
    }

    .chat_people{
      overflow:hidden;
      clear:both;
      padding-bottom: 30px;
      cursor: pointer;
    }
    .chat_people:hover{
      background-color: #fff;
    }
    .chat_list {
      border-bottom: 1px solid #c4c4c4;
      margin: 0;
      padding: 18px 16px 10px;
    }
    .inbox_chat {
      height: 550px;
      overflow-y: scroll;
    }

    .active_chat{ background:#ebebeb;}

    .incoming_msg_img {
      display: inline-block;
      width: 6%;
    }
    .received_msg {
      display: inline-block;
      padding: 0 0 0 10px;
      vertical-align: top;
      width: 92%;
    }
    .received_withd_msg p {
      background: #ebebeb none repeat scroll 0 0;
      border-radius: 3px;
      color: #646464;
      font-size: 14px;
      /* margin-bottom: 15px; */
      padding: 5px 10px 5px 12px;
      width: 100%;
      /* height: 40px; */
      /* line-height: 25px; */
      border-radius: 10px;
    }
    .time_date {
      color: #747474;
      display: block;
      font-size: 12px;
      margin: 8px 0 0;
    }
    .received_withd_msg { width: 57%;}
    .mesgs {
      float: left;
      padding: 30px 15px 0 25px;
      width: 60%;
    }
    .sent_msg p {
      background: #05728f none repeat scroll 0 0;
      border-radius: 3px;
      font-size: 14px;
      /* margin-bottom: 15px; */
      color:#fff;
      padding: 5px 10px 5px 12px;
      border-radius: 10px;
      /* line-height: 25px; */
      width:100%;
      /* height: 40px; */
    }
    .outgoing_msg{ overflow:hidden; margin:26px 0 26px;}
    .sent_msg {
      float: right;
      width: 46%;
    }
    .input_msg_write input {
      background: rgba(0, 0, 0, 0) none repeat scroll 0 0;
      border: medium none;
      color: #4c4c4c;
      font-size: 15px;
      min-height: 48px;
      width: 100%;
    }

    .type_msg {border-top: 1px solid #c4c4c4;position: relative;}
    .msg_send_btn {
      background: #05728f none repeat scroll 0 0;
      border: medium none;
      border-radius: 50%;
      color: #fff;
      cursor: pointer;
      font-size: 17px;
      height: 33px;
      position: absolute;
      right: 0;
      top: 11px;
      width: 33px;
    }
    .messaging { padding: 0 0 50px 0;}
    .msg_history {
      height: 516px;
      overflow-y: auto;
    }
    .chatmee{
      margin-left: 500px;
    }
</style>
