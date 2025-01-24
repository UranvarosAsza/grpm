<template>
    <h2>{{Userdata.contractType}}</h2>
    <br>
    <p>Szerződő neve</p>
    <p>{{Userdata.fullName}}</p>
    <p>Szerződészám</p>
    <p>{{Userdata.contractNumber}}</p>
    <p>Utolsó Befizetés</p>
    <p></p>
</template>

<script>
    import userdata from '../../resources/users.json'
    import paymentsData from '../../resources/payments.json'

     export default {
        components:{
            
        },
        data(){
            return{
                Userdata: [],
            }
        },
        mounted(){
            this.loadUserdata()
            console.log("userdata: ", this.Userdata)
        },
        methods:{
            loadUserdata(){
                this.Userdata = userdata[0];
            }
        }
    }
</script>