<template>
  <input class="inputField" :type="setType" :placeholder="placeholder" :value="value"/>
  <img class="showPassImage" v-if="type==='password'" @click="toggleShowPassword()" src="../assets/backArrow.svg"/>
</template>

<script>
export default {
  name: 'InputComponent',
  data(){
    return {
      setType: this.type
    }
  },
  props: {
    type: String,
    placeholder: String,
    value: String
  },
  methods:{
    toggleShowPassword(){
      console.log(this.setType)
      if (this.setType === 'text'){
        this.setType = 'password'
      }      
      else if (this.setType === 'password'){
        this.setType = 'text'
      }
    }
  },
  computed:{
    computedType(){
      return this.setType;
    }
  }
}
</script>

<style>

  .inputField {
    padding: 10px;
    display: block;
    margin: 10px auto;
    width: 321px;
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

.showPassImage{
  cursor: pointer;
  max-width: 24px;
  position: relative;
    top: -2.8rem;
    left: 10rem;
}


</style>
