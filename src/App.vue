<script setup>
import { ref } from 'vue'

const items = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
    isEditing: false,
    tempName: ''
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 15,
    isEditing: false,
    tempName: ''
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 30,
    isEditing: false,
    tempName: ''
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10,
    isEditing: false,
    tempName: ''
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25,
    isEditing: false,
    tempName: ''
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20,
    isEditing: false,
    tempName: ''
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18,
    isEditing: false,
    tempName: ''
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20,
    isEditing: false,
    tempName: ''
  }
])

// 庫存
const increaseStock = (item) => {
  item.stock++
}

const decreaseStock = (item) => {
  if (item.stock > 0) {
    item.stock--
  }
}

// 編輯
const editItemName = (item) => {
  item.tempName = item.name
  item.isEditing = true
}

const confirmEditing = (item) => {
  item.name = item.tempName
  item.isEditing = false
}

const cancelEditing = (item) => {
  item.isEditing = false
  item.tempName = ''
}
</script>

<template>
  <div class="container">
    <div>
      <header></header>
      <div>
        <table>
          <thead>
            <tr>
              <th scope="col">品項</th>
              <th scope="col">描述</th>
              <th scope="col">價格</th>
              <th scope="col">庫存</th>
              <th scope="col">修改品項</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, key) in items" v-bind:key="item.id">
              <td>
                <template v-if="item.isEditing">
                  <input v-model="item.tempName" />
                </template>
                <template v-else>
                  {{ item.name }}
                </template>
              </td>
              <td>
                <small>{{ items[key].description }}</small>
              </td>
              <td>
                {{ items[key].price }}
              </td>
              <td>
                <button @click="decreaseStock(item)">-</button>
                {{ items[key].stock }}
                <button v-on:click="increaseStock(item)">+</button>
              </td>
              <td>
                <template v-if="item.isEditing">
                  <button @click="confirmEditing(item)">確認</button>
                  <button @click="cancelEditing(item)">取消</button>
                </template>
                <template v-else>
                  <button @click="editItemName(item)">編輯</button>
                </template>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  margin: auto 0;
  display: flex;
  justify-content: center;
}

th,
td {
  padding: 8px;
  text-align: center;
}

button {
  margin: 0 5px;
}
</style>
