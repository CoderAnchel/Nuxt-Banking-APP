<script setup>
import { set } from "~/node_modules/nuxt/dist/app/compat/capi";

const token = ref("");

const router = useRouter();

let name = ref("");
let email = ref("");
let address = ref("");
let phoneNumber = ref("");
let userNUMBER = ref("");

let home = ref(true);
let transfer = ref(false);
let deposit = ref(false);
let withdraw = ref(false);
let history = ref(false);
let assets = ref(false);
let settings = ref(false);
let persons = ref(false);
let cards = ref(false);
let calculatedCost = ref(0);
let notifications = ref(0);

let showNotis = ref(false);
let requestList = ref([]);
let resolvedRequestList = ref([]);

const showNotifications = () => {
    showNotis.value = !showNotis.value;
    console.log(showNotis.value);
};

let balance = ref("");
let transfers = ref([]);
let values = ref([]);
let wallet = ref([]);
let listaCuentas = ref([]);

let date = ref("");
let hour = ref("");

const currencies = ["USD", "EUR", "GBP", "JPY", "CNY", "CAD", "AUD", "MXN", "CHF",];
const assetsList = ["AAPL", "GOOGL", "TSLA", "AMZN", "MSFT", "NFLX", "FB", "BTC", "ETH", "XRP", "GOLD", "SILVER"];
const colorsList = ["#ffec99", "#b2f2bb", "#a5d8ff"]
const plansList = ["Invest Pro", "Flex Card", "Media+", "Credit+"];

let investpro = ref(false);
let flexcard = ref(false);
let mediaplus = ref(false);
let creditplus = ref(false);

const activateInvestPro = () => {
    investpro.value = true;
    flexcard.value = false;
    mediaplus.value = false;
    creditplus.value = false;
}

const activateFlexCard = () => {
    investpro.value = false;
    flexcard.value = true;
    mediaplus.value = false;
    creditplus.value = false;
}

const activateMediaPlus = () => {
    investpro.value = false;
    flexcard.value = false;
    mediaplus.value = true;
    creditplus.value = false;
}

const activateCreditPlus = () => {
    investpro.value = false;
    flexcard.value = false;
    mediaplus.value = false;
    creditplus.value = true;
}

const selectedColor = ref("");

const showThis = ref(false);

let counter = ref(0);
let counter2 = ref(0);


const create = ref(true);

const tarjetas = [
  {
    name: "Gopherlite",
    number: "**** **** **** 1234",
    expiration: "12/23",
    cvv: "***",
    active: true,
    color: "#ffec99",
    balance: 0
  },
  {
    name: "GopherPremium",
    number: "**** **** **** 5678",
    expiration: "12/23",
    cvv: "***",
    active: false,
    color: "#b2f2bb",
    balance: 0
  },
  {
    name: "GopherGold",
    number: "**** **** **** 3786",
    expiration: "12/23",
    cvv: "***",
    active: false,
    color: "#a5d8ff",
    balance: 0
  }
]

let creditcardsList = ref([]);

let selectedcard = ref(tarjetas[0]);

let selectedFromServer = ref({});

const moveleft = () => {
  if (counter.value == 0) {
    console.log("No se puede mover a la izquierda");
  } else {
    counter.value--;
    console.log(counter.value);
    selectCard(counter.value);
  }
}

const moveright = () => {
  if (counter.value == tarjetas.length - 1) {
    console.log("No se puede mover a la derecha");
  } else {
    counter.value++;
    console.log(counter.value);
    selectCard(counter.value);
  }
}

const selectCard = (index) => {
  selectedcard.value = tarjetas[index];
  console.log(selectedcard.value);
}

//two

const moveleft2 = () => {
  if (counter2.value == 0) {
    console.log("No se puede mover a la izquierda");
  } else {
    counter2.value--;
    console.log(counter.value);
    selectCard2(counter2.value);
  }
}

const moveright2 = () => {
  if (counter2.value == creditcardsList.value.length - 1) {
    console.log("No se puede mover a la derecha");
  } else {
    counter2.value++;
    console.log(counter.value);
    selectCard2(counter2.value);
  }
}

const selectCard2 = (index) => {
  selectedFromServer.value = creditcardsList.value[index];
  console.log(selectedFromServer.value);
}



const copy = () => {

}

const qr = () => {

}

const emailSend = () => {

}

const Whatsapp = () => {

}

const sended = ref(false);

let findedUser = {
    name: ref(""),
    color: ref(""),
    small: ref(""),
    number: ref(""),
}


const gopherList = [
    {
        "color": "Purple",
        "small": "/smallPurple.svg",
        selected : ref(false),
    },
    {
        "color": "LightBlue",
        "small": "/smallLightBlue.svg",
        selected : ref(false),
    },
    {
        "color": "LightYellow",
        "small": "/smallLightYellow.svg",
        selected : ref(false),
    },
    {
        "color": "LightRed",
        "small": "/smallLightRed.svg",
        selected : ref(false),
    },
    {
        "color": "LightBrown",
        "small": "/smallLightBrown.svg",
        selected : ref(false),
    },
]

let selectedGopher = ref("a");
let smallPic = ref("");
let bigPic = ref("");

const selectRed = () => {
    selectedGopher.value = "LightRed";
    smallPic.value = "/smallLightRed.svg";
    gopherList[3].selected.value = true;
    gopherList[0].selected.value = false;
    gopherList[1].selected.value = false;
    gopherList[2].selected.value = false;
    gopherList[4].selected.value = false;

    updatePFP();
}

const selectPurple = () => {
    selectedGopher.value = "Purple";
    smallPic.value = "/smallPurple.svg";
    gopherList[0].selected.value = true;
    gopherList[1].selected.value = false;
    gopherList[2].selected.value = false;
    gopherList[3].selected.value = false;
    gopherList[4].selected.value = false;

    updatePFP();
}

const selectLightBlue = () => {
    selectedGopher.value = "LightBlue";
    smallPic.value = "/smallLightBlue.svg";
    gopherList[1].selected.value = true;
    gopherList[0].selected.value = false;
    gopherList[2].selected.value = false;
    gopherList[3].selected.value = false;
    gopherList[4].selected.value = false;

    updatePFP();
}

const selectLightYellow = () => {
    selectedGopher.value = "LightYellow";
    smallPic.value = "/smallLightYellow.svg";
    gopherList[2].selected.value = true;
    gopherList[0].selected.value = false;
    gopherList[1].selected.value = false;
    gopherList[3].selected.value = false;
    gopherList[4].selected.value = false;

    updatePFP();
}

const selectLightBrown = () => {
    selectedGopher.value = "LightBrown";
    smallPic.value = "/smallLightBrown.svg";
    gopherList[4].selected.value = true;
    gopherList[0].selected.value = false;
    gopherList[1].selected.value = false;
    gopherList[2].selected.value = false;
    gopherList[3].selected.value = false;

    updatePFP();
}

const getSmallPic = () => {
    if (findedUser.color.value == "LightRed") {
        findedUser.small.value = "/smallLightRed.svg";
    } else if (findedUser.color.value == "Purple") {
        findedUser.small.value = "/smallPurple.svg";
    } else if (findedUser.color.value == "LightBlue") {
        findedUser.small.value  = "/smallLightBlue.svg";
    } else if (findedUser.color.value == "LightYellow") {
        findedUser.small.value = "/smallLightYellow.svg";
    } else if (findedUser.color.value == "LightBrown") {
        findedUser.small.value = "/smallLightBrown.svg";
    }
}


let selectedCurrency = ref("");
let selectedAsset = ref("");
let selectedTransfer = ref({});
let showingDetails = ref(false);
let fromDetails = ref({});
let toDetails = ref({});
const input1 = ref("");
const input2 = ref("");
const input3 = ref("");
const selecting = ref(false);
const visible = ref(false);
const alert = ref(false);
const processing = ref(false);
const showAssets = ref(true);
const recipe = ref(false);

const deposit_card = ref(false);
let withdraw_card = ref(false);
let details_card = ref(false);
let transfer_card = ref(false);

const colorDefault = ref("#fffcff");

const depositCardActive = () => {
    deposit_card.value = !deposit_card.value;
    if (deposit_card.value == true) {
        withdraw_card.value = false;
        details_card.value = false;
        transfer_card.value = false;
        create.value = false;
    } else {
        create.value = true;
    }
}

const withdrawCardActive = () => {
    withdraw_card.value = !withdraw_card.value;
    if (withdraw_card.value == true) {
        deposit_card.value = false;
        details_card.value = false;
        transfer_card.value = false;
        create.value = false;
    } else {
        create.value = true;
    }
}

const transferCardActive = () => {
    transfer_card.value = !transfer_card.value;
    if (transfer_card.value == true) {
        deposit_card.value = false;
        details_card.value = false;
        withdraw_card.value = false;
        create.value = false;
    } else {
        create.value = true;
    }
}

const finded = ref(false);

const showTransfer = (ID) => {
  for (let i = 0; i < transfers.value.length; i++) {
    if (transfers.value[i].ID == ID) {
      selectedTransfer.value = transfers.value[i];

      showingDetails.value = true;
      break;
    }
  }
}


const closeTransfer = () => {
  showingDetails.value = false;
}

const changeSended = () => {
    sended.value = true;
    setTimeout(() => {
        sended.value = false;
    }, 10000);
}

const changeAlert = () => {
    alert.value = true;
    setTimeout(() => {
        alert.value = false;
    }, 5000);
}

const changeVisibility = () => {
    visible.value = true;
    setTimeout(() => {
        visible.value = false;
    }, 5000);
}

const check = () => {
    if (input2.value < 0) {
        input2.value = 0;
    }
}

const activateWindow = () => {
  selecting.value = !selecting.value;
  showAssets.value = !showAssets.value;
};

const show = () => {
  showAssets.value = !showAssets.value;
};

const showRecipe = () => {
  recipe.value = !recipe.value;
};

// const selectedAccount = (name) => {
//     for (let i = 0; i < accounts.length; i++) {
//         if (accounts[i].name == name) {
//             accounts[i].active.value = true;
//         } else {
//             accounts[i].active.value = false;
//         }
//     }
// }

const paint = () => {
    if (account.active.value == true) {
        return "selected";
    }

    return "selection";
}

const account = {
    name: ref(""),
    active: ref(false),
    balance: ref(0),
    accountNumber: ref(""),
}


const accounts = [
  {
    name: "Cuenta Ahorro",
    active: ref(false),
  },
  {
    name: " Cuenta Corriente",
    active: ref(true),
  },
];

const desplegable = ref(false);
const showDesplegable = () => {
  desplegable.value = !desplegable.value;
};

const activarHome = () => {
  home.value = true;
  transfer.value = false;
  deposit.value = false;
  withdraw.value = false;
  history.value = false;
    assets.value = false;
    settings.value = false;
    persons.value = false;
    cards.value = false;
};

const activarTransfer = () => {
  home.value = false;
  transfer.value = true;
  deposit.value = false;
  withdraw.value = false;
  history.value = false;
 assets.value = false;
 settings.value = false;
    persons.value = false;
    cards.value = false;
};

const activarDeposit = () => {
  home.value = false;
  transfer.value = false;
  deposit.value = true;
  withdraw.value = false;
  history.value = false;
    assets.value = false;
    settings.value = false;
    persons.value = false;
    cards.value = false;
};

const activarWithdraw = () => {
  home.value = false;
  transfer.value = false;
  deposit.value = false;
  withdraw.value = true;
  history.value = false;
    assets.value = false;
    settings.value = false;
    persons.value = false;
    cards.value = false;
};

const activarHistory = () => {
  home.value = false;
  transfer.value = false;
  deposit.value = false;
  withdraw.value = false;
  history.value = true;
    assets.value = false;
    settings.value = false;
    persons.value = false;
    cards.value = false;
};

const activarAssets = () => {
  home.value = false;
  transfer.value = false;
  deposit.value = false;
  withdraw.value = false;
  history.value = false;
  assets.value = true;
  settings.value = false;
  persons.value = false;
  cards.value = false;
};

const activarSettings = () => {
    persons.value = false;
  home.value = false;
  transfer.value = false;
  deposit.value = false;
  withdraw.value = false;
  history.value = false;
  assets.value = false;
  settings.value = true;
  cards.value = false;
};

const activarPersons = () => {
  persons.value = true;
  home.value = false;
    transfer.value = false;
    deposit.value = false;
    withdraw.value = false;
    history.value = false;
    assets.value = false;
    settings.value = false;
    cards.value = false;
};

const activarCards = () => {
  cards.value = true;
  home.value = false;
  transfer.value = false;
  deposit.value = false;
  withdraw.value = false;
  history.value = false;
  assets.value = false;
  settings.value = false;
};

const logOut = () => {
  localStorage.removeItem(`token`);
  localStorage.removeItem(`logged`);
  localStorage.removeItem(`Name`);
  localStorage.removeItem(`Email`);
  localStorage.removeItem(`Address`);
  localStorage.removeItem(`PhoneNumber`);
  router.push("/signin");
};


let friendList = ref([]);
let resolvedFriendList = ref([]);

const isfriend = (number) => {
    for (let i = 0; i < resolvedFriendList.value.length; i++) {
        if (resolvedFriendList.value[i].number == number) {
            return true;
        }
    }
    return false;
}

const showFriendData = async (userNUM) => {
    const res = await fetch('http://127.0.0.1:3001/showFriendData', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
          UserNUM: userNUM
        })
    })

    if (!res.ok) {
        console.log('Error');
    } else {
        const responseData = await res.json();

        resolvedFriendList.value.push({
            name: responseData.name,
            color: responseData.color,
            number: userNUM,
            small: `/small${responseData.color}.svg`,
            AccountNum: responseData.AccountNum
        })
    }

}

const obtenerFriends = async () => {
  resolvedFriendList.value = [];

  const res = await fetch("http://127.0.0.1:3001/showFriends",{
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${token.value}`,
    },
  });


  if (!res.ok) {
    console.log("Error");
    hour = new Date().toLocaleTimeString();
    changeAlert();
  } else {
    const responseData = await res.json();
    friendList.value = responseData;

    friendList.value.forEach(element => {
            showFriendData(element);
    });

    console.log(resolvedFriendList.value);
  }

}

const obtenerAccount = async () => {
  try {
    const res2 = await fetch("http://127.0.0.1:3001/checkAccounts", {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token.value}`,
      },
    });

    if (!res2.ok) {
      console.log("Error");
      hour = new Date().toLocaleTimeString();
      changeAlert();
    } else {
      const responseData2 = await res2.json();


        account.name.value = responseData2.name;
        account.balance.value = parseFloat(responseData2.balance).toFixed(2);
        account.active.value = true;
        account.accountNumber.value = responseData2.accountNumber;

        balance.value = account.balance.value;

        console.log(account);
    }
  } catch (error) {
    console.log("Fetch error: ", error);
  }
};

const obtenerTransfers = async () => {
  try {
    const res2 = await fetch("http://127.0.0.1:3001/transacctionHistory", {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token.value}`,
      },
    });

    if (!res2.ok) {
      console.log("Error");
      hour = new Date().toLocaleTimeString();
      changeAlert();
    } else {
      const responseData2 = await res2.json();

      transfers.value = responseData2;

      console.log(transfers.value);
    }
  } catch (error) {
    console.log("Fetch error: ", error);
  }
};

const obtenerWallet = async () => {
  const res = await fetch("http://127.0.0.1:3001/checkAssets", {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${token.value}`,
    },
  });

  if (!res.ok) {
    console.log("Error");
    hour = new Date().toLocaleTimeString();
    changeAlert();
  } else {
    const responseData = await res.json();

    wallet.value = responseData;

    console.log(responseData);
  }
};

const getValues = async () => {
  const res = await fetch(
    "https://faas-lon1-917a94a7.doserverless.co/api/v1/web/fn-e0f31110-7521-4cb9-86a2-645f66eefb63/default/market-prices-simulator",
    {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
    }
  );

  if (!res.ok) {
    console.log("Error");
    hour = new Date().toLocaleTimeString();
    changeAlert();
  } else {
    const responseData = await res.json();

    values.value = responseData;

    console.log(values.value);
  }
};

const sendTrasfer = async () => {
    const res = await fetch('http://127.0.0.1:3001/transferTest', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            to: input1.value,
            coin: selectedCurrency.value,
            quantity: input2.value,
            description: input3.value
        })
    })

    if (!res.ok) {
        hour = new Date().toLocaleTimeString();
        changeAlert();
        console.log('Error');
    } else {
        const responseData = await res.json();

        console.log(responseData);

        input1.value = "";
        input2.value = "";
        input3.value = "";
        selectedCurrency.value = "";

        hour = new Date().toLocaleTimeString();
        obtenerAccount();
        obtenerTransfers();
        changeVisibility();
    }
}

const sendDeposit = async () => {
    const res = await fetch('http://127.0.0.1:3001/deposit', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            coin: selectedCurrency.value,
            quantity: input2.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();

        console.log(responseData);

        input2.value = "";
        selectedCurrency.value = "";

        hour = new Date().toLocaleTimeString();
        obtenerAccount();
        obtenerTransfers();
        changeVisibility();
    }
}

const sendWithdraw = async () => {
    const res = await fetch('http://127.0.0.1:3001/withdraw', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            coin: selectedCurrency.value,
            quantity: input2.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();

        console.log(responseData);

        input2.value = "";
        selectedCurrency.value = "";

        hour = new Date().toLocaleTimeString();
        obtenerAccount();
        obtenerTransfers();
        changeVisibility();
    }
}

const calculatedPrice = () => {
    if (selectedAsset.value == "" || !values.value[selectedAsset.value] || input2.value == "") {
        calculatedCost.value = 0;
        return;
    }
    calculatedCost.value = parseFloat(values.value[selectedAsset.value]) * parseFloat(input2.value).toFixed(2);
}

watch([selectedAsset, input2], calculatedPrice);


const buyAsset =  async () => {
    processing.value = true;
    const res = await fetch("http://127.0.0.1:3001/buyassets", {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            AssetSymbol: selectedAsset.value,
            Amount: input2.value
        })
    })

    if(!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const respuesta = res.json();

        selectedAsset.value = ""
        input2.value = ""

        hour = new Date().toLocaleTimeString();
        obtenerAccount();
        obtenerTransfers();
        obtenerWallet();
        processing.value = false;
        changeVisibility();
    }
}

const updatePFP =  async () => {
    const res = await fetch("http://127.0.0.1:3001/updatePFP", {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            Color: selectedGopher.value,
        })
    })
    if(!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const respuesta = res.json();
        hour = new Date().toLocaleTimeString();
        getUserData();
        changeVisibility();
    }
}

const updateData = () => {
    updateName();
    updatePhone();
}

const updateName =  async () => {
    const res = await fetch("http://127.0.0.1:3001/updateName", {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            Name: input1.value,
        })
    })
    if(!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const respuesta = res.json();
        hour = new Date().toLocaleTimeString();
        input1.value = "";
        getUserData();
        changeVisibility();
    }
}

const updatePhone =  async () => {
    const res = await fetch("http://127.0.0.1:3001/updatePhone", {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            Number: input2.value,
        })
    })
    if(!res.ok) {
        console.log('Error');
    } else {
        const respuesta = res.json();

        input2.value = "";
        getUserData();
    }
}

const acceptRequest = async (number) => {
    const res = await fetch('http://127.0.0.1:3001/acceptFriendRequest',{
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            UserNUM: number
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();
        console.log(responseData);
        hour = new Date().toLocaleTimeString();
        getUserData();
        notifications.value = resolvedRequestList.value.length;
        showNotis.value = false;
        changeVisibility();
        obtenerFriends();
    }
}

const getRequests =  (lista) => {
    notifications.value = 0;
    resolvedRequestList.value = [];

    requestList.value = lista;
    requestList.value.forEach(element => {
        searchUser2(element).then((res) => {
            resolvedRequestList.value.push(res);
            notifications.value = resolvedRequestList.value.length;
        })
    });
    resolvedRequestList.value.forEach(element => {
        console.log(element);
    });
}


const getUserData = async () => {
    const res = await fetch('http://127.0.0.1:3001/user', {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        }
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();

        name.value = responseData.name;
        email.value = responseData.email;
        address.value = responseData.address;
        phoneNumber.value = responseData.phoneNumber;
        userNUMBER.value = responseData.UserNUM;
        // Color recibido del backend
        const receivedColor = responseData.Color;

        // Recorrer gopherList para encontrar coincidencias
        gopherList.forEach((gopher) => {
            // Si el color coincide, marcamos selected como true
            if (gopher.color === receivedColor) {
                gopher.selected.value = true;
                selectedGopher.value = gopher.color;
                smallPic.value = gopher.small;
            } else {
                // Si no coincide, aseguramos que selected sea false
                gopher.selected.value = false;
            }
        });

        if (responseData.Requests != null) {
            getRequests(responseData.Requests);
        }
        localStorage.setItem('Name', name.value);
        localStorage.setItem('Email', email.value);
        localStorage.setItem('Address', address.value);
        localStorage.setItem('PhoneNumber', phoneNumber.value);
    }
}

const searchUser2 = async (number) => {
    const res = await fetch('http://127.0.0.1:3001/showUser',{
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            UserNUM: number
        })
    })

    if (!res.ok) {
        console.log('Error');
    } else {
        const responseData = await res.json();

        return {
            name: responseData.name,
            color: responseData.Color,
            number: number,
            small: `/small${responseData.Color}.svg`
        }
    }
}

const searchUser = async () => {
    const res = await fetch('http://127.0.0.1:3001/showUser',{
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            UserNUM: input1.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
        finded.value = false;
    } else {
        const responseData = await res.json();

        findedUser.name.value = responseData.name;
        findedUser.color.value = responseData.Color;
        findedUser.number.value = input1.value;
        getSmallPic();
        input1.value = "";
        finded.value = true;
    }
}

const sendFriendRequest = async () => {
    processing.value = true;
    const res = await fetch('http://127.0.0.1:3001/sendFriendRequest', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            To: findedUser.number.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        processing.value = false;
        changeAlert();
    } else {
        const responseData = await res.json();
        console.log(responseData);
        hour = new Date().toLocaleTimeString();
        processing.value = false;
        changeSended();
        changeVisibility();
    }

}

let selectedNumero = ref("");
const selectFriendForTransfer = (number) => {
    input1.value = number;
    selectedNumero.value = number;
}

let number = ref(0);


const transferFromCard = async () => {
    const res = await fetch('http://127.0.0.1:3001/transferFromCard',{
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            cardNum: selectedFromServer.value.Number,
            amount: input2.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();
        console.log(responseData);
        input2.value = "";
        hour = new Date().toLocaleTimeString();
        changeVisibility();
        obtenerAccount();
        fetchCards();
        obtenerTransfers();
    }
}

const withdrawFromCard = async () => {
    const res = await fetch('http://127.0.0.1:3001/withdrawFromCard',{
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            cardNum: selectedFromServer.value.Number,
            amount: input2.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();
        console.log(responseData);
        input2.value = "";
        hour = new Date().toLocaleTimeString();
        changeVisibility();
        obtenerAccount();
        fetchCards();
        obtenerTransfers();
    }
}

const depostiToCard = async () => {
    const res = await fetch('http://127.0.0.1:3001/depositCard',{
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            cardNum: selectedFromServer.value.Number,
            amount: input2.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();
        console.log(responseData);
        input2.value = "";
        hour = new Date().toLocaleTimeString();
        changeVisibility();
        obtenerAccount();
        fetchCards();
        obtenerTransfers();
    }
}

const fetchCards = async () => {
    const res = await fetch('http://127.0.0.1:3001/creditCards',{
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        }
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();
        creditcardsList.value = responseData;

        number.value = creditcardsList.value.length;

        selectedFromServer.value = creditcardsList.value[0];
        console.log(creditcardsList.value);
    }
}

const createCard = async () => {
    if (input2.value == "" || selectedColor.value == "") {
      console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
      const res = await fetch('http://127.0.0.1:3001/createCard', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token.value}`,
        },
        body: JSON.stringify({
            Name: input2.value,
            Color: selectedColor.value
        })
    })

    if (!res.ok) {
        console.log('Error');
        hour = new Date().toLocaleTimeString();
        changeAlert();
    } else {
        const responseData = await res.json();
        console.log(responseData);

        input2.value = "";
        hour = new Date().toLocaleTimeString();
        changeVisibility();
        fetchCards();
    }
    }
}

onMounted(() => {
  token.value = localStorage.getItem(`token`);
  if (token.value === null) {
    router.push("/signin");
  }

  name.value = localStorage.getItem(`Name`);
  email.value = localStorage.getItem(`Email`);
  address.value = localStorage.getItem(`Address`);
  phoneNumber.value = localStorage.getItem(`PhoneNumber`);

  date = new Date().toLocaleDateString();
  hour = new Date().toLocaleTimeString();

  console.log(name.value);

  obtenerAccount();
  obtenerTransfers();
  getValues();
  obtenerWallet();
  getUserData();
  obtenerFriends();
  fetchCards();
});
</script>
<template>
  <div class="wrapper-index">
    <div class="main-index">
      <div class="navbar">
        <div class="logo">
          <h1>GoBank</h1>
        </div>

        <div class="options">
          <button :class="{ active: home }" @click="activarHome">
            <img
              v-if="home"
              src="public/home_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!home"
              src="public/home_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Home</span>
          </button>
          <button
            id="trans"
            :class="{ active: transfer }"
            @click="activarTransfer"
          >
            <img
              v-if="transfer"
              src="public/send_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!transfer"
              src="public/send_money_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Transfer</span>
          </button>
          <button
            id="depo"
            :class="{ active: deposit }"
            @click="activarDeposit"
          >
            <img
              v-if="deposit"
              src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!deposit"
              src="public/payments_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Deposit</span>
          </button>
          <button
            id="withd"
            :class="{ active: withdraw }"
            @click="activarWithdraw"
          >
            <img
              v-if="withdraw"
              src="public/money_bag_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!withdraw"
              src="public/money_bag_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Withdraw</span>
          </button>
          <button
            id="hist"
            :class="{ active: cards }"
            @click="activarCards"
          >
            <img
              v-if="cards"
              src="public/credit_card_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!cards"
              src="public/credit_card_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Cards</span>
          </button>
          <button
            id="hist"
            :class="{ active: assets }"
            @click="activarAssets"
          >
            <img
              v-if="assets"
              src="public/account_balance_wallet_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!assets"
              src="public/account_balance_wallet_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Assets</span>
          </button>
          <button
            id="hist"
            :class="{ active: history }"
            @click="activarHistory"
          >
            <img
              v-if="history"
              src="public/manage_search_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!history"
              src="public/manage_search_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>History</span>
          </button>
          <!-- <button
            id="hist"
            :class="{ active: settings }"
            @click="activarSettings"
          >
            <img
              v-if="settings"
              src="public/manage_accounts_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!settings"
              src="public/manage_accounts_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Settings</span>
          </button> -->
          <button
            id="hist"
            :class="{ active: persons }"
            @click="activarPersons"
          >
            <img
              v-if="persons"
              src="public/group_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <img
              v-if="!persons"
              src="public/group_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Persons</span>
          </button>
          <!-- <button @click="logOut">
            <img
              src="public/logout_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
              alt=""
            />
            <span>Log-out</span>
          </button> -->
        </div>

        <div class="menu">
            <div>
                <span style="position: relative !important; bottom: 9px; left: 13px">{{ notifications }}</span>
                <img
                    @click="showNotifications()"
                    class="notis"
                    src="public/notifications_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                />
            </div>

          <div>
            <span style="font-family: roboto; font-weight: 400">{{
              name
            }}</span>
            <img class="profile-pic" @click="showDesplegable()"  style="border: 2px solid #161d2c; padding: 5px 15px; border-radius: 50%; width: 40px; margin: 7px; background: #fffcff"  :src="smallPic" width="50px" alt="" />
          </div>
        </div>
      </div>
      <div class="main-body" v-if="home">
        <div class="column1">
          <div class="card-wrapper">
            <div class="row1">
              <div class="card-title">
                <h1
                  style="font-family: roboto; font-weight: 500; font-size: 22px"
                >
                  Total balance
                </h1>
                <h1 style="font-weight: 400">$ {{ balance }}</h1>
              </div>
              <div class="ticket-wrapper">
                <div class="ticket">-$28,23</div>
              </div>
            </div>
            <div class="row2">
              <div class="row2-wrapper">
                <div>
                  <div class="ticket">
                    <img
                      src="public/trending_up_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg"
                      alt=""
                    />
                    <span>+10%</span>
                  </div>
                </div>
                <p>compared <br />to last month</p>
              </div>
            </div>
          </div>
        </div>

        <div class="column2">
          <div class="card-wrapper second">
            <div class="row1">
              <div class="card-title">
                <h1 style="font-weight: 400; color: #47f3ce">+ $ 835.89</h1>
              </div>
              <div
                style="
                  border: 1px solid;
                  border-color: #47f3ce;
                  height: 30px;
                  padding: 5px 20px;
                  border-radius: 30px;
                "
                class="ticket-wrapper"
              >
                <img
                  src="public/trending_up_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                  alt=""
                />
                <span style="color: #47f3ce">+10%</span>
              </div>
            </div>
            <div class="row2">
              <p>Income this month</p>
            </div>
          </div>
          <div class="card-wrapper second">
            <div class="row1">
              <div class="card-title">
                <h1 style="font-weight: 400; color: #fc090f">- $ 255.59</h1>
              </div>
              <div
                style="
                  border: 1px solid;
                  border-color: #fc090f;
                  height: 30px;
                  padding: 5px 20px;
                  border-radius: 30px;
                "
                class="ticket-wrapper"
              >
                <img
                  src="public/trending_up_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg"
                  alt=""
                />
                <span style="color: #fc090f; margin: 0 !important">+40%</span>
              </div>
            </div>
            <div class="row2">
              <p>Spend this month</p>
            </div>
          </div>
        </div>

        <div class="column3">
          <div
            class="card-wrapper third"
            style="background: #161d2c; color: #fffcff"
          >
            <div class="row1">
              <div class="card-title">
                <h1
                  style="font-family: roboto; font-weight: 500; font-size: 22px"
                >
                  Market Values
                </h1>
              </div>
              <div class="ticket-wrapper">
                <div class="ticket espt" style="border-color: #fffcff">BUY</div>
              </div>
            </div>
            <div class="row2 gridRow">
              <div class="row2-wrapper grid">
                <li v-for="[key, value] in Object.entries(values)" :key="key">
                  <div style="display: flex; align-items: center">
                    <img
                      v-if="key == 'AAPL'"
                      src="public/Apple_logo_black.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'GOOGL'"
                      src="public/Google__G__logo.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'TSLA'"
                      src="public/tesla-svgrepo-com.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'AMZN'"
                      src="public/Amazon_icon.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'MSFT'"
                      src="public/Microsoft_logo.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'NFLX'"
                      src="public/netflix-1-logo-svgrepo-com.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'FB'"
                      src="public/meta-icon.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'BTC'"
                      src="public/Bitcoin.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'ETH'"
                      src="public/ethereum-eth.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'XRP'"
                      src="public/svgviewer-output.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'GOLD'"
                      src="public/gold-ingot-gold-svgrepo-com.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="key == 'SILVER'"
                      src="public/silver-icon.svg"
                      alt=""
                      width="15px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <span>{{ key }}</span>
                  </div>
                  <p style="color: #47f3ce">{{ value }}$</p>
                </li>
              </div>
            </div>
            <div
              style="
                display: flex;
                align-items: flex-end;
                justify-content: space-between;
                padding: 0 10px;
              "
            >
              <div></div>
              <span style="margin-top: 10px">{{ hour }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-if="home">
      <div class="container-content">
        <div class="card1">
          <div class="row1">
            <h1 style="font-size: 22px; font-weight: 500">
              Recent transaction
            </h1>
            <button class="button especial">View all</button>
          </div>
          <div
            class="carrussel"
            style="overflow: hidden; overflow-y: auto; height: 30vh"
          >
            <div></div>
            <li class="item" v-for="item in transfers" :key="item.ID">
              <div class="item item2">
                <div style="display: flex">
                  <img
                    v-if="item.TransactionType == 'CASH_DEPOSIT'"
                    src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                  />
                  <img
                    v-if="item.TransactionType == 'CASH_WITHDRAW'"
                    src="public/money_bag_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                  />
                  <img
                    v-if="item.TransactionType == 'ASSETS_BUY'"
                    src="public/finance_mode_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                  />
                  <img
                    v-if="item.TransactionType == 'CASH_TRANSFER'"
                    src="public/send_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                    />
                    <img
                      v-if="item.TransactionType == 'CARD_WITHDRAW' || item.TransactionType == 'CARD_DEPOSIT' || item.TransactionType == 'CARD_TO_ACCOUNT'"
                      src="public/credit_card_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                      alt=""
                    />
                  <p style="margin-left: 10px">{{ item.TransactionType }}</p>
                </div>
                <h1
                  v-if="item.TransactionType == 'CARD_DEPOSIT'"
                  style="font-size: 18px; font-weight: 400; color: #09b96d"
                >
                  + {{ item.quantity }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'CARD_TO_ACCOUNT'"
                  style="font-size: 18px; font-weight: 400; color: #09b96d"
                >
                   {{ item.quantity }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'CARD_WITHDRAW'"
                  style="font-size: 18px; font-weight: 400; color: #fc090f"
                >
                  - {{ item.quantity }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'CASH_DEPOSIT'"
                  style="font-size: 18px; font-weight: 400; color: #09b96d"
                >
                  + {{ item.quantity }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'CASH_WITHDRAW'"
                  style="font-size: 18px; font-weight: 400; color: #fc090f"
                >
                  - {{ item.quantity }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'ASSETS_BUY'"
                  style="font-size: 18px; font-weight: 400; color: #fc090f"
                >
                  - {{ parseFloat(item.Cost).toFixed(2) }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'CASH_TRANSFER' && item.From == account.accountNumber.value"
                  style="font-size: 18px; font-weight: 400; color: #fc090f"
                >
                  - {{ parseFloat(item.quantity).toFixed(2) }}$
                </h1>
                <h1
                  v-if="item.TransactionType == 'CASH_TRANSFER' && item.To == account.accountNumber.value"
                  style="font-size: 18px; font-weight: 400; color: #09b96d">
                  + {{ parseFloat(item.quantity).toFixed(2) }}$
                </h1>
              </div>
            </li>
          </div>
        </div>

        <div class="card1 accounts-card">
          <div class="row1">
            <h1 style="font-size: 22px; font-weight: 500">Select Account</h1>
          </div>
          <div
            class="carrussel"
            style="
              overflow: hidden;
              overflow-y: auto;
              max-height: 300px !important;
              height: 240px;
            "
          >
            <div></div>
            <li
              class="item account"
              style="border-bottom: none !important"
            >
              <div class="item item2" style="border-color: #fffcff">
                <div style="display: flex">
                  <img
                    src="public/account_balance_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                    style="margin-right: 10px"
                  />
                  <p>{{ account.name.value }}</p>
                </div>
                <img
                  src="public/add_circle_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg"
                  alt=""
                  style="margin-right: 10px"
                />
              </div>
            </li>
          </div>
        </div>

        <div class="card1 accounts-card2">
          <div class="row1">
            <h1
              style="
                font-size: 22px;
                font-weight: 500;
                display: flex;
                align-items: center;
              "
            >
              Assets
              <img
                style="margin-left: 10px"
                src="public/wallet_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg"
                alt=""
              />
            </h1>
          </div>
          <div
            class="carrussel"
            style="
              overflow: hidden;
              overflow-y: auto;
              height: 30svh;
              display: flex;
              flex-direction: column;
              justify-content: space-between;
              list-style: none;
            "
          >
            <div></div>
            <li
              v-for="[key, value] in Object.entries(wallet)"
              :key="key"
              style="
                margin: 10px;
                display: flex;
                justify-content: space-between;
                align-items: center;
                border-bottom: 1px solid #fffcff;
              "
            >
              <div
                style="display: flex; align-items: center; margin-right: 20px"
              >
                <img
                  v-if="key == 'AAPL'"
                  src="public/Apple_logo_black.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'GOOGL'"
                  src="public/Google__G__logo.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'TSLA'"
                  src="public/tesla-svgrepo-com.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'AMZN'"
                  src="public/Amazon_icon.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'MSFT'"
                  src="public/Microsoft_logo.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'NFLX'"
                  src="public/netflix-1-logo-svgrepo-com.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'FB'"
                  src="public/meta-icon.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'BTC'"
                  src="public/Bitcoin.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'ETH'"
                  src="public/ethereum-eth.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'XRP'"
                  src="public/svgviewer-output.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'GOLD'"
                  src="public/gold-ingot-gold-svgrepo-com.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'SILVER'"
                  src="public/silver-icon.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <span
                  style="
                    font-style: italic;
                    font-weight: 500;
                    font-family: quantico;
                  "
                  >{{ key }}</span
                >
              </div>
              <div
                style="
                  display: flex;
                  justify-content: space-between;
                  width: 20vw;
                "
              >
                <p
                  style="
                    width: 50px;
                    display: flex !important;
                    justify-content: center;
                  "
                >
                  {{ parseFloat(value.Quantity_Owned ).toFixed(8)}}
                </p>
                <p style="color: #47f3ce">
                  {{ parseFloat(value.Profit).toFixed(2) }}$
                </p>
              </div>
            </li>
          </div>
        </div>
      </div>
    </div>

    <div v-if="transfer" class="transfer-main">
      <div class="left">
        <h1>Transfer</h1>
        <div class="row1-transfer">
          <div class="account-selector-transfer">
            <h3>Selected Account</h3>
                <div v-if="account.active.value" class="transfer-selected-account" style="display: flex;">
                    <div style="display: flex; margin-left: 10px; margin-right: 20px;">
                        <img
                            src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                            alt=""
                            style="margin-right: 10px;"
                        />
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name  }}</p>
                    </div>
                    <button @click="activateWindow" class="changer">Change</button>
            </div>
          </div>

          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>
        <div class="inputs-transfer">
            <div class="input-trans">
                <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/person_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Reciver Account Number
                    </span>
                <input v-model="input1" style="font-style: italic;" type="text" placeholder="Introduce" />
            </div>
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">
                        Amount
                    </span>
                    <input v-model="input2"  style="color: #09b96d; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img v-if="selectedCurrency == ''" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'EUR'" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'JPY'" style="margin-right: 10px; padding: 0;" src="public/currency_yen_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'USD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CAD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'AUD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'GBP'" style="margin-right: 10px; padding: 0;" src="public/currency_pound_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CNY'" style="margin-right: 10px; padding: 0;" src="public/currency_yuan_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CHF'" style="margin-right: 10px; padding: 0;" src="public/currency_franc_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Divisa
                    </span>
                    <select class="select" id="currency" v-model="selectedCurrency">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="input-trans">
                <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/sticky_note_2_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Affair
                    </span>
                <input v-model="input3" type="text" placeholder="Description" />
            </div>
            <button @click="sendTrasfer" id="sender-transfer">
                Confirm
            </button>
        </div>
      </div>

        <div v-if="transfer" class="bar">

    </div>


    <div v-if="transfer" class="left selecting">
        <div style="display: flex; justify-content: space-between; align-items: center">
            <h1>Contacts</h1>
            <div>
                <input type="text" placeholder="introduce" style="margin: 0; padding: 5px 10px !important; height: 30px; border-radius: 0; border: 1px solid #020514; font-family: roboto; font-style: italic; ">
                <button class="accepters"  style="padding: 11.5px 10px; background: #1b76ff; color: #fffcff; font-family: quantico; border: none; ">Accept</button>
            </div>
        </div>
        <div class="assets-carrousel" style="margin-left: 20px; display: flex; flex-wrap: wrap; overflow: hidden;
              overflow-y: auto;
              max-height:80vh !important;
              height: 80vh;">
              <div  v-for="friend in resolvedFriendList" :key="friend.userNum">
                <div v-if="selectedNumero == friend.AccountNum"  @click="selectFriendForTransfer(friend.AccountNum)" style=" display: flex; flex-direction: column; align-items: center;">
                    <img class="smallGoph" style="border: 2px solid #1b76ff; padding: 10px 20px; border-radius: 50%; width: 60px; margin: 7px; background: #fffcff"  :src="friend.small" alt="" />
                    <span style="font-family: roboto; font-weight: 400; font-size: 18px">{{ friend.name  }}</span>
                </div>
                <div class="smallGoph" v-if="!(selectedNumero == friend.AccountNum)" @click="selectFriendForTransfer(friend.AccountNum)" style=" display: flex; flex-direction: column; align-items: center;">
                    <img style="border: 2px solid #161d2c; padding: 10px 20px; border-radius: 50%; width: 60px; margin: 7px; background: #fffcff"  :src="friend.small" alt="" />
                    <span style="font-family: roboto; font-weight: 400; font-size: 18px">{{ friend.name  }}</span>
                </div>
              </div>
        </div>

    </div>



      <div v-if="selecting" class="bar">

      </div>


    <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>

</div>
















    <div v-if="deposit" class="transfer-main">
      <div class="left2">
        <h1>Deposit</h1>
        <div class="row1-transfer">
            <div class="account-selector-transfer">
            <h3>Selected Account</h3>
            <div v-for="account in accounts" :key="account.name" >
                <div v-if="account.active.value" class="transfer-selected-account" style="display: flex;">
                    <div style="display: flex; margin-left: 10px; margin-right: 20px;">
                        <img
                            src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                            alt=""
                            style="margin-right: 10px;"
                        />
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name  }}</p>
                    </div>
                    <button @click="activateWindow" class="changer">Change</button>
            </div>
            </div>
          </div>

          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>

        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">
                        Amount
                    </span>
                    <input v-model="input2"  style="color: #09b96d; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img v-if="selectedCurrency == ''" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'EUR'" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'JPY'" style="margin-right: 10px; padding: 0;" src="public/currency_yen_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'USD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CAD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'AUD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'GBP'" style="margin-right: 10px; padding: 0;" src="public/currency_pound_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CNY'" style="margin-right: 10px; padding: 0;" src="public/currency_yuan_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CHF'" style="margin-right: 10px; padding: 0;" src="public/currency_franc_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Divisa
                    </span>
                    <select class="select" id="currency" v-model="selectedCurrency">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>

            <button @click="sendDeposit" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>

      <div v-if="selecting" class="bar">

    </div>

      <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>














    <div v-if="withdraw" class="transfer-main">
      <div class="left2">
        <h1>Withdraw</h1>
        <div class="row1-transfer">
            <div class="account-selector-transfer">
            <h3>Selected Account</h3>
            <div v-for="account in accounts" :key="account.name" >
                <div v-if="account.active.value" class="transfer-selected-account" style="display: flex;">
                    <div style="display: flex; margin-left: 10px; margin-right: 20px;">
                        <img
                            src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                            alt=""
                            style="margin-right: 10px;"
                        />
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name  }}</p>
                    </div>
                    <button @click="activateWindow" class="changer">Change</button>
            </div>
            </div>
          </div>

          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>

        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">
                        Amount
                    </span>
                    <input v-model="input2"  style="color: #fc090f; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img v-if="selectedCurrency == ''" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'EUR'" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'JPY'" style="margin-right: 10px; padding: 0;" src="public/currency_yen_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'USD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CAD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'AUD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'GBP'" style="margin-right: 10px; padding: 0;" src="public/currency_pound_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CNY'" style="margin-right: 10px; padding: 0;" src="public/currency_yuan_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CHF'" style="margin-right: 10px; padding: 0;" src="public/currency_franc_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Divisa
                    </span>
                    <select class="select" id="currency" v-model="selectedCurrency">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>

            <button @click="sendWithdraw" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>

      <div v-if="selecting" class="bar">

    </div>

      <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>






    <div v-if="cards" class="transfer-main">
      <div v-if="showAssets" class="left selecting">
        <h1>Credit Cards</h1>

        <div class="card-selector">
          <!-- <div>
            <div class="card" style="padding: 20px; margin-bottom: 20px; display: flex; justify-content: space-between;">
              <button @click="moveleft()" class="chevron" style="background: none; border: none;"><img src="public/chevron_left_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""></button>
              <div>
                <div class="card-container">
                  <div class="card2" :style="{ border: '1px solid #020514',width: '380px',height: '230px',padding: '0px 20px',borderRadius: '20px',flexDirection: 'column',background: selectedcard ? selectedcard.color : '#ffffff'}">
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%; align-items: center;">
                      <div style="display: flex; align-items: center;">
                        <h1 style="font-size: 25px; margin-right: 10px">GoBank</h1>
                        <div style="background: #C0C0C0; border-radius: 5px; height: 30px; width: 30px;">
                        <img src="public/chip-debit-svgrepo-com.svg" width="30px" alt="">
                        </div>
                      </div>
                      <span style="font-family: quantico;">{{ selectedcard.name }}</span>
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%; align-items: center;">
                      <span style="font-family: roboto; font-weight: 400">My Balance</span>
                      <img src="public/more_horiz_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%;    align-items: center;">
                      <div class="logo">
                        <h1 style="font-size: 25px; margin-right: 10px; display: flex; align-items: center; font-family: quantico">{{ selectedcard.balance  }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""></h1>
                      </div>
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%; align-items: center;">
                      <span style="font-family: roboto; font-weight: 400">Number</span>
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%;    align-items: center;">
                        <h1 style="font-size: 25px; margin-right: 10px; display: flex; align-items: center; font-family: roboto; font-weight: 400">{{ selectedcard.number }}</h1>
                    </div>
                  </div>
                </div>
              </div>
              <button @click="moveright()"  class="chevron" style="background: none; border: none;" ><img src="public/chevron_right_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""></button>
            </div>
          </div> -->

          <div v-for="card in creditcardsList" :key="card.Number">
            <div v-if="card.Number == selectedFromServer.Number" style="display: flex; flex-direction: column">
            <div class="card" style="padding: 20px; margin-bottom: 20px; display: flex; justify-content: space-between;">
              <button @click="moveleft2()" class="chevron" style="background: none; border: none;"><img src="public/chevron_left_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""></button>
              <div>
                <div class="card-container">
                  <div class="card2" :style="{ border: '1px solid #020514',width: '380px',height: '230px',padding: '0px 20px',borderRadius: '20px',flexDirection: 'column',background: card ? card.color : '#ffffff'}">
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%; align-items: center;">
                      <div style="display: flex; align-items: center;">
                        <h1 style="font-size: 25px; margin-right: 10px">GoBank</h1>
                        <div style="background: #C0C0C0; border-radius: 5px; height: 30px; width: 30px;">
                        <img src="public/chip-debit-svgrepo-com.svg" width="30px" alt="">
                        </div>
                      </div>
                      <span style="font-family: quantico;">{{ card.name }}</span>
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%; align-items: center;">
                      <span style="font-family: roboto; font-weight: 400">My Balance</span>
                      <img src="public/more_horiz_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%;    align-items: center;">
                      <div class="logo">
                        <h1 style="font-size: 25px; margin-right: 10px; display: flex; align-items: center; font-family: quantico">{{ card.Balance  }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""></h1>
                      </div>
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%; align-items: center;">
                      <span style="font-family: roboto; font-weight: 400">Number</span>
                    </div>
                    <div class="card-row" style="display: flex; justify-content: space-between; width: 100%;    align-items: center;">
                        <h1 style="font-size: 25px; margin-right: 10px; display: flex; align-items: center; font-family: roboto; font-weight: 400">{{ card.CensoredNumber }}</h1>
                    </div>
                  </div>
                </div>
              </div>
              <button @click="moveright2()"  class="chevron" style="background: none; border: none;" ><img src="public/chevron_right_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""></button>
            </div>
            <span style="display: flex; justify-content: center; font-family: quantico">{{ counter2 +1 }} / {{ number  }}</span>
          </div>
          </div>
        </div>

        <div v-if="number > 0"  class="botonera" style=" display: flex; justify-content: space-between; margin-top: 50px">
          <button @click="depositCardActive()" class="card-buttons" style="padding:10px 20px; font-family: quantico; background: #1b76ff; color: #fffcff; border: none; border-radius: 10px; font-size: 20px; font-style: italic; display: flex"><img src="public/send_money_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24 (1).svg" style="margin-right: 10px" alt="">Deposit</button>
          <button @click="transferCardActive()" class="card-buttons" style="padding:10px 20px; font-family: quantico; background: #1b76ff; color: #fffcff; border: none; border-radius: 10px; font-size: 20px; font-style: italic; display: flex"><img src="public/move_up_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg" style="margin-right: 10px" alt="">Transfer</button>
          <button class="card-buttons" style="padding:10px 20px; font-family: quantico; background: #1b76ff; color: #fffcff; border: none; border-radius: 10px; font-size: 20px; font-style: italic; display: flex"><img src="public/credit_card_gear_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg" style="margin-right: 10px" alt="">Details</button>
          <button @click="withdrawCardActive()" class="card-buttons" style="padding:10px 20px; font-family: quantico; background: #1b76ff; color: #fffcff; border: none; border-radius: 10px; font-size: 20px; font-style: italic; display: flex"><img src="public/credit_card_off_24dp_F3F3F3_FILL0_wght400_GRAD0_opsz24.svg" style="margin-right: 10px" alt="">Withdraw</button>
        </div>

        </div>

        <div  class="bar">

        </div>


        <div v-if="deposit_card" class="left2 create">
        <h1 style="font-size: 35px !important; font-family: quantico">{{ selectedFromServer.name  }} Deposit</h1>
        <div class="row1-transfer" style="display: flex;">
          <img src="public/send_money_24dp_000000_FILL0_wght400_GRAD0_opsz24 (2).svg" width="90px" style="margin-right: 10px" alt="">
          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>

        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">
                        Amount
                    </span>
                    <input v-model="input2"  style="color: #09b96d; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img v-if="selectedCurrency == ''" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'EUR'" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'JPY'" style="margin-right: 10px; padding: 0;" src="public/currency_yen_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'USD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CAD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'AUD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'GBP'" style="margin-right: 10px; padding: 0;" src="public/currency_pound_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CNY'" style="margin-right: 10px; padding: 0;" src="public/currency_yuan_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CHF'" style="margin-right: 10px; padding: 0;" src="public/currency_franc_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Divisa
                    </span>
                    <select class="select" id="currency" v-model="selectedCurrency">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>

            <button @click="depostiToCard()" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>





      <div v-if="transfer_card" class="left2 create">
        <h1 style="font-size: 35px !important; font-family: quantico">{{ selectedFromServer.name  }} Transfer</h1>
        <div class="row1-transfer">
          <div class="account-selector-transfer">
            <h3>Selected Account</h3>
                <div v-if="account.active.value" class="transfer-selected-account" style="display: flex;">
                    <div style="display: flex; margin-left: 10px; margin-right: 20px;">
                        <img
                            src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                            alt=""
                            style="margin-right: 10px;"
                        />
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name  }}</p>
                    </div>
                    <button @click="activateWindow" class="changer">Change</button>
            </div>
          </div>

          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>

        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">
                        Amount
                    </span>
                    <input v-model="input2"  style="color: #09b96d; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img v-if="selectedCurrency == ''" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'EUR'" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'JPY'" style="margin-right: 10px; padding: 0;" src="public/currency_yen_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'USD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CAD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'AUD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'GBP'" style="margin-right: 10px; padding: 0;" src="public/currency_pound_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CNY'" style="margin-right: 10px; padding: 0;" src="public/currency_yuan_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CHF'" style="margin-right: 10px; padding: 0;" src="public/currency_franc_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Divisa
                    </span>
                    <select class="select" id="currency" v-model="selectedCurrency">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>

            <button @click="transferFromCard()" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>






      <div v-if="withdraw_card" class="left2 create">
        <h1 style="font-size: 35px !important; font-family: quantico">{{ selectedFromServer.name  }} Withdraw</h1>
        <div class="row1-transfer" style="display: flex;">
          <img src="public/credit_card_off_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" width="90px" alt="">
          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>

        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">
                        Amount
                    </span>
                    <input v-model="input2"  style="color: #fc090f; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img v-if="selectedCurrency == ''" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'EUR'" style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'JPY'" style="margin-right: 10px; padding: 0;" src="public/currency_yen_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'USD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CAD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'AUD'" style="margin-right: 10px; padding: 0;" src="public/attach_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'GBP'" style="margin-right: 10px; padding: 0;" src="public/currency_pound_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CNY'" style="margin-right: 10px; padding: 0;" src="public/currency_yuan_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        <img v-if="selectedCurrency == 'CHF'" style="margin-right: 10px; padding: 0;" src="public/currency_franc_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Divisa
                    </span>
                    <select class="select" id="currency" v-model="selectedCurrency">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="currency in currencies" :key="currency" :value="currency">
                            {{ currency }}
                        </option>
                    </select>
                </div>
            </div>

            <button @click="withdrawFromCard()" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>










      <div v-if="create" class="left2 create">
        <h1>Create New <img src="public/add_card_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" width="40px" alt=""></h1>
        <p style="font-family: roboto; margin-top: 0px; font-weight: 300">
          At GoBank, we understand that <b>every customer has unique needs</b>, which is why we offer three types of prepaid cards designed to fit different lifestyles and goals:
        </p>
        <span style="font-family: roboto; font-weight: 500;">Hover to see!</span>
        <div style="display: flex; margin-top: 30px; justify-content: center;">
          <div style="display: flex; width: 500px;  justify-content: space-between;">
            <div @mouseover="activateInvestPro()" class="card2 "  style="background: #000; color: #fffcff; width: 100px; height: 60px; border-radius: 13px; display: flex; justify-content: center; align-items: center;">
              <span style="font-family: DM Serif Text;font-style: italic;">INVEST Pro</span>
            </div>
            <div @mouseover="activateFlexCard()" class="card2 "  style="background: #b2f2bb; color: #020514; width: 100px; height: 60px; border-radius: 13px; display: flex; justify-content: center; align-items: center;">
              <span style="font-family: Lexend Exa">Flex Card </span>
            </div>
            <div @mouseover="activateMediaPlus()" class="card2 "  style="background: #a5d8ff; color: #020514; width: 100px; height: 60px; border-radius: 13px; display: flex; justify-content: center; align-items: center;">
               <span style="font-family: quantico">Media+</span>
            </div>
            <div @mouseover="activateCreditPlus()" class="card2 "  style="background: #ffec99; color: #020514; width: 100px; height: 60px; border-radius: 13px; display: flex; justify-content: center; align-items: center;">
               <span style="font-family: quantico">Credit+</span>
            </div>
          </div>
        </div>
        <p v-if="investpro" style="font-family: roboto; font-weight: 300; margin-top: 30px">
          <b>Pros:</b> Exclusive, secure, and focused on advanced financial needs. Perfect for large transactions.
          <br><br>
          <b>Cons:</b> Expensive and not very useful for everyday purchases.
        </p>
        <p v-if="flexcard" style="font-family: roboto; font-weight: 300; margin-top: 30px">
          <b>Pros:</b> Flexible, easy to use and accessible to everyone. Ideal for controlling daily expenses.
          <br><br>
          <b>Cons:</b> Few rewards and balance limits.
        </p>
        <p v-if="mediaplus" style="font-family: roboto; font-weight: 300; margin-top: 30px">
          <b>Pros:</b> Perfect for payments on entertainment platforms, with possible exclusive promotions.
          <br><br>
          <b>Cons:</b> Limited use outside of streaming services and possible monthly costs.
        </p>
        <p v-if="creditplus" style="font-family: roboto; font-weight: 300; margin-top: 30px">
          <b>Pros:</b> Ideal for large purchases, with access to flexible financing and attractive rewards programs.
          <br><br>
          <b>Cons:</b> Can generate high interest rates if not paid on time and requires a good credit history for approval.
        </p>
        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/credit_card_gear_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Card Type
                    </span>
                    <select class="select" id="currency" v-model="input2">
                        <option disabled value="">Select</option>
                        <option v-for="plan in plansList" :key="plan" :value="plan">
                            {{ plan }}
                        </option>
                    </select>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <div v-if="selectedColor == '#ffec99'" style="width: 15px; height: 15px; border-radius: 50%; background: #ffec99; margin-right: 10px">
                        </div>

                        <div v-if="selectedColor == '#b2f2bb'" style="width: 15px; height: 15px; border-radius: 50%; background: #b2f2bb; margin-right: 10px">
                        </div>

                        <div v-if="selectedColor == '#a5d8ff'" style="width: 15px; height: 15px; border-radius: 50%; background: #a5d8ff; margin-right: 10px">
                        </div>
                        Color
                    </span>
                    <select class="select" id="currency" v-model="selectedColor">
                        <option disabled value="">Select</option>
                        <option v-for="color in colorsList" :key="color" :value="color">
                            {{ color }}
                        </option>
                    </select>
                </div>
            </div>
            <button @click="createCard" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>




    <div v-if="selecting" class="bar">

    </div>

      <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>

















<div v-if="assets" class="transfer-main">
      <div class="left2">
        <h1>Assets Buy</h1>
        <div class="row1-transfer">
            <div class="account-selector-transfer">
            <h3>Selected Account</h3>
            <div v-for="account in accounts" :key="account.name" >
                <div v-if="account.active.value" class="transfer-selected-account" style="display: flex;">
                    <div style="display: flex; margin-left: 10px; margin-right: 20px;">
                        <img
                            src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                            alt=""
                            style="margin-right: 10px;"
                        />
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name  }}</p>
                    </div>
                    <button @click="activateWindow" class="changer">Change</button>
            </div>
            </div>
          </div>

          <div class="balance-container">
            <h2>Balance</h2>
            <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; align-items: center;"> {{ balance }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
          </div>

        </div>

        <div class="inputs-transfer">
            <div class="money-inputs">
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/paid_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Quantity
                    </span>
                    <input v-model="input2"  style="color: #09b96d; font-family: quantico; font-weight: 600 !important" type="number" min="0" @change="check, calculatedPrice()"/>
                </div>
                <div class="input-trans money">
                    <span style="display: flex; align-items: center;">
                         <img
                            v-if="selectedAsset == 'AAPL'"
                            src="public/Apple_logo_black copy.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'GOOGL'"
                            src="public/Google__G__logo.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'TSLA'"
                            src="public/tesla-svgrepo-com.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'AMZN'"
                            src="public/Amazon_icon.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'MSFT'"
                            src="public/Microsoft_logo.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'NFLX'"
                            src="public/netflix-1-logo-svgrepo-com.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'FB'"
                            src="public/meta-icon.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'BTC'"
                            src="public/Bitcoin.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'ETH'"
                            src="public/ethereum-eth.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'XRP'"
                            src="public/xrp-svgrepo-com.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'GOLD'"
                            src="public/gold-ingot-gold-svgrepo-com.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                            <img
                            v-if="selectedAsset == 'SILVER'"
                            src="public/silver-icon.svg"
                            alt=""
                            width="15px"
                            style="margin-right: 10px; fill: #fffcff !important"
                            />
                        Asset
                    </span>
                    <select class="select" id="currency" v-model="selectedAsset">
                        <option disabled value="">Selecciona una divisa</option>
                        <option v-for="asset in assetsList" :key="asset" :value="asset">
                            {{ asset }}
                        </option>
                    </select>
                </div>
            </div>
            <div>
                <h3 style="font-family: roboto;">Calculated Cost:</h3>
                <span style="font-family: quantico; color: #09b96d; font-weight: 600; display: flex; justify-content: flex-end; margin-right: 20px; font-size: 22px"> {{ parseFloat(calculatedCost).toFixed(2) }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                <span style="font-family: quantico; color: #161d2c; font-weight: 600; display: flex; justify-content: flex-end; margin-right: 30px; font-size: 10px">*price at {{ hour  }}</span>
            </div>
            <button @click="buyAsset" id="sender-transfer">
                Confirm
            </button>
        </div>

      </div>


    <div v-if="showAssets" class="bar">

    </div>

    <div v-if="showAssets" class="left selecting">
        <h1>Owned Assets</h1>
        <div class="selections-wrapper assets-carrousel" style="
            overflow: hidden;
              overflow-y: auto;
              max-height: 80vh !important;
              height: 80vh;">
            <div  v-for="[key, value] in Object.entries(wallet)"
            :key="key" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border-bottom: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img
                  v-if="key == 'AAPL'"
                  src="public/Apple_logo_black copy.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'GOOGL'"
                  src="public/Google__G__logo.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'TSLA'"
                  src="public/tesla-svgrepo-com.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'AMZN'"
                  src="public/Amazon_icon.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'MSFT'"
                  src="public/Microsoft_logo.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'NFLX'"
                  src="public/netflix-1-logo-svgrepo-com.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'FB'"
                  src="public/meta-icon.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'BTC'"
                  src="public/Bitcoin.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'ETH'"
                  src="public/ethereum-eth.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'XRP'"
                  src="public/svgviewer-output.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'GOLD'"
                  src="public/gold-ingot-gold-svgrepo-com.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                <img
                  v-if="key == 'SILVER'"
                  src="public/silver-icon.svg"
                  alt=""
                  width="15px"
                  style="margin-right: 10px; fill: #fffcff !important"
                />
                        <p style="font-family: roboto; font-weight: 500; width: 10px;">{{ key  }}</p>
                    </div>
                    <div style="display: flex; justify-content: center; width: 200px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ parseFloat(value.Quantity_Owned ).toFixed(8)}}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">                  {{ parseFloat(value.Profit).toFixed(2) }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <span style="font-family: quantico; color: #161d2c; font-weight: 600; display: flex; justify-content: flex-end; margin-right: 30px; font-size: 10px">*price at {{ hour  }}</span>
        </div>



    <div v-if="selecting" class="bar">

    </div>

      <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>















    <div v-if="settings" class="transfer-main">
      <div class="left2">
        <div class="inputs-transfer" style="margin-top: 20px;">
            <div class="input-trans" style="margin-bottom: 20px">
                <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/person_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Full Name
                    </span>
                <input v-model="input1" style="font-style: italic;" type="text" placeholder="Introduce" />
            </div>
            <div class="input-trans">
                <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/call_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Phone Number
                    </span>
                <input v-model="input2" type="text" placeholder="Introduce" />
            </div>
            <button @click="updateData()" id="sender-transfer">
                Change
            </button>
        </div>
        <h2 style="font-family: roboto; font-weight: 500; margin-left: 20px; margin-top: 30px;">GOPHER</h2>
        <div class="assets-carrousel" style="margin-left: 20px; display: flex; flex-wrap: wrap; justify-content: space-between; align-items: center; overflow: hidden;
              overflow-y: auto;
              max-height:25vh !important;
              height: 25vh;">
              <div v-for="gopher in gopherList" :key="gopher" >
                <img v-if="gopher.color == selectedGopher" class="smallGoph" style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 60px; margin: 10px; border-color: #1b76ff!important;" :src="gopher.small" alt="">
                <img v-if="gopher.color == 'LightRed'  && !(gopher.selected.value == true)" @click="selectRed"  class="smallGoph" style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 60px; margin: 10px; " :src="gopher.small" alt="">
                <img v-if="gopher.color == 'LightBlue'  && !(gopher.selected.value == true)" @click="selectLightBlue"  class="smallGoph" style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 60px; margin: 10px; " :src="gopher.small" alt="">
                <img v-if="gopher.color == 'LightBrown' && !(gopher.selected.value == true)" @click="selectLightBrown"  class="smallGoph" style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 60px; margin: 10px; " :src="gopher.small" alt="">
                <img v-if="gopher.color == 'Purple'  && !(gopher.selected.value == true)" @click="selectPurple"  class="smallGoph" style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 60px; margin: 10px; " :src="gopher.small" alt="">
                <img v-if="gopher.color == 'LightYellow'  && !(gopher.selected.value == true)" @click="selectLightYellow"  class="smallGoph" style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 60px; margin: 10px; " :src="gopher.small" alt="">
              </div>
        </div>

      </div>


    <div v-if="settings" class="bar">

    </div>

    <div v-if="settings" class="left selecting">
        <h1>Details</h1>
        <div style=" display: flex; flex-direction: column; align-items: center;">
            <img style="border: 2px solid #161d2c; padding: 20px 50px; border-radius: 50%; width: 150px; margin: 7px; background: #fffcff"  :src="smallPic" alt="" />
            <h1 style="font-family: roboto">{{ name  }}</h1>
            <h3 style="font-family: roboto; font-weight: 400; margin-top: 0;">{{ email  }}</h3>
            <h3 style="font-family: roboto; font-weight: 400; margin-top: 0;">{{ phoneNumber  }}</h3>
            <h2 style="font-family: quantico; font-size: 18px;">{{ userNUMBER }}</h2>
        </div>
    </div>



    <div v-if="selecting" class="bar">

    </div>

      <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>








    <div v-if="persons" class="transfer-main">
      <div class="left2">
        <div class="inputs-transfer" style="margin-top: 20px;">
            <div class="input-trans" style="margin-bottom: 20px">
                <span style="display: flex; align-items: center; font-size: 20px;">
                        <img style="margin-right: 10px; padding: 0;" src="public/person_search_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Add People
                    </span>
                <input v-model="input1" style="font-style: italic;" type="text" placeholder="Introduce" />            <button @click="searchUser()" id="sender-transfer" style="padding: 5px 0">
                                Search
                             </button>
            </div>
            <div class="input-trans">
                <span style="display: flex; align-items: center;">
                        <img style="margin-right: 10px; padding: 0;" src="public/tag_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                        Send my Code!
                    </span>
                <span>
                    <h2 style="font-family: quantico; font-weight: 600; font-size: 18px; background: #fffddf; padding: 20px; border: 1px solid #161d2c;">{{ userNUMBER }}</h2>
                </span>
                <button class="share-options"  @click="copy()" id="sender-transfer" style="font-family: roboto; padding: 15px 0; border-radius: 0; font-weight: 400; background: #ffec99; color: #161d2c;display: flex; justify-content: center;">
                  <img style="margin-right: 5px;" src="public/content_copy_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                                    Copy
                </button>
                <button class="share-options"  @click="emailSend()" id="sender-transfer" style="font-family: roboto; padding: 15px 0; border-radius: 0;font-weight: 400; background: #a5d8ff; color: #161d2c;display: flex; justify-content: center;">
                  <img style="margin-right: 5px;" src="public/mail_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                                Email
                </button>
                <button @click="qr()" id="sender-transfer" style="font-family: roboto; padding: 15px 0; border-radius: 0;font-weight: 400; background: #000; display: flex; justify-content: center;">
                  <img style="margin-right: 5px;" src="public/qr_code_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                                QR
                </button>
                <button class="share-options" @click="Whatsapp()" id="sender-transfer" style="font-family: roboto; padding: 15px 0; border-radius: 0;font-weight: 400; background: #b2f2bb; color: #161d2c;display: flex; justify-content: center;">
                  <img style="margin-right: 5px;" src="public/chat_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="">
                                Whatsapp
                </button>
            </div>
        </div>


      </div>


    <div v-if="persons" class="bar">

    </div>

    <div v-if="persons && finded == true" class="left selecting">
        <h1>Person Finded</h1>
        <div style=" display: flex; flex-direction: column; align-items: center;">
            <img style="border: 2px solid #161d2c; padding: 20px 50px; border-radius: 50%; width: 150px; margin: 7px; background: #fffcff"  :src="findedUser.small.value" alt="" />
            <h1 style="font-family: roboto">{{ findedUser.name.value  }}</h1>
        </div>
        <button v-if="!sended && isfriend(findedUser.number.value)" class="requester" id="sender-transfer" style="padding: 15px 0; font-family: quantico; font-weight: 400; background: #09b96d !important; color: #fffcff">
                                Already Friend
        </button>
        <button v-if="!sended && !isfriend(findedUser.number.value)" class="requester" @click="sendFriendRequest()" id="sender-transfer" style="padding: 15px 0; font-family: roboto; font-weight: 400; background: #000;">
                                Send Request
        </button>
        <button v-if="sended" class="requester" @click="sendFriendRequest()" id="sender-transfer" style="padding: 15px 0; font-family: roboto; font-weight: 400; background: #1b76ff;">
                                Request sended
        </button>
    </div>

    <div style=" display: flex; justify-content: center; align-items: center;"  v-if="persons && finded == false" class="left selecting">
        <img width="480vw" src="public/error.svg" alt="">
    </div>









    <div v-if="selecting" class="bar">

    </div>

      <div v-if="selecting" class="left selecting">
        <h1>Select Account</h1>
        <div class="selections-wrapper">
            <div  :class="paint()" style="display: flex; justify-content: space-between; align-items: center; font-size: 20px;border: 2px solid #161d2c; padding: 20px; margin-bottom: 20px;">
                    <div style="display: flex; align-items: center;">
                        <img src="public/account_balance_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt="" style="margin-right: 10px;">
                        <p style="font-family: roboto; font-weight: 500;">{{ account.name.value }}</p>
                    </div>
                    <span style="display: flex; align-items: center; color: #09b96d; font-family: quantico; font-weight: 600;">1559.95<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                </div>
            </div>
            <button @click="activateWindow" id="sender-transfer2">
                Close
            </button>
        </div>
    </div>











    <div v-if="history" class="transfer-main">
      <div v-if="!showingDetails" class="left3">
        <h1>Transaction History</h1>
        <div style="
            margin-top: 0;
            padding-top: 0;
            overflow: hidden;
              overflow-y: auto;
              max-height: 80vh !important;
              height: 80vh;
        " class="assets-carrousel">
            <div v-for="item in transfers" :key="item.ID" style="font-family: roboto;">
            <div style="display: flex; margin: 10px; border-bottom: 2px solid #161d2c; align-items: center; justify-content: space-between;">
                <div style="display: flex; width: 50px;">
                    <img
                    v-if="item.TransactionType == 'CASH_DEPOSIT'"
                    src="public/payments_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                  />
                  <img
                    v-if="item.TransactionType == 'CASH_WITHDRAW'"
                    src="public/money_bag_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                  />
                  <img
                    v-if="item.TransactionType == 'ASSETS_BUY'"
                    src="public/finance_mode_24dp_E8EAED_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                  />
                  <img
                    v-if="item.TransactionType == 'CASH_TRANSFER'"
                    src="public/send_money_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                    />
                    <img
                    v-if="item.TransactionType == 'CARD_DEPOSIT' || item.TransactionType == 'CARD_WITHDRAW' || item.TransactionType == 'CARD_TO_ACCOUNT'"
                    src="public/credit_card_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg"
                    alt=""
                    />
                    <div style="margin-left: 10px; ">
                        <h3 style="font-weight: 400;">{{ item.TransactionType  }}</h3>
                    </div>
                </div>
                    <h4 style="font-weight: 300; width: 50px; display: flex; justify-content: center;">{{ item.Sender  }}</h4>
                    <span style="width: 50px; display: flex; justify-content: center;">{{ date }}</span>
                    <span  style="width: 50px; display: flex; justify-content: center;" >{{ hour }}</span>

                    <span style="font-family: quantico; color: #09b96d; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CARD_DEPOSIT'"> + {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>


                    <span style="font-family: quantico; color: #fc090f; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CARD_WITHDRAW'"> - {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg" alt=""></span>

                    <span style="font-family: quantico; color: #09b96d; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CARD_TO_ACCOUNT'"> {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>

                    <span style="font-family: quantico; color: #09b96d; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CASH_DEPOSIT'"> + {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>


                    <span style="font-family: quantico; color: #09b96d; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CASH_TRANSFER' && item.To == account.accountNumber.value"> + {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>

                    <span style="font-family: quantico; color: #fc090f; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CASH_TRANSFER' && item.From == account.accountNumber.value &&  !(item.From == account.accountNumber.value && item.To == account.accountNumber.value)"> - {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg" alt=""></span>


                    <span style="font-family: quantico; color: #fc090f; font-weight: 500; font-size: 18px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="!(item.TransactionType == 'ASSETS_BUY') && item.TransactionType == 'CASH_WITHDRAW'"> - {{  parseFloat(item.quantity).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg" alt=""></span>


                    <span style="font-family: quantico; color: #fc090f; font-weight: 500; font-size: 20px; display: flex; justify-content: center; width: 150px; align-items: center; " v-if="item.TransactionType == 'ASSETS_BUY'"> - {{  parseFloat(item.Cost).toFixed(2) }} <img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg" alt=""></span>
                    <button @click="showTransfer(item.ID)"  class="changer">Details</button>
            </div>
        </div>
        </div>
      </div>



      <div v-if="showingDetails && selectedTransfer.TransactionType == 'CASH_TRANSFER'" class="left3">
        <div style="display: flex; justify-content: space-between;">
          <h1 style="font-size: 35px;">{{ selectedTransfer.TransactionType }} Details</h1>
          <button class="closer" @click="closeTransfer()" style="height: 30px; padding: 30px; background: #fc090f; color: #fffcff; font-weight: 600; font-family: quantico; border: none; border-radius: 30px; display: flex; align-items: center; font-size: 15px;">Close</button>
        </div>
        <div style="display: flex; align-items: center; font-family: roboto; flex-direction: column;">
          <div style="display: flex; flex-direction: column;">
            <span style="font-weight: 500">ID</span>
            <span style="border: 1px solid #020514; padding: 15px; background: #b2f2bb">{{  selectedTransfer.ID }}</span>
          </div>
          <div style="margin-top: 40px; display: flex; align-items: center; font-family: roboto;">
            <div style="display: flex; flex-direction: column; align-items: center; margin-right: 30px;">
              <h2>FROM</h2>
              <span style="text-decoration: underline; font-style: italic">{{  selectedTransfer.From }}</span>
            </div>
            <div style="display: flex; align-items: center; font-family: roboto;">
                <div style=" display: flex;flex-direction: column; align-items: center;">
                    <span style="font-size: 12px; margin-bottom: 10px;">{{ selectedTransfer.Date  }}</span>
                    <img
                    src="public/arrow.svg"/>
                </div>
                <div style="display: flex; flex-direction: column; align-items: center;">
                    <h2>TO</h2>
                    <span style="text-decoration: underline; font-style: italic">{{  selectedTransfer.To }}</span>
                </div>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex;">
              <div style="margin-right: 10px; display: flex; align-items: center;">
                <h3 style="margin-right: 10px;">Quantity: </h3>
                <span style="font-family: quantico; font-size: 20px; color: #09b96d; font-weight: 600; display: flex;">{{ selectedTransfer.quantity  }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
              </div>
              <div style="display: flex; align-items: center;">
                <h3 style="margin-right: 10px">Currency: </h3>
                <span style="font-family: quantico; font-size: 20px" >{{ selectedTransfer.coin  }}</span>
              </div>
            </div>
            <div style="margin-top: 40px; display: flex;  width: 50vw; justify-content: center; font-family: quantico; font-size: 20px;">
              <p>"{{ selectedTransfer.Description  }}"</p>
            </div>
        </div>
      </div>



      <div v-if="showingDetails && selectedTransfer.TransactionType == 'CASH_DEPOSIT'" class="left3">
        <div style="display: flex; justify-content: space-between;">
          <h1 style="font-size: 35px;">{{ selectedTransfer.TransactionType }} Details</h1>
          <button class="closer" @click="closeTransfer()" style="height: 30px; padding: 30px; background: #fc090f; color: #fffcff; font-weight: 600; font-family: quantico; border: none; border-radius: 30px; display: flex; align-items: center; font-size: 15px;">Close</button>
        </div>
        <div style="display: flex; align-items: center; font-family: roboto; flex-direction: column;">
          <div style="display: flex; align-items: center;">
            <div style="display: flex; flex-direction: column;">
              <span style="font-weight: 500">ID</span>
              <span style="border: 1px solid #020514; padding: 15px; background: #b2f2bb">{{  selectedTransfer.ID }}</span>
            </div>
            <div style="display: flex; flex-direction: column; margin-left: 20px">
              <span style="font-weight: 500">DATE</span>
              <span style="border: 1px solid #020514; padding: 15px; background: #ffec99">{{ selectedTransfer.Date  }}</span>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex; align-items: center; font-family: roboto;">
            <div style="display: flex; flex-direction: column; align-items: center; margin-right: 30px;">
              <h2>{{ name  }}</h2>
              <img style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 80px; margin: 7px; background: #fffcff; margin-bottom: 20px;"  :src="smallPic" width="50px" alt="" />
              <span style="font-style: italic; font-family: quantico; text-decoration: underline;">{{  selectedTransfer.From }}</span>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex;">
              <div style="margin-right: 10px; display: flex; align-items: center;">
                <h3 style="margin-right: 10px;">Quantity: </h3>
                <span style="font-family: quantico; font-size: 20px; color: #09b96d; font-weight: 600; display: flex;">{{ selectedTransfer.quantity  }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
              </div>
              <div style="display: flex; align-items: center;">
                <h3 style="margin-right: 10px">Currency: </h3>
                <span style="font-family: quantico; font-size: 20px" >{{ selectedTransfer.coin  }}</span>
              </div>
            </div>
        </div>
      </div>


      <div v-if="showingDetails && selectedTransfer.TransactionType == 'CASH_WITHDRAW'" class="left3">
        <div style="display: flex; justify-content: space-between;">
          <h1 style="font-size: 35px;">{{ selectedTransfer.TransactionType }} Details</h1>
          <button class="closer" @click="closeTransfer()" style="height: 30px; padding: 30px; background: #fc090f; color: #fffcff; font-weight: 600; font-family: quantico; border: none; border-radius: 30px; display: flex; align-items: center; font-size: 15px;">Close</button>
        </div>
        <div style="display: flex; align-items: center; font-family: roboto; flex-direction: column;">
          <div style="display: flex; align-items: center;">
            <div style="display: flex; flex-direction: column;">
              <span style="font-weight: 500">ID</span>
              <span style="border: 1px solid #020514; padding: 15px; background: #b2f2bb;">{{  selectedTransfer.ID }}</span>
            </div>
            <div style="display: flex; flex-direction: column; margin-left: 20px">
              <span style="font-weight: 500">DATE</span>
              <span style="border: 1px solid #020514; padding: 15px; background: #ffec99">{{ selectedTransfer.Date  }}</span>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex; align-items: center; font-family: roboto;">
            <div style="display: flex; flex-direction: column; align-items: center; margin: 0 !important;">
              <h2>{{ name  }}</h2>
              <img style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 80px; margin: 7px; background: #fffcff; margin-bottom: 20px;"  :src="smallPic" width="50px" alt="" />
              <span style="font-style: italic; font-family: quantico; text-decoration: underline;">{{  selectedTransfer.From }}</span>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex;">
              <div style="margin-right: 10px; display: flex; align-items: center;">
                <h3 style="margin-right: 10px;">Quantity: </h3>
                <span style="font-family: quantico; font-size: 20px; color: #fc090f; font-weight: 600; display: flex;">-{{ selectedTransfer.quantity  }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg" alt=""></span>
              </div>
              <div style="display: flex; align-items: center;">
                <h3 style="margin-right: 10px">Currency: </h3>
                <span style="font-family: quantico; font-size: 20px" >{{ selectedTransfer.coin  }}</span>
              </div>
            </div>
        </div>
      </div>

      <div v-if="showingDetails && selectedTransfer.TransactionType == 'ASSETS_BUY'" class="left3">
        <div style="display: flex; justify-content: space-between;">
          <h1 style="font-size: 35px;     margin-top: 10px; font-size: 50px; font-family: DM Serif Text, serif;
          font-weight: lighter;font-style: italic;">{{ selectedTransfer.TransactionType }} Details</h1>
          <button class="closer" @click="closeTransfer()" style="height: 30px; padding: 30px; background: #fc090f; color: #fffcff; font-weight: 600; font-family: quantico; border: none; border-radius: 30px; display: flex; align-items: center; font-size: 15px;">Close</button>
        </div>
        <div style="display: flex; align-items: center; font-family: roboto; flex-direction: column;">
          <div style="display: flex; align-items: center;">
            <div style="display: flex; flex-direction: column;">
              <span style="font-weight: 500">ID</span>
              <span style="border: 1px solid #020514; padding: 15px; background: #b2f2bb">{{  selectedTransfer.ID }}</span>
            </div>

          </div>
          <div style="margin-top: 40px; display: flex; align-items: center; font-family: roboto;">
            <div style="display: flex; flex-direction: column; align-items: center; margin-right: 30px;">
              <h2>{{ name  }}</h2>
              <img style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 80px; margin: 7px; background: #fffcff; margin-bottom: 20px;"  :src="smallPic" width="50px" alt="" />
              <span style="font-style: italic; font-family: quantico; text-decoration: underline;">{{  selectedTransfer.From }}</span>
            </div>
            <div style=" display: flex;flex-direction: column; align-items: center;">
                    <span style="font-size: 12px; margin-bottom: 10px;">{{ selectedTransfer.Date  }}</span>
                    <img
                    src="public/arrow.svg"/>
            </div>
            <div style="display: flex; flex-direction: column; align-items: center; margin-right: 30px; margin-left: 60px">
              <h2>{{ selectedTransfer.coin  }}</h2>
              <img
                      v-if="selectedTransfer.coin  == 'AAPL'"
                      src="public/Apple_logo_black copy.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'GOOGL'"
                      src="public/Google__G__logo.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'TSLA'"
                      src="public/tesla-svgrepo-com.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'AMZN'"
                      src="public/Amazon_icon.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'MSFT'"
                      src="public/Microsoft_logo.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'NFLX'"
                      src="public/netflix-1-logo-svgrepo-com.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'FB'"
                      src="public/meta-icon.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'BTC'"
                      src="public/Bitcoin.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'ETH'"
                      src="public/ethereum-eth.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'XRP'"
                      src="public/xrp-svgrepo-com.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'GOLD'"
                      src="public/gold-ingot-gold-svgrepo-com.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <img
                      v-if="selectedTransfer.coin  == 'SILVER'"
                      src="public/silver-icon.svg"
                      alt=""
                      width="120px"
                      style="margin-right: 10px; fill: #fffcff !important; margin-right: 10px; fill: #fffcff !important"
                    />
                    <div style="margin-top: 20px; display: flex;align-items: center;">
                      <span style="font-family: roboto; font-size: 25px; font-weight: 500; margin-right: 10px">Price: </span>
                      <span style="font-style: italic; font-family: quantico; font-size: 25px; font-weight: 500; display: flex;align-items: center; color: #09b96d; font-weight: 600;">{{  selectedTransfer.Price }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy.svg" alt=""></span>
                    </div>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex; width: 400px; justify-content: space-between;">
              <div style="margin-right: 10px; display: flex; align-items: center;">
                <h3 style="margin-right: 10px; font-family: roboto; font-size: 25px; font-weight: 500">Quantity: </h3>
                <span style="display: flex; font-style: italic; font-family: quantico; font-size: 25px !important; font-weight: 500; display: flex;align-items: center;  font-weight: 500">{{ parseFloat(selectedTransfer.quantity).toFixed(8)  }}</span>
              </div>
              <div style="display: flex; align-items: center;">
                <h3 style="margin-right: 10px; font-family: roboto; font-size: 25px; font-weight: 500">Cost: </h3>
                <span style="font-style: italic; font-family: quantico; font-size: 25px; font-weight: 500; display: flex;align-items: center; color: #fc090f; font-weight: 600;" >-{{ selectedTransfer.Cost  }}<img style="margin-right: 10px; padding: 0;" src="public/euro_symbol_24dp_000000_FILL0_wght400_GRAD0_opsz24 copy 2.svg" alt=""></span>
              </div>
            </div>
        </div>
      </div>


      <div v-if="showingDetails && selectedTransfer.TransactionType == 'CARD_DEPOSIT'" class="left3">
        <div style="display: flex; justify-content: space-between;">
          <h1 style="font-size: 35px;     margin-top: 10px; font-size: 50px; font-family: DM Serif Text, serif;
          font-weight: lighter;font-style: italic;">{{ selectedTransfer.TransactionType }} Details</h1>
          <button class="closer" @click="closeTransfer()" style="height: 30px; padding: 30px; background: #fc090f; color: #fffcff; font-weight: 600; font-family: quantico; border: none; border-radius: 30px; display: flex; align-items: center; font-size: 15px;">Close</button>
        </div>
        <div style="display: flex; align-items: center; font-family: roboto; flex-direction: column;">
          <div style="display: flex; align-items: center;">
            <div style="display: flex; flex-direction: column;">
              <span style="font-weight: 500">ID</span>
              <span style="border: 1px solid #020514; padding: 15px; background: #b2f2bb">{{  selectedTransfer.ID }}</span>
            </div>

          </div>
          <div style="margin-top: 40px; display: flex; align-items: center; font-family: roboto;">
            <div style="display: flex; flex-direction: column; align-items: center; margin-right: 30px;">
              <h2>{{ name  }}</h2>
              <img style="border: 2px solid #161d2c; padding: 10px 25px; border-radius: 50%; width: 80px; margin: 7px; background: #fffcff; margin-bottom: 20px;"  :src="smallPic" width="50px" alt="" />
              <span style="font-style: italic; font-family: quantico; text-decoration: underline;">{{  selectedTransfer.From }}</span>
            </div>
            <div style=" display: flex;flex-direction: column; align-items: center;">
                    <span style="font-size: 12px; margin-bottom: 10px;">{{ selectedTransfer.Date  }}</span>
                    <img
                    src="public/arrow.svg"/>
            </div>
            <div style="display: flex; flex-direction: column; align-items: center; margin-right: 30px; margin-left: 60px">
              <div @mouseover="activateFlexCard()" class="card2" :style="{background: selectedTransfer ? selectedTransfer.CardColor : '#ffffff', color: '#020514', width: '100px', height: '60px', borderRadius: '13px', display: 'flex', justifyContent: 'center', alignItems: 'center'}">
              <span style="font-family: Lexend Exa">{{ selectedTransfer.CardName  }}</span>
            </div>
            </div>
          </div>
          <div style="margin-top: 40px; display: flex; width: 400px; justify-content: center;  width: 100%;">
              <div style="margin-right: 10px; display: flex; align-items: center; justify-content: center">
                <h3 style="margin-right: 10px; font-family: roboto; font-size: 25px; font-weight: 500">Quantity: </h3>
                <span style="display: flex; font-style: italic; font-family: quantico; font-size: 25px !important; font-weight: 500; display: flex;align-items: center;  font-weight: 500; color: #09b96d">{{ parseFloat(selectedTransfer.quantity).toFixed(2)  }}</span>
              </div>
            </div>
        </div>
      </div>

    </div>








    <div v-if="visible" class="confirmed" :class="{ 'slide-in': visible, 'slide-out': !visible }" style="position: fixed; bottom: 30px; right: 30px; background: #b2f2bb; display: flex; font-family: quantico; font-size: 9px; padding: 10px; align-items: center; border: 1px solid #161d2c;">
        <h1 style="margin-right: 20px; display: flex;"><img style="margin-right: 10px" src="public/credit_score_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt=""> Operation Completed</h1>
        <div class="bar2">
        </div>
        <h2>{{ hour  }}</h2>
    </div>

    <div v-if="alert" class="confirmed" :class="{ 'slide-in': visible, 'slide-out': !visible }" style="position: fixed; bottom: 30px; right: 30px; background: #ffc9c9; display: flex; font-family: quantico; font-size: 9px; padding: 10px; align-items: center; border: 1px solid #161d2c;">
        <h1 style="margin-right: 20px; display: flex;"><img style="margin-right: 10px" src="public/warning_24dp_000000_FILL0_wght400_GRAD0_opsz24.svg" alt=""> Error Processing Request</h1>
        <div class="bar2">
        </div>
        <h2>{{ hour  }}</h2>
    </div>

    <div v-if="processing" class="confirmed" :class="{ 'slide-in': visible, 'slide-out': !visible }" style="position: fixed; bottom: 30px; right: 30px; background: #ffec99; display: flex; font-family: quantico; font-size: 9px; padding: 10px; align-items: center; border: 1px solid #161d2c;">
        <h1 style="margin-right: 20px; display: flex;"><img style="margin-right: 10px" src="public/hourglass_top_24dp_000000_FILL0_wght400_GRAD0_opsz24 (1).svg" alt="">Processing Operation</h1>
        <div class="bar2">
        </div>
        <h2>{{ hour  }}</h2>
    </div>
















    <div v-if="desplegable"  class="desplegable">
        <div  class="options" style="display: flex; flex-direction: column; align-items: center; position: fixed; top: 130px; right: 20px; background: #020514; border: 1px solid #161d2c; border-radius: 10px; padding: 10px;">
            <button @click="activarSettings" class="share-options" style="padding: 10px 10px; background: #1b76ff; color: #fffcff; font-family: quantico; border: none;
            border-radius: 5px; margin: 3px">Settings</button>
            <button @click="logOut" class="share-options" style="padding: 10px 10px; background: #fc090f; color: #fffcff; font-family: quantico; border: none;
            border-radius: 5px; margin: 3px">Log-out</button>
        </div>
    </div>





    <div v-if="showNotis" class="confirmed" style="position: fixed; top: 130px; right: 20px; background: #020514; display: flex; font-family: quantico; font-size: 9px; padding: 10px; align-items: center; border: 1px solid #161d2c; color: #fffcff; border-radius: 10px; flex-direction: column;">
        <div v-for="request in resolvedRequestList" :key="request.number" style="display: flex;align-items: center; border-bottom: 1px solid #fffcff;">
            <div style="  flex-direction: column; align-items: center;">
                <img style="border: 2px solid #161d2c; padding: 5px 15px; border-radius: 50%; width: 40px; margin: 7px; background: #fffcff; margin-right: 20px"  :src="request.small" alt=""/>
            </div>
            <div>
                <h1 style="font-family: roboto; font-weight: 400">{{ request.name  }}</h1>
                <div>
                    <button @click="acceptRequest(request.number)" class="accepters"  style="padding: 10px 10px; background: #1b76ff; color: #fffcff; font-family: quantico; border: none;
                    border-radius: 5px; margin: 3px">Accept</button>
                     <button class="accepters" style="padding: 10px 10px; background: #fc090f; color: #fffcff; font-family: quantico; border: none;
                    border-radius: 5px; margin: 3px">Reject</button>
                </div>
            </div>
        </div>
    </div>

    </div>
</template>
<style>
@import url("https://fonts.googleapis.com/css2?family=DM+Serif+Text:ital@0;1&family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&family=Lilita+One&family=Noto+Sans+JP:wght@100..900&family=Quantico:ital,wght@0,400;0,700;1,400;1,700&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Lexend+Exa:wght@100..900&family=Source+Serif+4:ital,opsz,wght@0,8..60,200..900;1,8..60,200..900&display=swap');

.card-buttons:hover {
    cursor: pointer;
    transition: all 0.2s;
    background: #000 !important;
}

.card2 {
  transition: transform 0.3s ease, background-color 0.8s ease, box-shadow 0.3s ease; /* Combina todas las transiciones en una sola */
  transform-origin: center; /* Define el punto de rotación */
}

.card2:hover {
    cursor: pointer;
    transition: all 0.1s;
    transform: scale(1.03) rotateX(5deg) rotateY(-10deg); /* Escala + rotación */
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.chevron:hover{
    cursor: pointer;
    transition: all 0.2s;
    transform: scale(1.3);
}

.profile-pic:hover {
    cursor: pointer;
    transition: all 0.2s;
    transform: scale(1.1);
}

.closer:hover {
    cursor: pointer;
    transition: all 0.2s;
    background: #000 !important;
}


.accepters:hover {
    cursor: pointer;
    transition: all 0.2s;
    background: #000 !important;
}

.requester:hover {
    cursor: pointer;
    color: #fffcff;
    transition: all 0.2s;
}

.share-options:hover {
    color: #fffcff !important;
    background: #000 !important;
}


.smallGoph:hover {
    cursor: pointer;
    transition: all 0.2s;
    transform: scale(1.1);
    border-color: #1b76ff!important;
}

#sender-transfer2 {
    font-size: 22px;
    padding: 20px;
    margin-top: 20px;
    width: 100%;
    background: #020514;
    border: 1px solid #020514;
    border-radius: 10px;
    color: #fffcff;
    font-family: "DM Serif Text", serif;
    font-weight: lighter;
    font-style: italic;
}

#sender-transfer2:hover {
    cursor: pointer;
    text-decoration: underline;
    transition: all 0.2s;
}

.bar2 {
    height: 40px;
    padding: 1px;
    background: #020514;
    margin-right: 10px;
}

.selected {
    background: #f6ef68 !important;
}

.selecting {
    width: 43vw !important;
}

.selection:hover {
    cursor: pointer;
    background: #f6ef68;
    transition: all 0.2s;
}

.bar {
    width: 2px;
    margin-top: 30px;
    height: 93%;
    background: #020514;
    margin-right: 30px;
    margin-left: 90px;
}

.transfer-main {
    display: flex;
    justify-content: space-between;
    margin-right: 30px;
}

html {
    scroll-behavior: smooth;
}

input:focus {
    outline: none; /* Elimina el borde azul de enfoque */
    box-shadow: none; /* Elimina cualquier sombra que pueda añadirse */
}

.select {
    padding: 18px;
    border: 1px solid ;
    margin-top: 10px;
    border-radius: 10px;
    font-size: 15px;
    border: 1px solid #020514;
}

#sender-transfer {
    font-size: 22px;
    padding: 20px;
    margin-top: 20px;
    width: 100%;
    background: #1b76ff;
    border: 1px solid #020514;
    border-radius: 10px;
    color: #fffcff;
    font-family: "DM Serif Text", serif;
    font-weight: lighter;
    font-style: italic;
}

#sender-transfer:hover {
    cursor: pointer;
    background: #020514 !important;
    transition: all 0.2s;
}

.inputs-transfer {
    margin-top: 30px;
}

.money {
    width: 40%;
}

.money-inputs {
    display: flex;
    justify-content: space-between;
    padding: 20px;
}

.input-trans {
    display: flex;
    flex-direction: column;
}

.input-trans input {
    border: 1px solid #020514;
    padding: 17px;
    margin-top: 10px;
    border-radius: 10px;
    font-size: 18px;
}

.input-trans span {
    font-size: 18px;
    font-family: "Roboto", sans-serif;
    font-weight: 500;
    margin-bottom: 10px;
}

.balance-container h2 {
    font-size: 22px;
    font-family: "Roboto", sans-serif;
    font-weight: 500;
    margin-top: 0;
}

.balance-container span {
    font-size: 25px;
    font-weight: lighter;
    margin-top: 10px;
}

.balance-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-right: 30px;;
}

.changer {
    background: #1b76ff;
    color: #fffcff;
    border: none;
    border-radius: 30px;
    padding: 10px 20px;
    font-family: "Roboto", sans-serif;
    font-weight: 500;
    font-size: 15px;
}

.changer:hover {
    cursor: pointer;
    background: #020514 !important;
    transition: all 0.2s;
}

.account-selector-transfer {
    margin-right: 30px;
}

.account-selector-transfer h3{
    font-size: 23px;
    font-family: "Roboto", sans-serif;
    font-weight: 500;
    margin-top: 0;
}

.row1-transfer {
    display: flex;
    margin: 0;
    padding: 0;
    justify-content: space-between;
}

.transfer-main {
    height: 82vh;
    margin-left: 10px;
}

.left {
    display: flex;
    flex-direction: column;
    margin: 10px;
    width: 35vw;
    margin-left: 40px;
}

.left h1 {
    margin-top: 10px;
    font-size: 50px;
    font-family: "DM Serif Text", serif;
    font-weight: lighter;
    font-style: italic;
}

.left2 {
    display: flex;
    flex-direction: column;
    margin: 10px;
    width: 35vw;
    margin-left: 40px;
}

.left2 h1 {
    margin-top: 10px;
    font-size: 50px;
    font-family: "DM Serif Text", serif;
    font-weight: lighter;
    font-style: italic;
}


.left3 {
    display: flex;
    flex-direction: column;
    margin: 10px;
    width: 95vw;
    margin-left: 30px;

}

.left3 h1 {
    margin-top: 10px;
    font-size: 50px;
    font-family: "DM Serif Text", serif;
    font-weight: lighter;
    font-style: italic;
}





.account2:hover {
  cursor: pointer;
  font-weight: 500;
}

.accounts-card2 {
  background: #fe4a23;
  color: #fffcff;
  width: 40vw !important;
}
.accounts-card2 button:hover {
  background: #020514 !important;
  color: #fffcff;
}

.accounts-card2 button {
  background: #fffcff;
  color: #020514;
  border: none;
}

.account:hover {
  cursor: pointer;
  font-weight: 500;
}

.accounts-card {
  background: #1b76ff;
  color: #fffcff;
}
.accounts-card button:hover {
  background: #020514 !important;
  color: #fffcff;
}

.accounts-card button {
  background: #fffcff;
  color: #020514;
  border: none;
}

.gridRow {
  overflow-x: hidden; /* Elimina el desplazamiento horizontal */
  overflow-y: auto; /* Activa el desplazamiento vertical si es necesario */
  margin-top: 0 !important;
  max-height: 75%;
}

.grid {
  margin-top: 0 !important;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}

.gridRow::-webkit-scrollbar {
  display: none;
}

.assets-carrousel::-webkit-scrollbar {
    width: 8px; /* Ancho de la barra (horizontal: height) */
}

.assets-carrousel::-webkit-scrollbar-track {
    background: transparent; /* Hace invisible la pista (track) */
}

.assets-carrousel::-webkit-scrollbar-thumb {
    background: black; /* Color del indicador (thumb) */
    border-radius: 4px; /* Bordes redondeados para el indicador */
}

.assets-carrousel {
    scrollbar-width: thin; /* Para navegadores que soporten esta propiedad (como Firefox) */
    scrollbar-color: #020514 transparent; /* Color del thumb y del track */
}

.grid li {
  display: flex;
  align-items: center;
  list-style: none; /* Elimina el estilo de lista */
  padding: 10px;
  text-align: center; /* Centra el texto */
  color: #fffcff;
  margin: 10px;
  border-bottom: 1px solid #fffcff;
  width: 150px;
}

.grid li span {
  margin-right: 20px;
}

.espt:hover {
  cursor: pointer;
  background: #1b76ff !important;
  transition: all 0.2s;
  border-color: #161d2c !important;
}

.third {
  width: 40vw !important;
  display: block !important;
}

.carrussel::-webkit-scrollbar {
  display: none;
}

.item2 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #020514;
}

.item {
  list-style: none;
}

.especial {
  background: #020514;
  color: #fffcff;
  border: 1px solid #020514;
  border-radius: 50px;
  padding: 10px 20px;
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  font-size: 15px;
}

.especial:hover {
  cursor: pointer;
  background: #1b76ff !important;
  transition: all 0.2s;
}

.card1 {
  padding: 20px;
  border: 1px solid #020514;
  width: 25vw;
  height: 36vh;
  border-radius: 30px;
  margin-right: 20px;
}

.container-content {
  margin: 30px 10px;
  display: flex;
  font-family: "roboto";
}

.second {
  height: 130px !important;
  background: #161d2c !important;
  color: #fffcff;
}

.row1 {
  display: flex;
  justify-content: space-between;
}

.row2-wrapper {
  display: flex;
  align-items: center;
}

.ticket {
  font-size: 20px;
  font-weight: 400;
  border: 1px solid #020514;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 5px 10px;
  border-radius: 30px;
  width: 100px;
  margin-right: 10px;
}

.card-wrapper {
  background: #f6ef68;
  border-radius: 30px;
  padding: 20px;
  margin: 10px;
  width: 21vw;
  height: 40vh;
  font-family: "Quantico";
  font-weight: 300;
  font-style: normal;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.main-body {
  margin-top: 20px;
}

.logo {
  display: flex;
  align-items: center;
  font-weight: 300;
  font-size: 15px;
}

.wrapper-index {
  background: #fffcff;
}

.main-body {
  width: 100%;
  display: flex;
}

.main-index {
  background: #020514;
  margin: 10px;
  border-radius: 20px;
  padding: 15px;
  font-family: "DM Serif Text", serif;
  font-weight: lighter;
  font-style: italic;
}

.navbar {
  color: #fffcff;
  display: flex;
  justify-content: space-between;
}

.navbar div {
  display: flex;
  align-items: center;
  justify-content: center;
}

.options button {
  background: none;
  color: #fffcff;
  border: 1px solid #3c404d;
  border-radius: 10px;
  padding: 17px;
  border-radius: 30px;
  font-family: "Roboto", sans-serif;
  font-size: 15px;
  display: flex;
  align-items: center;
}

.options button.active {
  background: #f6ef68;
  color: #020514;
  fill: #f6ef68 !important;
  font-weight: 500;
}

.options button:hover {
  cursor: pointer;
  background: #1b76ff;
  transition: all 0.2s;
}

.options button img {
  margin-right: 5px;
}

.notis {
  margin-right: 10px;
  border: 1px solid#3c404d;
  padding: 10px;
  border-radius: 50%;
}

.notis:hover{
    cursor: pointer;
    background: #1b76ff;
    transition: all 0.2s;
}
</style>
