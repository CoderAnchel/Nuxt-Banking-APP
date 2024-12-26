<script setup>
    import { ref } from 'vue';

    const router = useRouter();

    let token = ref("");

    function change1() {
        router.push('/signup');
    }

    function change2() {
        router.push('/signin');
    }

    const data = {
        user: ref(""),
        email: ref(""),
        password: ref(""),
    }

    const input1 = ref("");
    const input2 = ref("");

    const enviarDatos = async () => {
        data.user.value = input1.value;
        data.email.value = input1.value;
        data.password.value = input2.value;

        const res = await fetch('http://127.0.0.1:3001/login', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                user: data.user.value,
                email: data.email.value,
                password: data.password.value
            })
        });
        if (!res.ok) {
            console.log('Error');
        } else {
            const responseData = await res.json();

            console.log(responseData);

            token.value = responseData.token;
        }

        // Save important date from that JWT
            try {
                const res2 = await fetch('http://127.0.0.1:3001/user', {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${token.value}`
                    },
                });

                if(!res2.ok) {
                    console.log('Error');
                } else {
                    const responseData2 = await res2.json();

                    console.log(responseData2);

                    localStorage.setItem(`Name`, responseData2.name);
                    localStorage.setItem(`Email`, responseData2.email);
                    localStorage.setItem(`Address`, responseData2.address);
                    localStorage.setItem(`PhoneNumber`, responseData2.phoneNumber);
                    localStorage.setItem(`token`, token.value);
                    localStorage.setItem(`logged`, "true");

                    input1.value = "";
                    input2.value = "";

                    router.push('/');
                }
            } catch (error) {
                console.log('Fetch error: ', error);
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
                    <div class="title">
                        <h2 style="font-weight: 500; font-size: 32px;">Welcome Back</h2>
                        <h3 style="font-weight: 300; color: #aaaaaa;">Welcome Back, Please enter Your Details</h3>
                    </div>
                    <div class="selector">
                        <div class="selector-container">
                            <div @click="change2" class="SignIn button">
                                <span>Sign In</span>
                            </div>
                            <div @click="change1" class="Signup button">
                                <span>Signup</span>
                            </div>
                        </div>
                    </div>
                    <div class="inputs">
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="../public/badge_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Email or User</span>
                                <input type="text" v-model="input1" >
                            </div>
                        </div>
                        <div class="input1">
                            <img class="icon" style="fill: #000;" src="../public/password_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                            <div class="input">
                                <span>Password</span>
                                <input type="password" v-model="input2">
                            </div>
                        </div>
                        <button @click="enviarDatos" class="sender">Continue</button>
                    </div>
                </div>
            </div>
            <div class="bottom">
                <p>Try the GoBank fintech system capable of making transactioins and assets buy, build in FIBER and MySql and Nuxt, by @CoderAnchel.</p>
            </div>
        </div>
        <div class="wrapper2">
            <div class="side-container">
                <img src="../public/go-gopher-svgrepo-com.svg" alt="gopher" style="width: 60%; height: 60%;">
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
        padding: 8vh;
        justify-content: center;
        font-size: 40px;
        font-family: "DM Serif Text", serif;
        font-weight: lighter;
        font-style: italic;
    }


    .content {
        font-family: "Roboto", sans-serif;
        font-weight: 300;
        font-style: normal;
    }

    .title {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-self: center;
        height: 70px;
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
