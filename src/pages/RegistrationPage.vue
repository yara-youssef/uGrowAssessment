<template>
<div class="mainDiv">
    <div class="headerDiv">
        <img src="../assets/backArrow.svg" class="backArrow" @click="goBack()"/> 
        <progress class="progressBar" max="100" :value="progress"></progress>
    </div>
        <div class="contentDiv"> 
            <span v-if="pageNumber===1 || pageNumber==2">
            <h1> Hey{{pageNumber > 1 ? ' ['+firstName+']' :''}}! </h1>
            <p   class="mainParagraph"> Schön, dass du hier bist. Melde Dich jetzt an und starte mit uns in eine grüne und gesunde Zukunft! </p>
            </span>

            <span v-if="pageNumber===1">
                 <input class="inputField" :type="textInput" v-model="firstName" :placeholder="'Dein Vorname'" :value="firstName"/>
                 <input class="inputField" :type="textInput" v-model="lastName" :placeholder="'Dein Nachname'" :value="lastName"/>
           </span>

             
            <span v-if="pageNumber===2">
                
                 <input class="inputField" :class="checkEmailValidity(email) && email !=''? '' : 'notValidInputField'" :type="emailInput" v-model="email" :placeholder="'Deine Emailadresse'" />
                 <input class="inputField" :class="checkPasswordValidity(password) && password !=''? '' : 'notValidInputField'" :type="passwordInputFieldType" v-model="password" :placeholder="'Passwort'" />
                  <img class="showPassImage" @click="isShownPassword=!isShownPassword" src="../assets/backArrow.svg"/>

                <div v-if="!checkPasswordValidity(password)"> 
                    Dein Passwort muss folgende Voraussetzungen erfüllen: <br>
                  <span>{{password.length >= 8 ? '✓' : 'x'}}</span>   Es muss 8 Zeichen umfassen <br/>
                    <span>{{checkPasswordLetter(password) ? '✓' : 'x'}}</span> Es muss mind. 1 Buchstabe enthalten <br/>
                  <span>{{checkPasswordNumber(password) ? '✓' : 'x'}}</span>   Es muss mindestens 1 Zahl enthalten <br/>
                </div> 

            </span>

            <button v-if="pageNumber===1 || pageNumber===2" :disabled="disableWeitarButton" @click="weiterFunction" class="buttonField">Weiter</button>

             
            <span v-if="pageNumber===3">
                <h1>Wunderbar!</h1>
                 <p class="mainParagraph">
Willkommen bei urgrow! Wir helfen dir nun dein Basecamp mit der App zu verbinden und deine Pflanzen der App zuzuordnen.
                 </p>

                  <p class="mainParagraph">
                      Schau dir für den Aufbau deines Basecamps unser Onboarding Tutorial an oder starte direkt mit der Basecampeinrichtung über die App.
                  </p>

                <button class="buttonField">Zum Youtube Tutorial</button>
                
                <button class="buttonField">Einrichtung mit App starten</button>

            </span>

           
        </div>
    </div>

</template>

<script>
// import InputComponent from '../components/InputComponent.vue'

export default {
  name: 'RegistrationPage',
  data(){
      return{
          firstName: '',
          lastName: '',
          email: '',
          password: '',
          isShownPassword: false,
        
         pageNumber: 1,

          textInput: 'text',
          passwordInput: 'password',
          emailInput: 'email',
      }
  },
  components:{
    // InputComponent
  },
  methods:{
      goBack(){
          if(this.pageNumber>1){
              this.pageNumber--;
          }
      },
      checkPasswordValidity(password){
          if(password!='' & password.length >= 8){
            return this.checkPasswordLetter(password) && this.checkPasswordNumber(password)
          }
          return false;
      },
      checkPasswordLetter(password){
          var letterTest = /[a-zA-Z]/g;
          return letterTest.test(password);

      },
      checkPasswordNumber(password){
          var numberTest = /\d+/g;
          return numberTest.test(password);
      },
      checkEmailValidity(email){
          var mailformat = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return mailformat.test(email);
      },
      weiterFunction(){
          console.log('in weiter')
          if (this.pageNumber === 1 && this.firstName !='' && this.lastName !=''){
              this.pageNumber = 2
          }
          else if (this.pageNumber === 2 && this.checkPasswordValidity(this.password) && this.checkEmailValidity(this.email)){
               this.pageNumber = 3
          }
      }
  },
  computed:{
      progress(){
          console.log('progressing');
           if (this.pageNumber === 1){
               return 33;
           }
          else if (this.pageNumber === 2){
              return 66;
          }
          else if (this.pageNumber === 3){
              return 100;
          }
          else{
              return 0
          }
          
      },
      passwordInputFieldType(){
          if (this.isShownPassword){
              return this.textInput;
          }
          return this.passwordInput;

      },
      disableWeitarButton(){
          if (this.pageNumber === 1){
              return (this.firstName ==='' && this.lastName ==='')
          }
          else if (this.pageNumber === 2){
              return !(this.checkPasswordValidity(this.password) && this.checkEmailValidity(this.email))
          }
          return true;
      }
  }
}
</script>

<style scoped>
.mainDiv{
    min-height: 75vh;
    padding: 10px;
    backdrop-filter: blur(20px);

}

.headerDiv{

}
.backArrow{
    max-width: 24px;
    color: red;
    position: absolute;
    top: 10px;
    left: 10px;
    cursor: pointer;
}

.progressBar::-moz-progress-, ::-webkit-progress-value, ::-webkit-progress-bar{
  background: red;
}

.contentDiv{

}

.mainParagraph{
    color: #383838;
    font-size: 14px;
}

.weiterButton{

}

.buttonField{
    cursor: pointer;
       padding: 10px;
    display: block;
    margin: 10px auto;
    width: min(321px, 90%);
    color: #FFFFFF;
    font-family: Poppins;
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 24px;
    border-radius: 25px;
    background-color: #41BAFF;
    border: 0;
    outline: none;
}


  .inputField {
    padding: 10px;
    display: block;
    margin: 10px auto;
    width: min(321px, 90%);
    color: #D7D8D9;
    font-family: Poppins;
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 24px;
    border-radius: 25px;
    background-color: #38383880;
    border: 0;
    outline: none;
  }

  .inputField::placeholder, .inputField::-webkit-input-placeholder  { 
  color: #D7D8D9;
}

.notValidInputField{
        border: 1px solid #E8635A;
}

.showPassImage{
  cursor: pointer;
  max-width: 24px;
  position: relative;
    top: -2.8rem;
    left: 10rem;
}

</style>
