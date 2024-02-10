<template>
    <HeaderComponent/>
    <h1>Welcome to add restaurant page!</h1>
    <div class="restaurant">
        <input type="text" v-model="name" placeholder="Restaurant Name"/>
        <input type="text" v-model="contact" placeholder="Contacts"/>
        <input type="text" v-model="address" placeholder="Address"/>
        <button v-on:click="addresto">Submit</button>

    </div>
</template>
<script>
import HeaderComponent from './HeaderComponent.vue';
import axios from 'axios'
export default{
    name:'AddResto',
    components:{
        HeaderComponent,

    },
    data(){
        return{
            name:'',
            contact:'',
            address:'',
        }

    },
    methods:{
        async addresto(){
            let result= await axios.post("http://127.0.0.1:8000/restaurants/",{
                name:this.name,
                contact:this.contact,
                address:this.address
            });
            console.warn(result)
            if(result.status==201){
                this.$router.push({name:'HomePage'})
            }
        }

    },
    mounted(){
        let user=localStorage.getItem("user-info");
        if(!user){
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>