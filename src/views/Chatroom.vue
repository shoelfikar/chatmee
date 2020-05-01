<template>
  <div>
    <div class="container">
      <nav class="navbar navbar-light">
        <div class="menu">
          <a class="navbar-brand" href="#">
            <img src="../assets/image/menu.svg" width="20" alt="">
            <!-- <img src="../assets/image/chatMee1.png" width="80"  alt=""> -->
          </a>
        </div>
        <div class="icon">
          <a class="navbar-brand" href="#">
          </a>
        </div>
      </nav>
      <div class="row">
        <div class="col-md-4 listmenu">
          <div class="friends-search">
            <input type="text" placeholder="Search">
          </div>
          <div class="chatlist">
            <div class="friends" @click="chatmee">
              <div class="photo">
                <img src="../assets/image/user.png" alt="" @click="chatmee">
              </div>
              <div class="message">
                <div class="name">

                </div>
                <div class="sending">
                  <h3>Ismail</h3>
                  <p>Hello</p>
                </div>
              </div>
              <div class="times">
                <p>8:17 PM</p>
              </div>
            </div>
            <div class="friends">
              <div class="photo">
                <img src="../assets/image/user.png" alt="">
              </div>
              <div class="message">
                <div class="name">

                </div>
                <div class="sending">
                  <h3>Ismail</h3>
                  <p>Hello</p>
                </div>
              </div>
              <div class="times">
                <p>8:17 PM</p>
              </div>
            </div>
            <div class="friends">
              <div class="photo">
                <img src="../assets/image/user.png" alt="">
              </div>
              <div class="message">
                <div class="name">

                </div>
                <div class="sending">
                  <h3>Ismail</h3>
                  <p>Hello</p>
                </div>
              </div>
              <div class="times">
                <p>8:17 PM</p>
              </div>
            </div>
            <div class="friends">
              <div class="photo">
                <img src="../assets/image/user.png" alt="">
              </div>
              <div class="message">
                <div class="name">

                </div>
                <div class="sending">
                  <h3>Ismail</h3>
                  <p>Hello</p>
                </div>
              </div>
              <div class="times">
                <p>8:17 PM</p>
              </div>
            </div>
            <div class="friends">
              <div class="photo">
                <img src="../assets/image/user.png" alt="">
              </div>
              <div class="message">
                <div class="name">

                </div>
                <div class="sending">
                  <h3>Ismail</h3>
                  <p>Hello</p>
                </div>
              </div>
              <div class="times">
                <p>8:17 PM</p>
              </div>
            </div>
            <div class="friends">
              <div class="photo">
                <img src="../assets/image/user.png" alt="">
              </div>
              <div class="message">
                <div class="name">

                </div>
                <div class="sending">
                  <h3>Ismail</h3>
                  <p>Hello</p>
                </div>
              </div>
              <div class="times">
                <p>8:17 PM</p>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-8 chatbody">
          empty
          <div class="displaymsg hide">
            <article>
              chat disini aja ya!!!
            </article>
          </div>
          <div class="inputmsg">
            <input type="text">
            <button class="btn btn-outline-primary">Send</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Chatroom',
  methods: {
    chatmee () {
      // const friends = document.querySelector('.friends')
      const displayMsg = document.querySelector('.displaymsg')
      displayMsg.classList.toggle('hide')
    }
  }
}
</script>

<style scoped>
  .navbar{
    display: flex;
    background: #5580a3;
  }
  .menu{
    width: 30%;
    height: 55px;
    /* background-color: cornflowerblue; */
  }
  .listmenu{
    display: flex;
    flex-direction: column;
  }
  .chatbody{
    position: relative;
  }
  .inputmsg{
    position: absolute;
    bottom: 0;
    /* padding-bottom: 20px; */
    margin-top: 50px;
    margin-bottom: -15px;
  }
  .inputmsg input{
    width: 600px;
    height: 38px;
    margin-right: 20px;
    border-radius: 25px;
    font-size: 20px;
    padding-left: 10px;
    border: 1px solid #5580a3;
  }
  .inputmsg button {
    width: 100px;
    height: 38px;
    border-radius: 20px;
  }
  .displaymsg{
    width: 100%;
    height: 460px;
    margin-top: 10px;
    background-color: #ddd;
  }
  .hide{
    display: none;
  }
  .friends-search {
    margin-bottom: 20px;
  }
  .icon{
    width: 70%;
    /* background-color: darkblue; */
  }
  /* .col-md-4{
    background-color: cadetblue;
  } */
  /* .col-md-8{
    background-color: chocolate;
  } */
  .friends{
    display: flex;
    justify-content: space-between;
    cursor: pointer;
  }
  .friends:hover{
    background: #ddd;
  }
</style>
