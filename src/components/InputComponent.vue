<template>
    <div class="enter">
      <b-form-select v-model="selected" :options="options" class="custom-select" ></b-form-select>
      
    </div>
  </template>
  
  <script>
    export default {
      data() {
        return {
          selected: null,
          options: [
            { value: null, text: 'for example:6 month' },
            { value: 'unlimited', text: 'unlimited' },
            { value: '1 day', text: '1 day' },
            { value:  '1 month', text: '1 month ' },
            { value: '6 month', text: '6 month' },
            { value: '1 year', text: '1 year' },
           
            
          ]
        };
      },

      methods: {
    handleSelectChange() {
      if (this.selected && this.selected !== 'unlimited') {
        const currentDate = new Date();
        let expirationDate;

        switch (this.selected) {
          case '1 day':
            expirationDate = new Date(currentDate.getTime() + 1 * 24 * 60 * 60 * 1000);
            break;
          case '1 month':
            expirationDate = new Date(currentDate.setMonth(currentDate.getMonth() + 1));
            break;
          case '6 month':
            expirationDate = new Date(currentDate.setMonth(currentDate.getMonth() + 6));
            break;
          case '1 year':
            expirationDate = new Date(currentDate.setFullYear(currentDate.getFullYear() + 1));
            break;
          default:
            break;
        }

        const formattedDate = this.formatDateToCustomFormat(expirationDate);
        this.$emit('dateHandler', formattedDate);
      } else {
        this.$emit('dateHandler', this.selected);
      }

      this.$emit('input', this.selected);
      
      this.$emit('handleSelectChange');
    },

    formatDateToCustomFormat(date) {
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const day = String(date.getDate()).padStart(2, '0');
      const hours = String(date.getHours()).padStart(2, '0');
      const minutes = String(date.getMinutes()).padStart(2, '0');
      const seconds = String(date.getSeconds()).padStart(2, '0');

      return `${year}-${month}-${day} ${hours}:${minutes}:${seconds}`;
    },
  },



      watch:{

        selected(){

         
           this.$emit('dateHandler',this.handleSelectChange);
           this.$emit('input', this.selected);
           
          
       }
       },



      
    };
  </script>
  
  <style lang="scss" scoped>

$gray:#828282;
$lightGray:#f5f1f1;
@mixin padFunc($top,$right,$bottom,$left){


    padding:$top $right $bottom $left;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    text-align: center; 
}
  @mixin borderMaker(){

    background-color: $lightGray; 
    border: none; 

  }
  .enter {
    text-align: left; 
  }
  
  .custom-select {
      @include borderMaker();
      @include padFunc(0.375rem,0.25rem,0.375rem,0.75rem); 
    
   
  }
  
  .custom-select:focus {
    box-shadow: none; 
  }
  
  .custom-select option {
    border: none;
  }
  
  .custom-select option:selected {
    border: none; 
  }


  .custom-select[data-v-62be3503] {
    
    @include borderMaker();
    @include padFunc(0.375rem,0.25rem,0.375rem,0.75rem); 
    color: $gray;
  }

  
  .custom-select[data-v-62be3503][data-v-62be3503]{

    width: 100%;
  }
  
  @media only screen and (max-width: 576px){
   

  }
  
  </style>
  