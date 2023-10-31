<template>
  
  <div class="container">
    
      <div class="white-block" >
        <b-container class="bv-example-row inputcontainer">
         
           <div class="wrapper">
              <div  class="input-h-p one-input-wrapper">
                    <h5 class="inputcontainer__h5 ex-date broke-1">Expiration date</h5>
                  
                          <InputComponent
                      v-model="inputData1"
                      id="input__1"
                      class="enter"
                     @input="Func1"  @dateHandler="handleInput1" @handleSelectChange="handleSelectChangeInParent" />
              </div>

   
              <div class="input-h-p">
                <h5 class="inputcontainer__h5 broke " >Maximum download times</h5>
              
                <InputComponent1
                v-model="inputData2"
                id="input__2"
                class="enter"
                ref="inputComponent1Ref"
               @input1="Func2" @maxHandeler="handleInput2"  />
            
              </div>


         
              <div class="input-h-p"  id="inpu3" >
                <h5 class="inputcontainer__h5  " id="inputcontainer__h5-2 ">Choose a custom name</h5>
               
                <InputComponent2
                v-model="inputData3"
                id="input__3"
                class="enter"
                @input3="Func3" ref="nameOfzip" @inputHandeler="handleInput3"/><!-- @input3="active=false"-->
                  </div>

              <!--section3-->

            </div>





         
       
        </b-container>

        
      
            <div class="drop-zone " id="dropZone " >
              <input 
                @change="uploadFile($event)"
                type="file"
                id="fileInput"
                accept=".jpeg, .jpg, .png, .pdf, .zip,.rar"
                style="
                  opacity: 0;
                  width: 400rem;
                  height: 100%;
                  cursor: pointer;
                  z-index: 1000;
                "
                  multiple  ref="fileInputRef"   />


              
<!--drop--> 



<div class="drop-zone__containerP">

        <img
          src="../assets/add-file.png"
          alt="addfile image"
          class="addFile__img"   />
     
                  <div class="drop-zone__container">
                                  <p class="drop-zone__p">Drag and drop or browse to</p>
                                  <span class="drop-zone__span"> choose file</span>
                    </div>


                  <div class="">
                    <p class="limit__p">File Upload Limitations</p>
                    <p class="limit__p">format: jpeg, png, pdf, zip</p>
                    <p class="limit__p">size: 1GB</p>
                  </div>

</div>

    <!--drop--> 

</div>



       
            
  
  

            
           
              
  
              <b-modal
                id="my-modal"
                hide-footer
                class="custom-modal"
                  @hide="closeModalAndCollapse">
              
  
                <div class="d-flex flex-column align-items-center">
                  <div class="d-flex align-items-center">
                    <div class="iconCheck__wrapper">
                      
                     <SvgComponent/>
                    </div>
                    <p class="ml-2" id="modal__p">Uploaded Successfully</p>
                  </div>
                  <br />
                  <br />
  
                  <div class="d-flex align-items-center my-3">
                    <div class="linkicon__wrapper">
                      <b-icon-link class="linkicon" />
                    </div>
                    <input
                      ref="downloadLinkInput"
                      class="form-control mx-2 modal__input"
                      placeholder="Enter link..."
                      :value="downloadLink"
                    />
                    <b-button
                      @click="copyLink"
                      variant="primary"
                      class="copy__modal"
                      >Copy link</b-button
                    >
                  </div>
  
                  <div class="social-icons">
                    <b-icon-facebook class="social-icon" />
                    <b-icon-skype class="social-icon" />
                    <b-icon-twitter class="social-icon" />
                    <b-icon-whatsapp class="social-icon" />
                  </div>
                </div>
              </b-modal>
            
  




            <!-- end of  modal -->
            
          
        <!--end of input zone------>
              <!-- hamin ja dynamic kon-->
              
              




       <div   v-for="item in collapsed" :key="item" style="background-color:white;"  class="render">
             
              <div>
      
                      <transition name="fade ">
                        <div  class="collapse-content d-flex justify-content-start " :class="{ show: dataList }" >
                          
                          <div class="progress-bar-container">
                            
                            <div class="progress-bar" :style="{ width: progress + '%' }"></div>
                          </div>
                          <img src="../assets/file.svg" alt="" srcset="" class="image" />
                          <img src="../assets/check.svg" alt="" srcset="" class="greencheck">
                          <img src="../assets/bin.svg" alt="" class="bin"  id="tooltip-target-1" @click="view">
                          <p class="progress__p d-flex">100% Uploaded</p>

                   <b-tooltip target="tooltip-target-1" triggers="click" variant='light' ref="tooltip" v-if="showTooltip" >
                  <p>Are you sure to delete this file?</p>
                  <b-button variant='danger' style="background-color: #dc3545; color: white;" @click="removeBin($event)">Delete</b-button> 
                  <b-button variant='light' @click="cancel" >Cancel</b-button> 
                </b-tooltip>
                          <!-- v-b-tooltip.hover.v-light title="Danger variant" -->

                        </div>
                      
                      </transition>
      
        </div>
                <b-progress :value="progress" :max="100"  v-if="!item"  class="bar" variant="success">
                
                </b-progress>
  
  
  </div>


              
              
              
              
              <!-- hamin ja dynamic kon-->
        <section class="btn-check-wrapper">

            <b-button   :disabled="active"      v-b-modal.my-modal @click="fetchDownloadLink"  class="btn"  :style="{ backgroundColor: buttonBackgroundColor}"> Get the link</b-button>
            <CheckBox   v-model="downloadAsZip" class="fixed-checkbox"  @enable="downloadAsZip=!downloadAsZip"/>

        </section>
        

        
      </div>
      
    
  
  </div>
</template>

<script>
const token = "c14d0378-02b0-4ab8-8e5d-cc785fe636ce";
const baseUrl = "https://192.168.2.51/api/v1/files/temp?guest_token=";


import axios from "axios";
import { BContainer, BFormFile, BImg } from "bootstrap-vue";
import InputComponent2 from "./InputComponent2.vue";
import InputComponent1 from "./InputComponent1.vue";
import InputComponent from "./InputComponent.vue";
import SvgComponent from './SvgComponent.vue'
import CheckBox from "./CheckBox.vue";



export default {
  name: "Bod",

  components: {

    CheckBox,
    InputComponent,
    InputComponent1,
    InputComponent2,
    BContainer,
    BFormFile,
    BImg,
    SvgComponent,
    
    

  },
  props: {},
  data() {
    return {

      dataList:false,
      uploadedFileCount: 0,
      collapsed: [],
      progress: 0, 
      downloadLink: "",
      guestToken: "",
      inputData1: "",
      inputData2: "",
      inputData3: "",
      downloadLinkResponse: "",
      downloadAsZip:false, // zip or non zip
      isFileUploaded: false,
      selectedFileNames: [],
      active:true,
      buttonBackgroundColor: '#00baba',
      disabled:true,
      pram1:'',
      pram2:'',
      pram3:'',
      showTooltip: true,
      ar1:false,
      ar2:false,
      ar3:false,
      alterefile:[],
      mainfile:[],
      
      
    };
  },

  async created() {
    try {
      const response = await axios.post(
        "https://192.168.2.51/api/v1/users/guest"
      );
      
      if (response.data) {
        this.guestToken = response.data.guest_token;

        
      }
    } catch (error) {
      console.error("Error getting guest token:", error);
    }
  },


  mounted() {
    
    this.simulateProgress();
  },

  methods: {




    handleSelectChangeInParent(value){

      this.inputData1 = value;
    },
    handleInput1(value) {
       this.inputData1 = value;
    },
   
    handleInput2(value) {
      this.inputData2 = value;
    },

    handleInput3(value) {
      this.inputData3 = value;
    },

    view(){

      this.showTooltip=true;
    },

    cancel(){

      this.showTooltip = !this.showTooltip;
    },


 inputComp(val1){

      this.pram1=val1;
      if(this.pram1&&this.pram2&&this.pram3){

        this.active=false;

}

    },
    inputComp1(val2){

      this.pram2=val2
    
      if(this.pram1&&this.pram2&&this.pram3){

        this.active=false;

         }

    },
    inputComp2(val3){

      this.pram3=val3;
      
      if(this.pram1&&this.pram2&&this.pram3){

        this.active=false;

}

    },

    parametr(){

      if(this.pram1&&this.pram2&&this.pram3){

        this.active=false;

      }

    },











removeBin(){

  const fileInput = this.$refs.fileInputRef;

   

  setTimeout(this.collapsed.pop(),5000);//5000

  this.showTooltip = !this.showTooltip;


  
  
if (this.alterefile instanceof FileList) {
    // Convert FileList to an array
    const fileListArray = Array.from(this.alterefile);

    // Remove the last file from the array
    fileListArray.pop();

    // Create a new FileList with the modified array
    const newFileList = new DataTransfer();
    fileListArray.forEach(file => newFileList.items.add(file));

    // Set this.alterefile to the new FileList
    this.$set(this, 'alterefile', newFileList.files);
  }

  fileInput.value = '';
  
console.log(this.alterefile)


  
  

},








eventInput(option){


  this.option='';


},

handleDrop(event) {
      event.preventDefault();

      const files = event.dataTransfer.files;
      if (files.length > 0) {
        
        this.uploadFile({ target: { files } });
      }
    },

    openFileInput() {
      
      const fileInput = this.$refs.fileInput; 

      if (fileInput) {

        fileInput.click();
      }
    },



closeModalAndCollapse(){

  for(let i = 0; i < this.collapsed.length; i++){

    this.collapsed[i] = true
  }
  

  this.fetchNewGuestToken();
  this.eventInput();
  window.location.reload();
 
  

},

Func1(){

this.ar1=true;

if(this.ar2&&this.ar3) this.active=false;

},
Func2(){
this.ar2=true;

if(this.ar1&&this.ar3) this.active=false;
},
Func3(){

this.ar3=true;

if(this.ar1&&this.ar2) this.active=false;

},


    simulateProgress() {
      
      let currentProgress = 0;

      const interval = setInterval(() => {

        currentProgress += 1;

        this.progress = currentProgress;

        if (currentProgress === 100) {

          clearInterval(interval); 
        }
      }, 60); 
    },



    async uploadFile(event) {

      
  const files = event.target.files;


  this.alterefile=files;
  
  

  

  if (files.length === 0) {

    return; 
  }

  for (let file of files) {

    

    const formData = new FormData();

    formData.append("file", file);

    

    try {
      const response = await this.uploadFileToServer(formData);

      if (response.data && response.data.downloadLink) {

        

        this.downloadLink = response.data.downloadLink;

        this.isFileUploaded = true;
        this.active=true;
        
        
      }
      this.uploadedFileCount++;

      this.collapsed.push(this.uploadedFileCount);

      for(let i = 0; i < this.collapsed.length; i++){

       if(this.collapsed[i] == this.uploadedFileCount){

        this.collapsed[i] = false;
       }

       
       }
      
     


    } catch (error) {
      console.error("Error uploading file:", error);
    }
  }
},


    



    async uploadFileToServer(formData) {
      
      try {
        const response = await axios.post(
          "https://192.168.2.51/api/v1/files/temp?guest_token=" +
            this.guestToken,
          formData,
          {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          }
        );

        return response;
      } catch (error) {
        throw error;
      }
    },

    
    
    async fetchDownloadLink() {
      try {
        const formData = new FormData();
        formData.append("expires_at", this.pram1 );
        formData.append("max_download_count", this.inputData2);
        formData.append("save_as_name", this.inputData3);
        formData.append("timezone", "America/Los_Angeles");

        

        if (this.downloadAsZip) {

          formData.append("zip_files", 1); 

        } 
        
        else {

          formData.append("zip_files", 0); 
        }
        const response = await axios.post(
          "https://192.168.2.51/api/v1/files?guest_token=" + this.guestToken,
          formData,
          {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          }
        );

        if (response.data && response.data.download_link) {
          if (this.downloadAsZip && response.data.download_link) {
            this.downloadLink = `${response.data.download_link}`; 
          } else {
            this.downloadLink = response.data.download_link; 
          }

          this.downloadLinkResponse = JSON.stringify(response.data, null, 2);
          
        }
      } catch (error) {
        console.error("Error fetching download link:", error);
        
      }
    },

    

    copyLink() {
      const inputElement = this.$refs.downloadLinkInput; 
      inputElement.select(); 
      document.execCommand("copy"); 
    },

    
    async fetchNewGuestToken() {
      try {
        const response = await axios.post(
          "https://192.168.2.51/api/v1/users/guest"
        );
        console.log("New Guest Token Response:", response);
        if (response.data) {
          this.guestToken = response.data.guest_token;
          
        }
      } catch (error) {
        console.error("Error getting new guest token:", error);
      }
    },
  },

  

  watch: {
  isInputsFilled(newValue) {
    this.buttonBackgroundColor = newValue ? '#00baba' : '#yourDefaultColor';
  },
},


  computed: {
    isFormFilled() {
      return (
        this.inputData1 && 
        this.inputData2 && 
        this.inputData3 
      );

      
    },

    isInputsFilled() {
    return this.inputData1 && this.inputData2 && this.inputData3;
  },

  },
};
</script>


<style scoped lang="scss">
/////////////////// start scss
$oneHalf: 1.5rem;
$inContainFontSize: 0.85rem;
$babaColor: #00baba;
$whiteColor: #ffffff;
$inputbgColor: #f5f1f1;
$btnMixColor: #828282;
$DropZonePbgColor: #4a4a4a;
$enterSolidColor: #808080;
$aLinkColor: #42b983;
$dashZoneColor: #019797;
$blackColor: #000000;
$lightGreen:#3fd87a;
$shineGreen:#47cc1e;
$green:#008000;
$diactivecolor:#d4d4d4;
@mixin positionMix($top, $right, $bottom, $left) {
  position: absolute;
  top: $top;
  right: $right;
  bottom: $bottom;
  left: $left;
}
@mixin felJ() {
  display: flex;
  justify-content: center;
}

@mixin bttnMix() {
  @include positionMix(89%, 0%, 0%, 76.5%);
  border: 0;
  width: 9.7%;
  border-radius: 0.5rem;
  height: 40px;
  box-shadow: 0 2px 0 rgba(0, 0, 0, 0.015);
  background-color: $diactivecolor;
  color: $btnMixColor;
  font-size: 14px;
  font-weight: 400;
  .bt {
    color: $DropZonePbgColor;
    background-color: $lightGreen;
  }
}

@mixin zindexPointer($index) {
  z-index: $index;
  cursor: pointer;
}

@mixin mrg($top,$right,$bottom,$left){

margin-top: $top;
margin-right: $right;
margin-bottom: $bottom;
margin-left: $left;

}

@mixin flexClumn(){

  display: flex;
flex-direction: column;
}


* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}



.disactiveClass{

  background-color: $diactivecolor;
  color: $DropZonePbgColor;
}


.activeClass{

  background-color: $babaColor;
  color: $whiteColor;
}

#__BVID__7{

background:$inputbgColor ;


}


.scroll-y {
  overflow-y: scroll;
  max-height: 300px; /* Adjust the max height as needed */
}



*[data-v-01caf037]{

  background-color: $whiteColor;
}

.render{

 @include flexClumn();
justify-content: space-between;
margin-bottom: 1%;

}
.btn{
  margin-right: 10%;
  background-color: $whiteColor;
  
  
}
.btn-check-wrapper{

  display: flex;
  flex-direction: row-reverse;
  justify-content: space-between;
  align-items: center;
  border: none;
  width: 100%;
  margin-top: 0;
  background-color: $whiteColor;
  border-bottom-left-radius: 1.5rem;
  border-bottom-right-radius: 1.5rem;
  padding:1% ;
}
.one-input-wrapper{

  @include flexClumn();
flex-wrap: wrap;


}

.ex-date{


  margin-left: -10%;
  display: flex;
  flex-wrap: wrap;
  
  width: 50%;
}

.drop-zone__container{

  display: flex;
  justify-content:flex-start;
  
  width: 60%;

}

.drop-zone__containerP{


  @include flexClumn();
justify-content:center;
align-items: center;
width: 100%;
height: 100%;

position: absolute;


}

#inpu3{


width: 26%;
margin-right: 3%;
align-self:center;

}
.wrapper{

@include felJ();
width: 90%;
margin-top: 5%;

flex-wrap: wrap;
gap: 0%;




}

.show {
  opacity: 0; 
  animation: fadeIn 0.5s ease-in forwards;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}



.input-h-p{

  @include flexClumn();
flex-wrap: wrap;
width:35.5%;

align-items :center;



}
.wrap{

overflow-y: scroll;
max-height: 7rem;

transform: translateY(-2rem);

}

.scrollable-container {
  scrollbar-width: thin; 
  scrollbar-color: transparent transparent; 
}

.scrollable-container::-webkit-scrollbar {
  width: 12px; 
}

.scrollable-container::-webkit-scrollbar-thumb {
  background-color: transparent; 
  width: 0; 
}


.pro__bar-2{

 transform: translateY(-0.9rem);
}
.progress__p{

  color: $babaColor;
  font-size:$inContainFontSize;
}
.bin{
 
  @include mrg(1rem, 0, 0, 0.2rem);
  cursor: pointer;
}

.greencheck{

  @include mrg(1rem, 0,0 , 75%)
}

.custom-progress {
  background-color: $babaColor; 
}

.bar{

  @include mrg(-1.5rem,0,0,17.1rem);
  width: 40%;
  height: 0.4rem;

}


.collapse-content {
  
  border: 1px solid #ddd;
  padding:9px;
  width: 57%; 
   overflow: hidden;
  transition: max-height 0.5s ease-out;
  margin-left: 14rem;
  padding-right: 1rem;
  height: 3.5rem;
  
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s, max-height 0.5s ease-out;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
  max-height: 0;
}

.fixed-checkbox {
  
    margin-left: 9%;
    z-index: 999;
   
}
.custom-collapse {
  width: 100%; 
  height: 20%; 
  transform: translateY(-3rem);
   border: 2px solid $shineGreen ;
  
}

.progress-bar-container {
  display: flex;
  align-items: center;
}


.progress-bar {
  height: 10px;
  background-color: $green;
  transition: width 0.3s;
}

.copy__modal {
  @include felJ();
  background-color: $babaColor;
  color: $whiteColor;
  width: 108px;
  height: 37px;
  align-items: center;
  text-align: center;
}

.colaps {
  @include positionMix(85%, 10%, 0%, 0);
  @include zindexPointer(1000);
}


.limit__p {
  color: $btnMixColor !important;
  font-size: 14px;
 
  
}

.addFile__img {
  
  display: inline;
  
}


.drop-zone__span {
 
  @include zindexPointer(500);
  color: $babaColor;
  font-size: $oneHalf;
  text-decoration: underline;
  width: 40%;
  display: flex;
  


}
.drop-zone__p {
  
  @include zindexPointer(500);
  color: $blackColor;
  font-size: 1.4rem;
  width: 75%;
  font-weight: 400;
  display: flex;
 
 justify-content: center;
 margin-left: 3%;
 

  
}

.drop-zone {
  @include felJ();
  border: 2px dashed $dashZoneColor;
  background-color: $whiteColor;
  width:80%;
  border-radius: 0.6rem;
  height: 520px;
  align-items: center;
  cursor: pointer;
  margin: 2rem auto;
  position: relative;
}
.drop-zone:hover {
  border: 2px dashed $babaColor;
}
.drop-zone p {
  color: $DropZonePbgColor;
  text-align: center;
  font-family: Arial, sans-serif;
}


#input__1 {
  background-color: $inputbgColor;
 
  margin-left: 20%;
  width:80%;
}


#input__2 {
  background-color: $inputbgColor;
  align-self:flex-end;
  width:80%;
  margin-top: 1%;
}


#input__3 {
  background-color: $inputbgColor;
  width:100%;
  margin-left: 15%;
  margin-top: 3%;
}
.enter {
  
  margin-right: 5%;
  width: 70%;
  height: 38px;
  border-radius: 0.5rem;
}
.enter:hover {
  border: 1px solid $babaColor;
}


.h5-p__wrapper {
  
  @include flexClumn()
}
.inputcontainer__h5 {
  font-weight: bold;
  margin-bottom: 4%;
 
 
}



.inputcontainer {
  z-index: 200;
  margin-top: 6%;
}
.white-block {
  @include positionMix(50%, 0, 0, 50%);
  background-color: $whiteColor;
  border-radius: $oneHalf;
  width: 60%;
  margin: 0 auto;
  transform: translate(-50%, -50%);
 min-height: 85%;
 
 
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: $aLinkColor;
}

.bttn {
  @include bttnMix();
}
// ////////////////////////modal style start
.iconCheck__wrapper {
  width: 10%;
  transform: rotate(-50deg);
  position: relative;
}
.linkicon__wrapper {
  width: 10%;
  transform: rotate(130deg);
}
.iconCheck,
.linkicon,
.social-icon {
  font-size: 24px;
}

.social-icons {
  @include felJ();
  gap: 10px;
  margin-top: 20px;
}

.modal-header .close {
  border: none;
}

.green-check-icon {
  color: $babaColor;
  border: 2px solid $babaColor;
  font-size: 24px;
  border-radius: 50%;
  padding: 5px;
  margin-right: 10px;
}

#modal__p {
  position: absolute;
  font-size: 1.14rem;
  font-weight: 700;
  margin-bottom: 25px;
  text-align: center;
  transform: translateY(2rem) translateX(-5.5rem);
}

.modal__input {
  width: 250px;
}



.image {
  max-width: 100px; 
  margin-left: 10px; 
}

.progress-bar-container {
  height: 10px; 
  background-color: #ddd; 
  border-radius: 5px; 
  overflow: hidden; 
}

.progress-bar {
  height: 100%; 
  width: 0; 
  transition: width 0.5s ease; 
  background-color: $green; 
  border-radius: 5px; 
}


@media only screen and (max-width: 576px) {

.white-block{


  
 width: 60%;
}

.wrapper{


  // display: flex;
  // flex-direction: column;
  @include flexClumn()
}

.drop-zone{

  height: 350px;
}

.input-h-p{
  width: 100%;
  margin-left: -15%;
  margin-top: 4%;
}

#input__1{
  width: 100%;
  margin-left: 23%;
}
.ex-date{
  margin-left: -30%;
}

#input__2{
  width: 100%;
  margin-left: 23%;
}

.inputcontainer__h5{
  margin-left: -30%;
}
#inpu3{
  width: 100%;
  margin-right: 0;
}



#inputcontainer__h5-2{

  margin-left: -38%;


}


}


@media only screen and (max-width: 990px) {

.white-block{

overflow-x: hidden;
  
 width: 95%;
}

.wrapper{


  // display: flex;
  // flex-direction: column;
  @include flexClumn()
}

.drop-zone{

  height: 350px;
}

.input-h-p{
  width: 100%;
  margin-left: -15%;
  margin-top: 4%;
}

#input__1{
  width: 100%;
  margin-left: 23%;
}
.ex-date{
  margin-left: -30%;
}

#input__2{
  width: 100%;
  margin-left: 23%;
}

.inputcontainer__h5{
  margin-left: -30%;
}
#inpu3{
  width: 100%;
  margin-right: 0;
}

#inputcontainer__h5-2{

margin-left: -38%;


}



.collapse-content{
  width: 85%;
  margin-left: 5rem;
}
.bar{
  margin-left: 20%;
  width: 50%;
}
.greencheck{
  margin-left: 71%;
}
.drop-zone{
  width: 68%;
 margin-left: 18%;
}
.fixed-checkbox{
  margin-top: 5%;
}

.progress__p{
  margin-top: 2%;
}

}

@media only screen and (max-width: 808px){

  .progress__p{
  margin-top: -0.5%;
}

.bar{
  margin-left: 30%;
  width: 50%;
}


}

@media only screen and (width: 1525px){

  .collapse-content{
  width: 70%;
  margin-left: 11rem;
}


}
@media only screen and (width: 1533px){

  .collapse-content{
  width: 65%;
  margin-left: 11rem;
}


}
@media  (min-width: 990px)and (max-width:1525px){

  .collapse-content{
  
    width: 75%;
    margin-left: 15%;
}

.progress-bar{
 
  width: 50%;
}


}
@media  (min-width: 990px)and  (max-width:1328px){

 

.bar{
 
  width: 50%;
  margin-left: 24%;
}


}
@media  (min-width: 1356px)and  (max-width:1639px){

  .broke{

    width: 80%;
    

  }

  .broke-1{
    width: 40%;
  
  }


}
@media  (min-width: 1338px)and  (max-width:1355px){

  .broke{

    width: 80%;
    

  }

  


}
@media  (min-width: 613px)and  (max-width:808px){

  
.bar{

  margin-left: 25%;
    width: 50%;
}
  


}

</style>
