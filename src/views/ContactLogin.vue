<template>
    <div class="page">
        <h4>Login</h4>
        <LoginForm
            :contact="contact"
            @submit:contact="login"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
    import LoginForm from '@/components/LoginForm.vue';
    import ContactService from "@/services/contact.service";
    export default{
        components: {
            LoginForm,
        },
        data() {
            return {
                contact: {},
                message: "",
            };
        },
        methods:{
            async login(data){
                try{
                    await ContactService.login(data);
                    this.message = "Success";
                }catch(error){
                    console.log(error);
                }
            }
        },
        created() {
            this.message = "";
        },
    }
</script>