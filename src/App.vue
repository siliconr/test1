//template part
<template>
   <article>
     <div class="container" :class="{'sign-up-active' : signUp}">
        <div class="overlay-container">
          <div class="overlay">
            <div class="overlay-left">
              <h2>Welcome Back</h2>
              <p>Please Login With Your Personal Information</p>
              <button class="invert" id="signIn"  @click="signUp =! signUp">Sign In</button>

            </div>
            <div class="overlay-right">
              <h2>Hello, User!</h2>
              <p>Please Enter Your Personal Details</p>
              <button class="invert" id='signUp'   @click="signUp =! signUp">Sign Up</button>


            </div>
          </div>
        </div>

        
        <form class="sign-up" action="#">
           <h2>Create Login</h2>
           <div>Use Your Email For Registration</div>
           <input type="text" placeholder="Name" >
           <input type="email" placeholder="Email">
           <input :type="show === true ? 'text' :'password'" id='password' v-model='password' placeholder="password">
           <div class ='strength' :class="'level_' + strengthLevel"></div>
           <i class="fas fa-eye show-icon" v-if="show" @click="show = !show"></i>
           <i class="fas fa-eye-slash hide-icon" v-else @click="show = !show"></i>
           <i class="fas fa-frown level-icon" v-if="strengthLevel === 1"></i>
           <i class="fas fas-meh level-icon" v-if="strengthLevel ===2"></i>
           <i class="fas fa-smile level-icon" v-if="strengthLevel ===3"></i>
           <i class="fas fa-grin-stars level-icon" v-if="strengthLevel ===4"></i>
           <button>Sign Up</button>
        </form>


        <form class="sign-in" action="#">
           <h2>Sign In</h2>
           <div>Use Your Account</div>
           <input type="email" placeholder="Email">
           <input :type="show === true ? 'text' :'password'" id='password' v-model='password' placeholder="password">
           <div class ='strength' :class="'level_' + strengthLevel"></div>
           <i class="fas fa-eye show-icon" v-if="show" @click="show = !show"></i>
           <i class="fas fa-eye-slash hide-icon" v-else @click="show = !show"></i>
           <i class="fas fa-frown level-icon" v-if="strengthLevel === 1"></i>
           <i class="fas fa-meh level-icon" v-if="strengthLevel ===2"></i>
           <i class="fas fa-smile level-icon" v-if="strengthLevel ===3"></i>
           <i class="fas fa-grin-stars level-icon" v-if="strengthLevel ===4"></i>
           <a href="#">Forgot Your Password?</a>
           <button>Sign Up</button>
        </form>

     </div>
   </article>

</template>



//script part
<script>
export default {
 data:() =>{
   return{
     signUp:false,
     password: '',
     show:true
   }
 },

  computed:{
   scorePassword(){
     let score =0;
     if(this.password=== '') return score;

     let letters ={};
     for(let i=0; i< this.password.length; i++){
       letters[this.password[i]] = (letters[this.password[i]] || 0) +1;
       score += 5.0 / letters[this.password[i]];
     }

     let variations = {

       digits : /\d/.test(this.password),
       lower :/[a-z]/.test(this.password),
       upper :/[A-Z]/.test(this.password),
       special:/\w/.test(this.password)
     };

     let variationsCount = 0;
     for(let check in variations){
       variationsCount += (variations[check] === true) ? 1 : 0;
     }

     score += (variationsCount - 1) * 10;
     return parseInt(score);
    },
     
    strengthLevel() {
      let pass = this.scorePassword;
      if(pass === 0) return 0;
      if(pass < 25) return 1;
      if(pass <= 30) return 2;
      if(pass <= 40) return 3; 
      if(pass >= 40) return 4;
      else
      return null;
    } 

  }
  
}
</script>


//style part
<style lang="scss" scoped>
  @import url("https://use.fontawesome.com/releases/v5.7.2/css/all.css");

  .container {

    position: relative;
    width: auto;
    height: 600px;
    border-radius: 10px;
    overflow:hidden;
    box-shadow: 0 15px 30px rgba(0, 0, 0, .2),
                0 10px 10px rgba(0, 0, 0, .2);
    background: linear-gradient(to bottom , white , white);            


    .overlay-container {
      position: absolute;
      top: 0;
      left: 50%;
      width: 50%;
      height: 100%;
      overflow: hidden;
      transition:transform .5s ease-in-out;
      z-index: 100;
    }

    

    .overlay {
      position: relative;
      left: -100%;
      height: 100%;
      width: 200%;
      background: linear-gradient(to bottom right,blue,green);
      color: seashell;
      transform: translateX(0);
      transition:transform .5s ease-in-out;
    }

    @mixin overlays($property) {
      position: absolute;
      top: 0;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: column;
      padding: 70px 40px;
      width: calc(50% - 80px);
      height: calc(100% - 140px);
      text-align: center;
      transform: translateX($property);
      transition: transform .5s ease-in-out;

    }

    .overlay-left{
      @include overlays(-20%);

    }


    .overlay-right{
      @include overlays(0);
       right: 0;
    }
         
  }

  h2{
   font-family: sans-serif;
   margin: 0;
   font-size: 3rem;
  }

  p{
   font-family: sans-serif;
   margin: 20px 0 30px;
   font-size: 1.5rem;
  }

  a{
   font-size: 20px;
   color: darkblue;
   text-decoration: none;
   margin:  15px 0;
  }

  button{
   border-radius: 20px;
   border: 1px solid rgb(26, 26, 134);
   background-color: rgb(0, 172, 0);
   color: white;
   font-size: 1rem;
   font-weight: bold;
   padding: 10px 40px;
   letter-spacing: 1px;
   text-transform: uppercase;
   transition: transform .1s ease-in;

   &:active{
     transform: scale(.9);
   }

   &:focus{
     outline: none;
   }
  }

  button.invert{
    background-color: transparent;
    border-color: white;
  }


form{

    position: absolute;
    top:0;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: column;
    padding: 90px 60px;
    width: calc(50% - 120px);
    height: calc(100% - 180px);
    text-align: center;
    background:linear-gradient(to bottom,rgb(72, 72, 255),rgb(75, 241, 111));
    transition:all .5s ease-in-out;
    

  div{
    font-size: 1rem;
  }

  input{
    background-color: white;
    border:none;
    padding:8px 15px;
    margin: 6px 0;
    width: calc(100% - 30px);
    border-radius: 15px;
    border-bottom:  1px solid  white;
    box-shadow: inset 0 1px 2px grey, 0 -1px 1px white , 0 1px 0 white;
    overflow: hidden;

    &:focus{
      outline: none;
      background-color: white;
     }
    }
    
} 

  
  .strength{

    position: absolute;
    bottom: -10px;
    left:0;
    right: 0;
    display: block;
    width: 25%;
    height: 3%;
    background-color: rgb(5, 196, 5);
    border-radius: 40px;
    overflow: hidden;
    z-index: 9;
    transition: all .5s linear;
  }


  @mixin level($position, $width, $color){

    bottom: $position;
    width: $width;
    background-color: $color;
  }


  .level_0{
    @include level(0, 0, 0 )

  }

  .level_1{
    @include level(-10px, 25% , rgb(248, 4, 4) )
  }

  .level_2{
    @include level(-10px, 50% , rgb(255, 94, 30) )
  }

  .level_3{
    @include level(-10px, 75% , orange )
  }

  .level_4{
    @include level(-10px, 100% ,rgb(5, 196, 5) )
  }


  @mixin showpass($property){
    left: $property;
    z-index: 11;
    cursor: pointer;
  }

  .show-icon{
    @include showpass(20px);
  }
  .hide-icon{
    @include showpass(20px)
  }

  .level-icon{
    position: absolute;
    right: center;
    top: 25px;
    z-index: 11;

  }




  .sign-in{
    left:0;
    z-index: 2;
  }


  .sign-up{
    left:0;
    z-index: 1;
    opacity: 0;
  }


  .sign-up-active{

    .sign-in{
      transform: translateX(100%);
    }

    .sign-up{
      transform: translateX(100%);
      opacity :1;
      z-index: 5;
      animation: show .5s;
    }
    
    .overlay-container{
      transform: translateX(-100%);
    }
    

    .overlay{
       transform: translateX(50%);

    }

    .overlay-left{
       transform: translateX(0);
    }
    
    .overlay-right{
       transform: translateX(20%);
    }

  }


  @keyframes show {
    0%{
      opacity: 0;
      z-index: 1;
    }

    49%{ 
      opacity: 1;
      z-index: 1;
    }

    50%{
      opacity: 1;
      z-index: 10;
    }
    
  }
</style>
