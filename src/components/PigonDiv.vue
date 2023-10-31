<template>
    

  <div>

  <b-container>
  
   
      <b-col    cols="2" class="bg-white img__wrapper d-flex justify-content-evenly ">
        
        <div class="logo__wrapper-text"> 
            <div class="logo__wrapper">
            <img src="../assets/logo.png" alt="Image" class="logo">
          </div>
            <h4 class="logo__wrapper-h4">Pigeon</h4>
      </div>
      
      </b-col>
   
  </b-container>
</div>
</template>

<script >
export default {
  name: 'PigonDiv',
  props: {

  },
}
</script>

<style lang="scss" scoped>
/* Your SCSS styles here */


$darkBlue: #0B3A42;
@mixin posDirection($top,$right,$bottom,$left) {
top: $top;
right: $right;
bottom: $bottom;
left: $left;
position: absolute;

}




.logo__wrapper-text{
display: flex;
justify-content: space-evenly;
width: 100%;
margin-top: -4%;
gap: 18%;
height: 7rem;

}
.logo__wrapper{


margin-top:5%;

}



.img__wrapper{
 


  width: 260px;
  border-top-right-radius: 1.5rem;
  border-top-left-radius: 1.5rem;
  z-index:10;
  display: flex;
  
  margin-left: 50%;
  margin-top: 5%;
  
  
  
}





.logo{
  margin-top: 8%;
  margin-left: 50%;
 
  
}

.logo__wrapper-h4{

 
  font-weight: bold;
  margin-top: 8%;
  margin-right: 35%;
}


@media only screen and (max-width: 576px) {

.img__wrapper{


  
  margin-left: 0%;
}

}
@media only screen and (max-width: 990px) {

.img__wrapper{


  
  margin-left: -20%;
}

}

</style>
