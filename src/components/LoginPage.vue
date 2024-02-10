<template>
    <img class="logo" alt="Topend" src="../assets/front.jpg">
    <h1>Login</h1>
    <div class="login">
        <input type="text" v-model="email" placeholder="Email"/>
        <input type="text" v-model="password" placeholder="Password"/>
        <button v-on:click="login">Login</button>
        <p>
            <router-link to="/sign-up">Go to Sign Up</router-link>
        </p>

    </div>
</template>
<script>
import axios from 'axios'
export default{
    name:'LoginPage',
    data()
    {
        return{
            email:'',
            password:''
        }
    },
    methods:{
        async login(){
            let result= await axios.get(
                `http://127.0.0.1:8000/resto/${this.email}/${this.password}`
            )
            console.warn(result)
            if(result.status==200){
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:'HomePage'})
            }
            else{
                alert("User Does not exist")
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
