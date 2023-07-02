<template>
    <div class="billitem">
        <input placeholder="Item Name" class="big" type="text" v-model="name" @input="emitUpdates">
        <input placeholder="Qty" type="text" v-model="quantity" :disabled="nameEntered">
        <input placeholder="Price" type="text" v-model="price" :disabled="nameEntered">
        <input type="text" readonly :value="total">
        <button @click="emit('delete')"><ion-icon name="trash-outline"></ion-icon></button>
    </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const emit = defineEmits(["change", "delete"])

const name = ref("")
const quantity = ref("")
const price = ref("")

const nameEntered = computed({
    get() {
        return !name.value.length
    }
})


const total = computed({
    get() {

        return quantity.value * price.value
    }
})
watch(total, () => {
    emitUpdates()
})

const emitUpdates = () => {
    emit("change", {name:name.value, total:total.value})
}

</script>

<style lang="scss" scoped>
.billitem {
    width: 100%;
    height: 50px;

    margin: 10px 0;

    display: flex;
    justify-content: space-around;
    align-items: center;

    background: #ececec;
    border-radius: 10px;

    input {
        height: 40px;
        width: 50px;
        outline: none;

        border: none;
        background: transparent;
    }

    .big {
        width: 200px;
    }

    button {
        outline: none;
        border: none;

        // margin: 10px;

        height: 50px;
        width: 50px;
        border-radius: 25px;

        display: flex;
        align-items: center;
        justify-content: center;

        

        font-size: 18px;
    }

}
</style>