<script setup>
// import formInput from './components/formInput.vue'
// import listItem from './components/listItem.vue'
import { createApp, ref, computed, reactive, watch, watchEffect, nextTick, onMounted } from 'vue';

const inputValue = ref('');
const list = ref([]);

const handleInputValueChange = (e) => {
  inputValue.value = e.target.value;
}

const handleSubmit = () => {
  const timestamp = Math.floor(Date.now() / 1000);
  if (inputValue.value === "") {
    alert("您輸入為空值")
  } else {
    list.value.push({ id: timestamp, name: inputValue.value, isCompleted: false });
    console.log(list.value)
    inputValue.value = "";
  }
}

const delThisList = (index) => {
list.value.splice(index, 1);
}

const editTodo = (index) => {
  const cacheName = list.value[index].name;
  list.value[index].name = prompt("請輸入修改後的名稱", cacheName);
}


</script>

<template>
  <div class="container m-[auto]">
    <h1 class="text-[32px] font-bold my-[20px]">
      ToDo List
    </h1>

    <div class="flex justify-center pb-12">
      <input type="text" class="border-[1px] w-[77%] rounded pl-3" placeholder="New Task" autocomplete="off"
        :value="inputValue" @input="handleInputValueChange" @keyup.enter="handleSubmit" />
      <div class="pl-8">
        <button type="submit" class="bg-[#0a58ca] text-white w-[60px] h-[38px] rounded-md"
          @click="handleSubmit">Add</button>
      </div>
    </div>

    <ul>
      <li v-for="(item, index) in list" :key="index" class="border-[1px] border-[#f1f1f1] border-solid flex py-[30px]">
        <label class="pl-[30px]" :class="(item.isCompleted) ? 'line-through text-[#888]' : ''">
          <input type="checkbox" name="type" v-model="item.isCompleted" />
          <span class="pl-[30px]">{{ item.name }}</span>
        </label>
        <a class="cursor-pointer m-auto mr-[35px]" @click="delThisList(index)">
          <svg viewBox="0 0 24 24" style="color: red; width: 24px; height: 24px;">
            <path fill="currentColor"
              d="M9,3V4H4V6H5V19A2,2 0 0,0 7,21H17A2,2 0 0,0 19,19V6H20V4H15V3H9M9,8H11V17H9V8M13,8H15V17H13V8Z" />
          </svg>
        </a>
        <input type="checkbox" name="type" @click="editTodo(index)" />
      </li>
    </ul>
    <!-- <formInput></formInput> -->
    <!-- <listItem></listItem> -->
  </div>
</template>

<style scoped></style>