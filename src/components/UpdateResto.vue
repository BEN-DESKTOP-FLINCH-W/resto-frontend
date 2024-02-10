<template>
    <HeaderComponent/>
    <h1>Welcome to add restaurant page!</h1>
    <div class="restaurant">
        <input type="text" name="name" v-model="restaurant.name" placeholder="Restaurant Name"/>
        <input type="text" name="contact" v-model="restaurant.contact" placeholder="Contacts"/>
        <input type="text" name="address" v-model="restaurant.address" placeholder="Address"/>
        <button v-on:click="updateresto">Update</button>

    </div>
</template>
<script>
import HeaderComponent from './HeaderComponent.vue';
import axios from 'axios'
export default{
    name:'UpdateResto',
    components:{
        HeaderComponent,

    },
    data(){
        return{
            restaurant:{
                name:'',
                contact:'',
                address:''
            }
        }

    },
    methods:{
        async updateresto(){
            let result= await axios.put("http://127.0.0.1:8000/restaurants/"+this.$route.params.id,{
                name:this.restaurant.name,
                contact:this.restaurant.contact,
                address:this.restaurant.address
            });
            if(result.status==200){
                this.$router.push({name:'HomePage'})
            }
            else{
                alert("Not Successful")
            }
        }

    },
    async mounted(){
        let user=localStorage.getItem("user-info");
        if(!user){
            this.$router.push({name:'SignUp'})
        }
        const result= await axios.get('http://127.0.0.1:8000/restaurants/'+this.$route.params.id)
        console.log(result)
        this.restaurant=result.data
    }
}
</script>