<template>
    <p v-if="msg" class="alert" :class="{'text-green': this.type === 'success', 'text-red': this.type === 'alert'}">{{ msg }}</p>
</template>

<script>

export default {
    props: {
        msg: String,
        type: {
            default: 'success',
            type: String
        }
    }
}
</script>

<style scoped>
.alert {
    display: block;
    padding: 10px;
    background: lightgrey;
}
.text-green {
    color: green;
}
.text-red {
    color: red;
}
</style>