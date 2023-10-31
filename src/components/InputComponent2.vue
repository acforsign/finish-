<template>
    <div class="inputtext" >
      <b-form-input v-model="text" placeholder="Enter your favourite name " class="formtxt"></b-form-input>
      
    </div>
  </template>

<script>
export default {
    name: 'InputComponent2',

    data() {
        return {
          text: ''
        }
      },

    mounted() {
        
    },
    watch: {




      text(){
       
          this.$emit('inputHandeler', this.text)
          this.$emit('input3', this.text)
        
      }
    },

    methods: {
        
    },
};
</script>

<style lang="scss" scoped>

$babaColor: #00baba;
$lightGray: #f5f1f1;
$gray:#828282;
.inputtext{

   
  background-color: $lightGray;
  
  width: 16.58rem;
  
}

#input__3[data-v-01caf037] {
   
    background-color: $lightGray;
    
   
    
}

.formtxt{

    //background-color: $lightGray;
    
   background-color: $lightGray;


}
.formtxt:hover{

   //background-color: $lightGray;
   background-color: $lightGray;
    border: 1px solid $babaColor;
   


}
.formtxt:focus{

    background-color: $lightGray;
    border: 1px solid $babaColor;
   


}

.custom-select[data-v-62be3503]{

  color: $gray;


}

@media only screen and (max-width: 576px){

  .formtxt[data-v-15bfd682]{
  text-align: center;
  
  }
}



</style>


  
  