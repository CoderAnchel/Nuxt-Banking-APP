<script setup>
    import { ref } from 'vue';

    const router = useRouter();

    let token = ref("");

    const data = {
        name: ref(""),
        password: ref(""),
        email: ref(""),
        address: ref(""),
        phoneNumber: ref(""),
        InitialAccountName: ref("")
    }

    const input1 = ref("");
    const input2 = ref("");
    const input3 = ref("");
    const input4 = ref("");
    const input5 = ref("");
    const input6 = ref("");

    function change1() {
        router.push('/signup');
    }

    function change2() {
        router.push('/signin');
    }

    const enviarDatos = async () => {
        data.name.value = input1.value;
        data.email.value = input2.value;
        data.phoneNumber.value = input3.value;
        data.address.value = input4.value;
        data.password.value = input5.value;
        data.InitialAccountName.value = input6.value;

        const res = await fetch('http://127.0.0.1:3001/createuser', {
            method: 'POST',
            headers: {
           'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                name: data.name.value,
                password: data.password.value,
                email: data.email.value,
                address: data.address.value,
                phoneNumber: data.phoneNumber.value,
                InitialAccountName: data.InitialAccountName.value
            })
        });
        if (!res.ok) {
            console.log('Error');
        } else {
           const responseData = await res.json();
           console.log(responseData);

            input1.value = "";
            input2.value = "";
            input3.value = "";
            input4.value = "";
            input5.value = "";
            input6.value = "";

            router.push('/signin');
        }
    }

    onMounted(() => {
        if (localStorage.getItem(`logged`) === "true") {
            router.push('/');
        }
    });

</script>
<template>
    <div class="container">
        <div class="wrapper">
            <div class="top">
                <div class="main">
                    <h1>GoBank</h1>
                </div>
                <div class="content">
                    <div class="title2">
                        <h2 style="font-weight: 500; font-size: 25px;">Create Account</h2>
                        <h3 style="font-weight: 300; color: #aaaaaa;">Start making transactions with GoBank</h3>
                    </div>
                    <div class="selector">
                        <div class="selector-container">
                            <div @click="change2" class="Signup button">
                                <span>Sign In</span>
                            </div>
                            <div @click="change1" class="SignIn button">
                                <span>Signup</span>
                            </div>
                        </div>
                    </div>
                    <div class="inputs">
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="../public/badge_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Full Name</span>
                                <input type="text" v-model="input1" >
                            </div>
                        </div>
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="public/mail_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Email</span>
                                <input type="email" v-model="input2">
                            </div>
                        </div>
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="public/call_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Phone Number</span>
                                <input type="tel" v-model="input3">
                            </div>
                        </div>
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="public/home_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Address</span>
                                <input type="text" v-model="input4">
                            </div>
                        </div>
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Initial Account Name</span>
                                <input type="text" v-model="input6">
                            </div>
                        </div>
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="../public/password_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Password</span>
                                <input type="password" v-model="input5">
                            </div>
                        </div>
                        <button @click="enviarDatos" class="sender">Continue</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="wrapper2">
            <div class="side-container">
                <img src="../public/yellow.svg" alt="gopher" style="width: 60%; height: 60%;">
            </div>
        </div>
    </div>
</template>
<style>
    .container {
        display: flex;
        }

    .wrapper {
        background: #FFFCFF;
        width: 50vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .wrapper2 {
        width: 50vw;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .side-container {
        display: flex;
        justify-content: center;
        align-items: center;
        background: #a5d8ff;
        width: 49vw;
        height: 95vh;
        border-radius: 20px;
    }


    .main {
        display: flex;
        padding: 3vh;
        justify-content: center;
        font-size: 30px;
        font-family: "DM Serif Text", serif;
        font-weight: lighter;
        font-style: italic;
    }


    .content {
        font-family: "Roboto", sans-serif;
        font-weight: 300;
        font-style: normal;
    }

    .title2 {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-self: center;
        height: 60px;
        justify-content: space-between;
    }

    .bottom {
        display: flex;
        justify-content: center;
        font-family: "Roboto", sans-serif;
        font-weight: 300;
        font-style: normal;
        padding: 20px 80px;
        text-align: center;
    }

    .selector {

        display: flex;
        justify-content: center;
        align-items: center;
        gap: 20px;
    }

    .selector-container {
        margin-top: 20px;
        background: #f0f0f2;
        display: flex;
        border-radius: 10px;
        padding: 5px;
    }

    .button {
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 10px;
        padding: 10px;
        cursor: pointer;
        font-family: "Roboto", sans-serif;
        font-weight: 700;
    }

    .SignIn {
        width: 12.5vw;
        background: #FFFCFF;
        border-radius: 10px;
        font-family: "Roboto", sans-serif;
        font-weight: 300;
        font-style: normal;
        cursor: pointer;
        padding: 15px;
        font-family: "Roboto", sans-serif;
        font-weight: 700;
    }

    .Signup {
        width: 12.5vw;
        border-radius: 10px;
        font-family: "Roboto", sans-serif;
        font-weight: 300;
        font-style: normal;
        cursor: pointer;
    }

    .inputs {
        margin: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .input1 {
        display: flex;
        padding: 5px;
        border-radius: 10px;
        border: 1px solid #f0f0f2;
        margin: 10px;
    }

    .input {
        display: flex;
        flex-direction: column;
        width: 350px;
        justify-content: center;
    }

    .icon {
        padding: 10px 20px;
    }

    .input input {
        border: none;
        background: #FFFCFF;
        padding: 10px 0;
        border-radius: 10px;
        font-weight: 500;
        font-style: normal;
        font-size: 15px;
        color: #000;
        outline: none;
    }

    .input span {
        padding-top: 5px;
        font-weight: 600;
        font-style: normal;
        font-size: 12px;
        color: #aaaaaa;
    }
    .sender {
        margin-top: 10px;
        background: #0166ff;
        color: #FFFCFF;
        border: none;
        padding: 20px;
        border-radius: 10px;
        width: 425px;
        font-weight: 600;
        font-style: normal;
        font-size: 15px;
    }

    .sender:hover {
        background: #0146ff;
        cursor: pointer;
    }

    .button:hover {
        background: #000;
        color: #FFFCFF;
        transition: all 0.2s;
        font-weight: 700;
    }
</style>
