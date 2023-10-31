<template>
    <div class="enter">
      <b-form-select v-model="selected1" :options="options" class="custom-select"></b-form-select>
      <div class="mt-3"><strong>{{  }}</strong></div>
    </div>
  </template>
  
  <script>
    export default {
      data() {
        return {
          selected1: null,
          options: [
            { value: null, text: 'for example:126' },
            { value: 'unlimited', text: 'unlimited' },
            { value: '1', text: '1 ' },
            { value:  '100', text: '100 ' },
            { value: '1000', text: '1000' },

           
            
          ]
        };
      },
      watch:{
        selected1(){


          this.$emit('maxHandeler', this.selected1);
          this.$emit('input1', this.selected1);
        }
      }
    };
  </script>
  
  <style lang="scss" scoped>

$gray:#828282;
$lightGray: #f5f1f1;
@mixin borderMaker(){

background-color: $lightGray; 
border: none; 

}
@mixin padFunc($top,$right,$bottom,$left){


padding:$top $right $bottom $left;
-webkit-appearance: none;
-moz-appearance: none;
appearance: none;
text-align: center; 
}
  .enter {
    text-align: left; 
  }
  
  .custom-select {
   @include borderMaker();
   @include padFunc(0.375rem ,0.25rem ,0.375rem ,0.75rem);
    color: $gray;
  }
  
  .custom-select:focus {
    box-shadow: none; /* Remove focus box-shadow */
  }
  
  .custom-select option {
    border: none; /* Remove the border around the select options' text */
    
  }
  
  .custom-select option:selected {
    border: none; /* Remove the border around the selected option */
    
  }


  .custom-select[data-v-62be3503] {
   @include padFunc(0.375rem ,0.25rem ,0.375rem ,0.75rem);
    
    
  }

 
  .custom-select[data-v-15dc0584]{

width: 100%;
}
  
  </style>
  