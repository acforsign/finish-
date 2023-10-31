<template>
  <div class="check">
    <b-form-checkbox
      id="checkbox-1"
      v-model="status"
      name="checkbox-1"
      value="accepted"
      unchecked-value="not_accepted"
      class="d-flex justify-content-center"
      
      
    >
     <span class="zip__text"> Zip files</span>
    </b-form-checkbox>

   
  </div>
</template>

<script>
  export default {
    name:'CheckBox',
     // boolean
    data() {
      return {
        status: 'not_accepted',
      }
    },


    
    methods: {
   

 

    },
    computed:{

      

    },
    watch:{

      status(){
        if (this.status==='accepted'){
        this.$emit('enable',this.status);
      }
      }
    }
  }
</script>
<style scoped lang="scss">
$babaColor: #00baba;

@mixin mrg($top,$right,$bottom,$left){

margin-top: $top;
margin-right: $right;
margin-bottom: $bottom;
margin-left: $left;

};
@mixin flexMargin($width,$top,$right,$bottom,$left) {
  @include mrg($top,$right,$bottom,$left);
  display: flex;
  width: $width;

}

  



.check{
@include flexMargin(10%,0 ,0 ,0 , 12%);

padding: 1rem;
z-index: 3000;
font-size: 14px;


}

.zip__text{
  @include flexMargin(100%,0.5rem ,0.5rem, 0.5rem, 0.5rem);

    flex-wrap: nowrap;
}


.custom-control-input:checked + .custom-control-label::before {
  border-color: $babaColor;
  background-color: $babaColor;
}


.custom-checkbox .custom-control-input:checked .custom-control-indicator {
  background-color: $babaColor;
}

</style>