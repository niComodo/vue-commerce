<template>
    <div class="carrello">
        <div v-if="carrello.length > 0">
            <a href="#" class="svuota" @click.prevent="svuotaCarrello">svuota il carrello</a>
        </div>

        <div v-for="(prodotto, key) in carrello" v-bind:key="key">
            <span>{{ prodotto.nome }} - {{ prodotto.prezzo }}</span>
            <span class="btn remove" @click="rimuovi(prodotto, key)">x</span>
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
        rimuovi(prodotto, key) {
            this.carrello.splice(key, 1)
            bus.$emit('carrello:rimosso')
            bus.$emit('prodotto:incrementaQta', prodotto)
        },
        svuotaCarrello() {
            this.carrello = [];
            bus.$emit('carrello:svuota')
        }
    },
    mounted() {
        bus.$on('prodotto:aggiungi', (prodotto) => {
            if (prodotto.qta > 0) {
                prodotto.qta--
                this.carrello.push(prodotto)
                bus.$emit('carrello:aggiunto')
            }
        });
    }
}
</script>

<style scoped>
.svuota,
.remove {
    color: red;
}
</style>