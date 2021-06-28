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
// import bus from '@/bus';

export default {
    name: 'App',
    data() {
        return {
            prodotti: [
                {
                    nome: 'Aspirapolvere',
                    prezzo: 10
                },
                {
                    nome: 'Dentifricio',
                    prezzo: 15
                },
                {
                    nome: 'Papera di gomma',
                    prezzo: 32
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
            this.notification.msg = msg;
            this.notification.type = type;
        }
    },
    mounted() {
        bus.$on('cart:removed', () => this.notify('prodotto rimosso', 'alert'));
        bus.$on('cart:added', () => this.notify('prodotto agginto'));
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
</style>
