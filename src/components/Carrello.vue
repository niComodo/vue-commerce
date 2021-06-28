<template>
    <div class="carrello">
        <div v-for="(prodotto, key) in carrello" v-bind:key="key">
            <span>{{ prodotto.nome }} - {{ prodotto.prezzo }}</span>
            <span><button @click="rimuovi(key)">rimuovi</button></span>
        </div>

    </div>
</template>

<script>

import bus from "@/bus";

export default {
    data() {
        return {
            carrello: []
        };
    },
    methods: {
        rimuovi(key) {
            this.carrello.splice(key, 1);
            bus.$emit('cart:removed');
        }
    },
    mounted() {
        bus.$on('product:add', (prodotto) => {
            this.carrello.push(prodotto);
            bus.$emit('cart:added');
        });
    }
}
</script>