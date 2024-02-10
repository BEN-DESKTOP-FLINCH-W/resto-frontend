<template>
    <HeaderComponent/>
    <h1>Welcome {{ name }}</h1>
    <table border="1">
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Contacts</th>
            <th>Address</th>
        </tr>
        <tr v-for="item in restaurants" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td>
                <router-link :to="'update-restaurant/'+item.id">Edit</router-link>
                <button v-on:click="deleteresto(item.id)">Delete</button>
            </td>

        </tr>
    </table>
</template>
<script>
import HeaderComponent from './HeaderComponent.vue';
import axios from 'axios';
export default{
    name:'HomePage',
    components:{
        HeaderComponent,
    },
    data(){
        return{
            name:'',
            restaurants:[],
        }

    },
    methods:{
        async deleteresto(id){
            let result= await axios.delete("http://127.0.0.1:8000/restaurants/"+id)
            console.warn(result.status)
            if(result.status==200){
                this.loaddata();

            }
            else{
                alert("Not deleted")
            }



        },
        async loaddata(){
            let user=localStorage.getItem("user-info");
            this.name=JSON.parse(user).email;
            if(!user){
                this.$router.push({name:'SignUp'})
            }

            let result=await axios.get("http://127.0.0.1:8000/restaurants");
            console.warn(result)
            this.restaurants=result.data;
            }

    },
    async mounted(){
      this.loaddata();  

    }

}
</script>
<style>
td{
    width:160px;
    height: 40px;
}
</style>