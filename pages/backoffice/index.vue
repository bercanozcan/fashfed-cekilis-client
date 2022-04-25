<template>
    <div class="wrapper">
        <div class="auth" v-if="!this.$auth.loggedIn">
            <div class="container">
                <div class="form">
                    <div class="form-group">
                        <label>Email</label>
                        <input type="text" v-model="formData.email">
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" v-model="formData.password">
                    </div>
                    <div class="form-group" v-if="!loadingButton">
                        <button type="button" @click="login">Giriş</button>
                    </div>
                    <div class="form-group" v-if="loadingButton">
                        <p>Güvenlik kontrolleri sağlanıyor...</p>
                    </div>
                </div>
            </div>
        </div>
        <div class="list" v-if="this.$auth.loggedIn">
            <div>
                <h3>Katılımcılar</h3>
                <DrawList />
            </div>
        </div>
    </div>
</template>

<script>
import DrawList from '../../components/DrawList.vue';
export default {
    components: { DrawList },
    data(){
        return {
            loadingButton: false,
            formData: {
                email: "",
                password: ""
            }
        }
    },
    methods: {
        async login(){
            this.loadingButton = true;
            try {
                let response = await this.$auth.loginWith('local', { data: this.formData })
                setTimeout(()=>{
                    if(response.data.status){

                        this.$auth.setUser(response.data.data)
                        this.$auth.setUserToken(response.data.access_token).then(() => this.$toast.success('User set!'))

                        this.$notify({
                            title: 'Başarılı!',
                            message: response.data.message,
                            type: 'success'
                        });
                    }else{
                        this.$notify({
                            title: 'Uyarı!',
                            message: response.data.message,
                            type: 'warning'
                        });
                    }
                    this.loadingButton = false;
                },3000)
            } catch (error) {
                this.loadingButton = false;
                this.$notify({
                    title: 'Uyarı!',
                    message: error,
                    type: 'warning'
                });
            }
        }
    }
}
</script>

<style>
    body {
        padding: 0;
        margin: 0;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    }

    :focus-visible {
        outline: none;
    }

    .wrapper auth {
        display:flex;
        height: 100vh;
        width: 100%;
        justify-content: center;
        align-items: center;
    }

    .form {
        width: 360px;
    }

    .form-group {
        display:flex;
        flex-direction: column;
        margin-bottom:15px;
        width: 100%;
    }
    
    .form-group label{
        font-size:20px;
        margin-bottom:10px;
        font-weight: bold;
    }
    .form-group input{
        font-size:20px;
        padding-left:10px;
        padding-right: 10px;
        height: 40px;
        border:1px solid #8d8d8d;
    }
    .form-group button{
        background-color: #000;
        border:0;
        color: #fff;
        height: 50px;
        margin-top: 5px;
        font-size:20px;
    }

    .list {
        width: 100%;
    }
</style>