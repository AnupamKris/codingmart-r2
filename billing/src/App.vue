<script setup>
import { computed, ref } from "vue"
import BillItem from "./components/BillItem.vue";

const items = ref({})
const index = ref(0)
const updateValues = (data, index) => {
  console.log(data);
  items.value[index] = data
}

const addNewItem = () => {
  let vals = Object.values(items.value)
  let last;

  if (vals.length) {
    last = vals[vals.length - 1]
  }

  console.log(vals, last);

  if ((last && last.name.length > 0) || vals.length == 0) {
    console.log("adding item", index.value);
    items.value[index.value] = {name:"", total:0}
    index.value++
  }
}

const deleteItem = (index) => {
  console.log("deleting", index);
  delete items.value[index]
}

const total = computed({
  get() {
    let s = 0;
    Object.values(items.value).forEach(element => {
      s += element.total
    });

    return s
  }
})
</script>

<template>
  <main>
    <div class="nav">
      <h1>
        Billing
      </h1>
    </div>
    <div class="items">
      <BillItem v-for="(item, key) in items" :key="key" @change="(data) => updateValues(data, key)"
        @delete="deleteItem(key)" />
    </div>
    <div class="total">
      <span>Total</span><span>{{ total }}</span>
    </div>

    <button class="add" @click="addNewItem"><ion-icon name="add-outline"></ion-icon></button>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;

  width: 100%;
  height: 100%;

  .items {
    width: 90%;
  }

}

.nav {
  height: 60px;
  width: 100%;

  display: flex;
  align-items: center;
  background: #ececec;

  h1 {
    font-size: 24px;
    margin-left: 20px;
    font-weight: 400;
  }

}

.add {
  outline: none;
  border: none;

  margin: 10px;

  height: 50px;
  width: 50px;
  border-radius: 25px;

  display: flex;
  align-items: center;
  justify-content: center;

  background: #0088ff;
  color: #ffffff;

  font-size: 48px;
}

.total {
  width: 200px;
  height: 50px;

  margin: 10px;
  margin-right: 35px;

  align-self: flex-end;

  display: flex;
  justify-content: space-around;
  align-items: center;

  background: #ececec;
  border-radius: 10px;

  font-size: 14px;

  p {
    width: 200px;
  }
  
  span {
    text-align: center;
    width: 50px;
  }
}
</style>
