<template>
    <div id="app">
        <Message :msg="notification.msg" :type="notification.type"/>
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Vue-commerce"/>

        <!--PRODOTTI-->
        <h2>I nostri prodotti</h2>

        <div class="lista-prodotti">
            <Prodotto v-for="(prodotto, key) in prodotti" v-bind:key="key"
                      :prodotto="prodotto"/>
        </div>

        <!--CARRELLO-->
        <h2>Il tuo carrello</h2>
        <Carrello/>
    </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Prodotto from './components/Prodotto.vue';
import Carrello from './components/Carrello.vue';
import Message from './components/Message.vue';
import bus from "@/bus";

export default {
    name: 'App',
    data() {
        return {
            prodotti: [
                {
                    nome: 'Aspirapolvere',
                    prezzo: 10,
                    qta: 1
                },
                {
                    nome: 'Dentifricio',
                    prezzo: 15,
                    qta: 2
                },
                {
                    nome: 'Papera di gomma',
                    prezzo: 32,
                    qta: 3
                }
            ],
            notification: {
                msg: null,
                type: 'success'
            }
        }
    },
    components: {
        HelloWorld,
        Prodotto,
        Carrello,
        Message,
    },
    methods: {
        notify(msg, type='success') {
            this.notification.msg = msg
            this.notification.type = type
        }
    },
    mounted() {
        bus.$on('carrello:rimosso', () => this.notify('prodotto rimosso', 'danger'))
        bus.$on('carrello:aggiunto', () => this.notify('prodotto agginto'))
        bus.$on('carrello:svuota', () => this.notify('carrello svuotato', 'warning'))
        bus.$on('prodotto:terminato', () => this.notify('prodotto terminato', 'danger'))
        bus.$on('prodotto:incrementaQta', (prodotto) => {prodotto.qta++});
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

.lista-prodotti {
    padding: 0;
    list-style-type: none;
}
.btn {
    margin-left: 10px;
    font-weight: bold;
    cursor: pointer;
}
</style>
