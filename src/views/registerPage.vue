<template>
  <div id="registerPage">
      <div class="container" id="register-box" >
        <div class="row align-items-center justify-content-center">
            <!-- <div class="col-4"></div> -->
            <div class="col-4 border border-primary rounded m-3 p-3">
                <div class="form-horizontal ">
                    <h1 class="text-center">First time?</h1>
                    <p class="lead text-muted text-center">Step right up and register here!</p>
                    <hr/>
                    <form class="justify-content-center" @submit.prevent="register()">
                        <label class="control-label" for="registerEmail">Email:</label>
                        <input type="email" class="form-control" id="registerEmail" v-model="newUser.registerEmail">
                        <label class="control-label" for="registerOrganization">Organization:</label>
                        <input type="text" class="form-control" id="registerOrganization" v-model="newUser.registerOrganization">
                        <label class="control-label" for="registerPassword">Password:</label>
                        <input type="password" class="form-control" id="registerPassword" v-model="newUser.registerPassword"><br>
                        <label class="control-label" for="registerPassword_verify">Confirm password:</label>
                        <input type="password" class="form-control" id="registerPassword_verify" v-model="newUser.registerConfirmPassword"><br>
                        <button type="submit" class="btn btn-success">Register</button>
                        <button type="button" class="btn btn-danger" @click="changePage('loginPage')">Cancel</button>
                    </form>
                </div>
            </div>
            <!-- <div class="col-4"></div> -->
        </div>
    </div>
  </div>
  
</template>

<script>
import axios from 'axios'

export default {
    name: "registerPage",
    data (){
        return {
            message:"Hello from registerPage!",
            newUser:{
                registerEmail:"",
                registerPassword:"",
                registerOrganization:"",
                registerConfirmPassword:""
            }
        }
    },
    methods:{
        changePage(page){
            this.$emit( 'changePage', page )
        },
        registerSuccessful(){
            this.$emit('registerSuccessful')
        },
        register(){
            if(this.newUser.registerPassword == this.newUser.registerConfirmPassword){
                console.log("Password match")
                let payload = {
                    email: this.newUser.registerEmail,
                    password: this.newUser.registerPassword,
                    organization: this.newUser.registerOrganization
                }
                axios({
                    method: 'POST',
                    url:'https://fierce-savannah-25696.herokuapp.com/register',
                    data:{
                        email: payload.email,
                        password: payload.password,
                        organization: payload.organization
                    }
                })
                    .then(result =>{
                    console.log(result)
                    this.registerSuccessful()
                    this.changePage('loginPage')
                    })
                    .catch(error =>{
                    console.log(error)
                    })
            } else {
                console.log("Re-typed password doesn't match ")
            }
        }
    }
}
</script>

<style>

</style>