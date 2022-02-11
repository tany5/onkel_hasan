<template>
  <div class="template">
    <div class="preloader" v-show="isLoading">
      <div class="loader">
        <div class="loader-circle"></div>
        <span>Onkel <br />Hasan</span>
      </div>
    </div>
    <!-- Start Coming Soon Area -->
        <div class="coming-soon-area" >          
            <div class="coming-soon-content">
                <div class="logo">
                    <a href="/"><img src="../assets/logo.png" alt="image"></a>
                </div>
                <h1 v-show="!isLoading">
                    <span class="typed-text" v-html="typeValue"></span>
                    <span class="cursor" :class="{'typing': typeStatus}">&nbsp;</span>
                </h1>                                                      
                <p>Grabenweg 4, 6020 Innsbruck, Austria</p>
                
                <div class="newsletter">
                    <!-- <h2>Subscribe To Our Newsletter</h2>
                    <p>Being the first to know always feels great. Signing up to our newsletter gives you exclusive access to our Grand Opening!</p> -->
                    <form class="newsletter-form" data-toggle="validator" novalidate="true">
                        <input type="email" class="input-newsletter" placeholder="Enter email address" name="EMAIL" required="" autocomplete="off">    
                        
                        <button type="submit" class="disabled" style="pointer-events: all; cursor: pointer;">Subscribe Now</button><div id="validator-newsletter" class="form-result"></div>
                    </form>
                </div>
            </div>                 
        </div>               
    <!-- End Coming Soon Area -->
    
  </div>
</template>

<script>
export default {
  data() {
    return {
        isLoading: true,
        typeValue: '',
        typeStatus: false,
        typeArray: ['Kaming Suun'],
        typingSpeed: 200,
        erasingSpeed: 100,
        newTextDelay: 2000,
        typeArrayIndex: 0,
        charIndex: 0
    };
  },
   methods: {
      typeText() {
        if(this.charIndex < this.typeArray[this.typeArrayIndex].length) {
          if(!this.typeStatus)
            this.typeStatus = true;
          this.typeValue += this.typeArray[this.typeArrayIndex].charAt(this.charIndex);
          this.charIndex += 1;
          setTimeout(this.typeText, this.typingSpeed);
        }
        else {
          this.typeStatus = false;
          setTimeout(this.eraseText, this.newTextDelay);
        }
      },
      eraseText() {
        if(this.charIndex > 0) {
          if(!this.typeStatus)
            this.typeStatus = true;
          this.typeValue = this.typeArray[this.typeArrayIndex].substring(0, this.charIndex - 1);
          this.charIndex -= 1;
          setTimeout(this.eraseText, this.erasingSpeed);
        }
        else {
          this.typeStatus = false;
          this.typeArrayIndex += 1;
          if(this.typeArrayIndex >= this.typeArray.length)
            this.typeArrayIndex = 0;
          setTimeout(this.typeText, this.typingSpeed + 1000);
        }
      }
    },
  created() {
        setTimeout(() => this.isLoading = false, 4000)
        setTimeout(this.typeText, this.newTextDelay + 2000);
    } 
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Hind:300,400,500,600,700&display=swap");
@import url("https://fonts.googleapis.com/css?family=Dosis:200,300,400,500,600,700,800&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@500&display=swap');
.template {
  width: 100%;
  height: 100%;
}
/*================================================
Preloader CSS
=================================================*/
.preloader {
  position: fixed;
  left: 0;
  width: 0;
  height: 100%;
  width: 100%;
  text-align: center;
  z-index: 9999999;
  background-color: #272b31;
  font-family: 'Dancing Script', cursive;
}

.preloader .loader {
  width: 150px;
  height: 150px;
  position: absolute;
  left: 0;
  right: 0;
  margin: 0 auto;
  top: 45%;
  -webkit-transform: translateY(-45%);
  transform: translateY(-45%);
  border-radius: 50%;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.preloader .loader-circle {
  border-top: 5px solid red;
  border-radius: 50%;
  width: 100%;
  height: 100%;
  -webkit-animation: spin 1.5s linear infinite;
  animation: spin 1.5s linear infinite;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
}

.preloader span {
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  margin: 0 auto;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
  text-transform: capitalize;
  color: #ffffff;
  font-size: 40px;
  font-weight: 700;
}

@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}


/*================================================
Coming Soon Area CSS
=================================================*/
.coming-soon-area {
  height: 100vh;
  position: relative;
  overflow: hidden;
  z-index: 1;
  background-image: url('~@/assets/img/main-bg7.jpg');
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;  
  font-family: "Hind", sans-serif;
}

.coming-soon-area::before {
  position: absolute;
  left: 0;
  top: 0;
  z-index: -1;
  width: 100%;
  height: 100%;
  background-color: #000000;
  content: '';
  opacity: .30;
}

.coming-soon-area::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  z-index: -2;
    -webkit-animation: movescale 20s linear infinite;
            animation: movescale 20s linear infinite;
    background-image: url('~@/assets/img/bg-shape.png');
  background-position: center center;
  background-size: cover;
  background-repeat: no-repeat;
}

.coming-soon-content {
    position: absolute;
    width: 100%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50% );
    text-align: center;
}

.coming-soon-content .logo {
  margin-bottom: 40px;
}

.coming-soon-content .logo a {
  display: inline-block;
}

.coming-soon-content h5 {
  display: block;
  color: #f39d07;
  margin-bottom: 18px;
  line-height: initial;
  font-size: 22px;
  font-weight: 600;
  font-family: "Dosis", sans-serif;
}

.coming-soon-content h5 span {
  color: #ffffff;
}
.coming-soon-content p {
  color: #f4f4f4;
  max-width: 550px;
  line-height: 1.7;
  font-family: "Dosis", sans-serif;
  font-size: 27px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 0;
  margin-top: 5px;
}

@-webkit-keyframes movescale {
  0% {
    -webkit-transform: scale(1);
            transform: scale(1);
  }
  50% {
    -webkit-transform: scale(1.5);
            transform: scale(1.5);
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
  }
}

@keyframes movescale {
  0% {
    -webkit-transform: scale(1);
            transform: scale(1);
  }
  50% {
    -webkit-transform: scale(1.5);
            transform: scale(1.5);
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
  }
}

.coming-soon-content h1 {
    max-width: 700px;    
    color: #ffffff;
    line-height: 1.1;
    font-size: 80px;
    font-weight: 700;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 0;
    font-family: "Hind", sans-serif;
    text-transform: capitalize;    
    font-size: 40px;
}
    .coming-soon-content h1 span.typed-text {
      color: #ffd82c;
      /*font-family: 'Dancing Script', cursive;*/
      font-style: italic;
      /* text-decoration:underline;
      text-decoration-color: #fd3d2a; */
    }
   .coming-soon-content h1 span.cursor {
      display: inline-block;
      margin-left: 3px;
      width: 4px;
      background-color: #fff;
      animation: cursorBlink 1s infinite;
    }
   .coming-soon-content h1 span.cursor.typing {
      animation: none;
    }
  
  @keyframes cursorBlink {
    49% { background-color: #fff; }
    50% { background-color: transparent; }
    99% { background-color: transparent; }
  }

  .newsletter {
    color: #fff;
  }
  .newsletter h2{
    margin-bottom: 0;
    margin-top: 30px;
    font-size: 25px;
    font-weight: 600;
    color: #f39d07;
  }
 .newsletter p{
    font-size: 17px;
    max-width: 520px;
    line-height: 1.7;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 0;
    margin-top: 13px;
 }
 form {
    position: relative;
    max-width: 500px;
    -webkit-box-shadow: 0 5px 28.5px 1.5px rgb(149 152 200 / 20%);
    box-shadow: 0 5px 28.5px 1.5px rgb(149 152 200 / 20%);
    border-radius: 30px;
    margin-left: auto;
    margin-right: auto;
    margin-top: 35px;
    display: flex;
}

 .input-newsletter {
    display: inline-block;
    width: 100%;
    background-color: #ffffff;
    border: none;
    outline: 0;
    -webkit-transition: 0.5s;
    transition: 0.5s;
    border-radius: 30px;
    height: 50px;
    font-size: 13.5px;
    padding: 0px;
    padding-left: 21px;
}

form button {
    position: absolute;
    right: 0;
    top: 0;
    height: 50px;
    border-radius: 0 30px 30px 0;
    border: none;
    background-color: #fd3d2a;
    outline: 0;
    color: #ffffff;
    -webkit-transition: 0.5s;
    transition: 0.5s;
    font-family: "Dosis", sans-serif;
    font-size: 16px;
    font-weight: 600;
    padding-left: 15px;
    padding-right: 15px;
}

@media only screen and (max-width: 767px) {
  .coming-soon-area:after {    
    bottom: 0px;
    background-position: 57% !important;
    background-size: auto;
    background-repeat: no-repeat;
    z-index: -1;
}
form {
  margin-top: 16px;
  padding: 0px 6px;
}
 form button{
   right: 6px;
 }  
 .newsletter p{
   padding: 0 6px !important;
   margin: 0 ;
 } 
 .newsletter h2{
   margin-top: 5px;
 } 
  .coming-soon-content h5 {
    margin-bottom: 15px;
    font-size: 18px;
  }
  .coming-soon-content h1 {
    max-width: 100%;
    line-height: 1.2;
    font-size: 28px;
  }
  .coming-soon-content p {
    font-size: 18px;
    padding: 6px;
    font-weight: 700;
    line-height: 1.5;
  } 
  
}

@media only screen and (min-width: 667px) and (max-width: 767px) {
  .coming-soon-area {
    height: 100%;
    padding-top: 210px;
    padding-bottom: 170px;
  }
  .coming-soon-content {
    margin-top: 0;
  }
}

@media only screen and (min-width: 576px) and (max-width: 767px) {
  .coming-soon-content h5 {
    font-size: 19px;
  }
  .coming-soon-content h1 {
    font-size: 44px;
  }
  .coming-soon-content p {
    font-size: 17px;
  }
  .coming-soon-content #timer div {
    font-size: 50px;
    margin-left: 15px;
    margin-right: 15px;
  }
  .coming-soon-content #timer div span {
    font-size: 18px;
  }
  
}

@media only screen and (min-width: 768px) and (max-width: 991px) {  
  
  .coming-soon-content {
    margin-top: 50px;
  }
  /* .coming-soon-content .logo {
    display: none;
  } */
  .coming-soon-content h5 {
    font-size: 20px;
  }
  .coming-soon-content h1 {
    font-size: 65px;
  }
  .coming-soon-content #timer div {
    font-size: 50px;
    margin-left: 25px;
    margin-right: 25px;
  }
  
}


  
/*# sourceMappingURL=responsive.css.map */
</style>
