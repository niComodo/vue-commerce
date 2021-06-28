<template>
    <div class="singolo-prodotto">
        <span>{{ prodotto.nome }} - {{ prodotto.prezzo }}</span>
        <span><button @click="aggiungi">aggiungi</button></span>
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
            bus.$emit('product:add', this.prodotto);
        }
    }
}
</script>

<style scoped>

</style>