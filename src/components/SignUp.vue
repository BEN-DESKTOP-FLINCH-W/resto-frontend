<template>
     <img class="logo" alt="Topend" src="../assets/front.jpg">
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Your Name"/>
        <input type="text" v-model="email" placeholder="Email"/>
        <input type="text" v-model="password" placeholder="Password"/>
        <button v-on:click="signUp">Sign Up</button>
        <p>
            <router-link to="/login">Go to Login</router-link>
        </p>

    </div>
</template>
<script>
import axios from 'axios'
export default{
    name: 'SignUp',
    data()
    {
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods:
    {
        async signUp()
        {
            let result= await axios.post("http://127.0.0.1:8000/resto/",{
                name:this.name,
                email:this.email,
                password:this.password
            });
            console.warn(result);
            if(result.status==201){
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:'HomePage'})
            }
        }
    },
    mounted(){
        let user=localStorage.getItem("user-info");
        if(user){
            this.$router.push({name:'HomePage'})
        }
    }
}

</script>
<style>

</style>