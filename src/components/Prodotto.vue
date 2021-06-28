<template>
    <div class="singolo-prodotto">
        <span>{{ prodotto.nome }} - {{ prodotto.prezzo }}€ (qta: {{prodotto.qta}})</span>
        <span class="btn add" @click="aggiungi">+</span>
    </div>
</template>

<script>
import bus from '@/bus';

export default {
    props: {
        prodotto: Object,
    },
    methods: {
        aggiungi() {
            if (this.prodotto.qta === 0) {
                bus.$emit('prodotto:terminato')
                return
            }
            bus.$emit('prodotto:aggiungi', this.prodotto)
        }
    }
}
</script>

<style scoped>
.add {
    color: green;
}
</style>